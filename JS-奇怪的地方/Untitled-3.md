3-1 動態型別:不用告訴 JS 你的變數是何種型別(不用宣告變數型別)，

    也不用在程式裡寫出來，在執行的時後會自動切換型別。
    
    跟其他程式語言不同，例:Java、c#，是靜態型別。

3-2 純值:資料的型別，一個值，不是物件。

    JS 有六種基本型別，

    1.undefined:表示不存在或是所有變數的初始值，不應該設定變數等於 undefined。

    2.null(空值):表示不存在或是空值，較適合設定變數表示空值。

    3.boolean(布林值):用 true 或 false 表示，小寫。

    4.numder(數值):JS 唯一的數值型態，是浮點數，表示有小數點在後面，
    
                   不像其他程式語言，可能有整數型態或其他特定數值型態，JS 只有一種。

    5.string(字串):一連串字符組成，單引號或雙引號包覆內容來表示。

    6.symbol(符號):ES6 版本，此節只提一下子。

3-3 運算子:需要兩個參數來回傳一個結果，例:
    
    var a = 3 + 4;
    console.log(a);

    得到的是 7，加號就是運算子，是個函數，但不用像一般函數一樣呼叫方式，

    常見運算子:加(+)、減(-)、乘(*)、除(/)、餘數
    
            、大於、小於(>、<)、等於(=)
    
    ，大於、小於、等號是回傳布林值

3-4 運算子的優先性:表示哪個運算子優先被運算。

    相依性:運算子被計算的順序，有左到右(左相依)、右到左(右相依)。

    當一行程式有很多運算子時，優先性能夠幫助判斷誰先，
    
    但如果全部的運算子優先性相同，就要看相依性。
    
    基本運算的優先性就是先乘除、餘數，後加減，
    
    有括號就最先處理括號裡的內容。

    相依性則要看規則，例:

        var a = 2, b = 3, c = 4;
        a = b = c;
        console.log(a,b,c);

    得到的全是 4，等號相依規則是右到左，處理方式:
    (我的解釋:右到左去賦予)
        a = b = c;

        會先處理右邊參數 b 和 c，
        
        b = c 回傳 4，

        a = 4。

        優先性順序權重表:
        https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence

3-5 強制轉型:轉換一個值的型別。

    var a = 1 + "2";

    console.log(a); //得到字串 12

    數字 1 會被強制轉換成字串。

3-6 console.log(1 < 2 < 3);//得到 true

    console.log(3 < 2 < 1);//得到也是 true

    原因是:當運算子權重都相同，就看相依性，< 是左到右(左相依)，

    所以處理是:

        3 < 2 //得到 flase

        flase < 1 //得到 true

    flase 會被強制轉成 0，(true 會被轉換成 1)，

    當轉換後，0 確實小於 1，但在人類角度是錯的，

    JS 引擎角度是合理的。

    console.log(1 < 2 < 3); 得到 true 也是，

    1 < 2 得到 true，true < 3，true 轉換成 1，

    1 < 3 得到 true。

    可能 Numder() 試著轉換，

    Numder(undefined);//NaN 無法被轉換，

    Numder(null);// 0

    undefined 和 null 意思不存在，轉換卻不同，
    
    例:

        3 == 3 // true
        3 == "3" // ture

        "" == 0 // ture
        "" == false // ture

        false == 0 // ture
        var a = false;
        a == 0 // ture

        false == 0 // ture
        null == 0 // false，剛剛 Numder(null) 轉換等於 0，
        
        但現在是 false，null在比較的時候不會轉換，這造成很多疑問和問題，

        被視為這個語言的缺點，所以可以用三等號(===)，

        === 不會轉換型別，在比較時比較不會出錯，也盡量使用 ===。

        比較運算子網址:
        https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness

3-7 boolean 轉換 undefined 和 null 範例。

3-8 預設值，例: 

    ture || false // 得到 ture

    undefined || "hello" // 得到 "hello"，他會強制轉換成 ture，

    就像 boolean("hello");。

    "hi" || "hello" // 得到 "hi"，因為他回傳第一個，被轉換成 ture，

    0 || 1 就會被轉換成 false || ture，回傳 1，

    undefined || "hello" // 得到 "hello"

    null || "hello" // 得到 "hello"

    "" || "hello" // 得到 "hello"

    運算子會回傳 "hello"，並覺得是 ture，所以可以這樣寫:

    function greet( name ){
        name = name || "YOUR name here"

        // || 的權重比 = 高，所以 || 先執行

        console.log("Hello " + name)
    }

    greet(); // "Hello YOUR name here"

    而不是 undefined，帶值進去也是可以，

    greet("Tony"); // "Hello Tony"

    也可以用 if，但這寫法簡潔些，但要帶值要注意 0，

    0 會被轉換成 false，這是特例，大多時候這樣做很好，

    greet(0); // "Hello YOUR name here"

3-9 當使用框架或於別人合作，例:

    <script src="lib1.js"></script>
    裡面放: var libraryName = "Lib 1";

    <script src="lib2.js"></script>
    裡面放: var libraryName = "Lib 2";

    <script src="app.js"></script>
    裡面放: console.log(libraryName);

    會出現 "Lib 2"，因為 "Lib 1" 被蓋掉了，要解決框架衝突，

    可以在 lib2.js 寫:

        window.libraryName = window.libraryName || "Lib 2";

    可以檢查全域執行環境，如果有，會出現 "Lib 1"，就可不使用這變數名稱，

    如果沒有，window.libraryName || "Lib 2"; 判定 undefined，

    並在 console.log(libraryName); 出現 "Lib 2"，
    
    這是在檢查全域命名空間，或全域物件，看是否已經有那個名稱。
