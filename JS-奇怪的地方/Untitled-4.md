4-1 物件與點，物件是一群[名稱/值]的組合，值也可以是另一個[名稱/值]。

    另個觀點看物件，物件 (Object) 可以有:
    1.原始設定 (property)，屬性，純值，例:布林、數值、字串。
    2.另一個物件。
    3.函數 (function) ，函數在物件時，稱之為[方法] (method)。

    var person = new Object();

    person["firstname"] = "Tony";
    person["lastname"] = "Alicea";

    var firstNameProperty = "firstname";

    console.log(person[firstNameProperty]); // Tony

    console.log(person.firstname); // Tony
    與兩個 console 顯示相同，不用加""，錯誤範例:console.log(person."firstname");

    放點在後面，語法解析器會自動了解你打的東西是想要傳入字串。

    person.address = new Object();
    person.address.street = "111 Main St."
    person.address.city = "New York";
    person.address.state = "NY";

    點和中刮號是左到右，在記憶體左到右找尋，最後找到值。

    console.log(person.address.street);
    console.log(person["address"]["street"]);

    這兩個本質是相同，找到物件，點 ( . ) 或中刮號 ( [] ) 會尋找屬性。

    最好還是用點運算子，較快較簡潔，好除錯。

4-2 物件實體語法，就是用大括號 ( {} )，

    原先 var person = new Object();

    大括號 var person = {};

    比較快，大括號不是運算子，如果不是用在 if 或迴圈，
    
    JS 會假設你在創造一個的物件，並用冒號區隔名稱/值，
    
    裡面在一個的大括號，就知道是另一個物件，例:第二種。

    第一種:
            var person = new Object();
            person["firstname"] = "Tony";
            person["lastname"] = "Alicea";

            person.address.street = "111 Main St."
            person.address.city = "New York";
            person.address.state = "NY";
    第二種:

            var person = {
                firstname: "Tony",
                lastname: "Alicea",
                address:{
                    street: "111 Main St.",
                    city: "New York",
                    state : "NY"
                }
            };
    
    兩種都是一樣，第二種比較容易寫出來。

    function greet(person); {
        console.log("Hi " + person.firstname);
    }

    greet(Tony); // Hi Tony

    greet({
        firstname: "Mary",
        lastname: "Alicea"
    }); // Hi Mary

    function 也可以透過物件實體語法:大括號來呼叫。

    也可以結合運用，例:

        Tony.address2:{
            street: "333 Second St."
        }
    
    物件實體語法的強大之處，JS 引擎仍然能轉換電腦能懂的東西，

    運用大括號去定義，冒號區隔名稱和值。

    不論物件實體語法還是點，對 JS 引擎 來說就是建立物件到記憶體中，

    還有屬性和方法到記憶體中，因為都是建立同樣東西。

4-3 命名空間:是變數和函數的容器。

    假設:
        
        var greet = 'hello!';

        var greet = 'hola!';

        console.log(greet);

    這樣第一個就會被覆蓋掉，但假如用物件:
    
    偽裝命名空間:

        var english = {
            greet:'hello!'
        };

        var spanish = {
            greet:'hola!'
        };
    
    這樣就不會被覆蓋掉，防止命名衝突。

4-4 JSON (JavaScript Object Notation)，像物件實體語法，

    [ 屬性包在引號裡 ]，在物件都可以，在 JSON 是一定要包，

    技術上來說，JSON 是物件實體語法的子集合，代表在 JSON 有效的，

    物件就是有效，但不是所有物件實體語法在 JSON 有效，
    
    JSON 的規則比較嚴格，所以 JSON 不是 JS 的一部份，

    但受歡迎，因為很簡單的讓 JS 解析他， JS 的內建讓任何物件變 JSON:

    JSON.stringify(物件); 物件轉為 JSON 字串，例:

        '{ "firstname": "Mary","isAProgrammer": true }'
    
        外層單引號，裡面雙引號。

    JSON.parse(JSON 資料); 接受字串，轉為 JS 物件。

4-5 一級函數:別的型別，例:物件、字串、數值、布林所做的事，也都可以對函數做，

            可以變數的值為函數，或函數當參數傳入另一個函數，
            
            可以用實體語法創造函數，可以用多個角度、不同方法去寫函數。

    在記憶體裡的函數物件和其他物件一樣，它是特殊型態的物件，
    
    它有所有物件的特色和其他屬性，可以:

        1.連結純值到名稱/配對。

        2.連結其他物件。

        3.連結其他函數。

        4.JS 的函數不一定要有名字，但它可以有名字。

        5.程式碼所在，可以寫在屬性，用屬性呼叫。



            在 JS 中，函數就是物件，任何物件裡可以擁有屬性，例:

                function greet(){
                    console.log('hi');
                }

                greet.language = 'english';

                console.log(greet);// function 全內容

                console.log(greet.language); // 'english'

4-6 陳述式:會做某些事。

    表示式:程式碼的單位，會形成一個值，這個值不一定要存在變數，例:

    在 console:
        var a;

        a = 3; //回傳 3

        1 + 2; //回傳 3

    意思就是執行完後回傳值、結果，反之，陳述式不會回傳值，例:if，
    
    裡面的表示式可以，三等號會回傳 true 和 false，例:

        if(a === 3) {...略 }

    函數陳述式，會放進記憶體，呼叫會執行，但不會回傳:

        function greet(){
                    console.log('hi');
                }
    
    函數表示式，有等號運算子，會把物件放入記憶體中，
    
    並指向 anonymousGreet 變數的位址，這不是函數真正的名稱，

    只是記憶體位址，就像住址，如範例，函數沒有名字，因為已經知道物件位址的變數，

    這是個匿名函數，呼叫住址就可以執行。

    var anonymousGreet = function() {
        console.log('hi');
    }

    anonymousGreet();

    函數陳述式單純在記憶體執行，讓 JS 知道有個函數在，

    函數表示式則會讓裡面的函數陳述式創造物件，回傳物件，

    但它是變數，不會提升，先呼叫會出現 undefined。

    函數表示式，因為函數是物件，就可以函數當參數，稱為函數程式語言:

        function log(a){
            a();
        }

        log(function(){
            console.log('hi');
        });
    
4-7 by value，by reference，關於變數的東西

    var a = 值，可能是布林、字串、數字

    假設 var b = a;

    也就是 by value:傳入或設定這個值為另一個值拷貝，

    兩個變數就一樣，藉由拷貝一個值到另一個不同的記憶體地點。

    假如有個物件，所有物件都算，包含函數，也就是特殊類型的物件，

    當: var a = {} ，設定變數為物件，仍然會得到一個記憶體，

    這是該物件的記憶體位址，可以參考它，當 var b = a;

    b 不會得到記憶體位址，而是指向 a 的記憶體位址，沒有新物件創造，

    也沒有物件的拷貝被創造，兩個同樣指向同一個位址，當要取用，
    
    也是會指向同樣記憶體位址，稱為 by reference，

    by value 和 by reference 非常不同，最重要的一點是，

    所有物件都是 by reference。

    ( by value )

    var a = 3;
    var b;

    b = a;
    a = 2;

    拷貝 a 的值，創造新的記憶體，值填入 b 的位址，

    改變 a 的值不影響 b 。

    ( by reference )

    var c = { greeting:'hi' };

    var d;

    d = c;

    c.greeting = 'hello';
        
    對所有類型的物件都可以做。

    console.log 出來是一樣，但不是拷貝，而是指向同一個記憶體位址，

    c 改變，console.log 出來也一起被改變。

    mutate:改變某些事、改變一個物件、改變一個值。

    immutable:不可改變。

    function changGreeting(obj) {
        obj.greeting = 'Hola';
    }

    changGreeting(d);
    console.log(c);
    console.log(d);

    一樣改變，指向同一個記憶體位址。

    還要注意一件事，等號運算子會設定新的記憶體空間，

    c 用等號改變，就和 d 不是指向同一個記憶體位址，

    也就不是 by reference，是新的創造物件的方法，
    
    藉由物件實體語法，增加新的記憶體，指向 c，在指向不同於 d 的記憶體位置。

    c = { greeting:'howdy' };
    console.log(c);
    console.log(d);

4-8 this 用 console 是指向全域，如果是用在物件:

    var c = {
        name:'The c object',
        log:function(){
            var self = this;

            self.name = 'Updated c object';
            console.log(self);

            var setname = function(newname){
                self.name = newname;
            }
            setname('Updated again!');
            console.log(self);
        }
    }

    c.log(); // 裡面的 this 指向 c 物件
    
    setname 執行，執行結果是創造一個 window.name，

    而不是參數 'Updated again!'，

    表示 setname 是指向全域物件，即使在自己創造的物件裡，

    確保能用對的物件，加上 var self = this;，

    因為是 by reference 模式，self 會指向和 this 一樣的記憶體位置，

    所以 var self = this; 指向整個物件，物件裡全部改用 self，

    子函數 setname 也是。

4-9 陣列裡可放各種型別的資料；

    var arr = [
            1,
            false,
            {
                name:'Tony',
                address:'111 Main St.'
            },
            fuction(name){
                var greeting ='hello';
            },
            "hello"
        ];

        console.log(arr); // [number,false,Object,function,"hello"]

        如何呼叫陣列裡的函數:

        arr[3](arr[2].name);

4-10 arguments:參數，傳入變數的另一個名稱。

    function greet(firstname, lastname, language){
        console.log(firstname);
        console.log(lastname);
        console.log(language);
    }
    greet();

    在呼叫 greet(); 但不帶參數，其他語言會產生錯誤，

    在 JS，出現 undefined，當裡面只帶一個參數:

        greet("John");

    會從左到右給參數:

        "John"
        undefined
        undefined
    
    意思是沒有給滿也是可以，也可以用預設:

        language = language || 'en';

    也可以用 arguments，

    console.log(arguments);

    出現結果會是斜斜的中括號包著參數，稱為 array-like (像陣列的)，

    它不是陣列，只有一部份的陣列功能，可以在 greet 函數裡使用:

        if(arguments.length === 0){
            console.log('Missing parameters!');
            return;
        }

    來找出參數數量，或抓出來使用:

        console.log(arguments[0]);

    因為不是最好的方法，隨著時間出現新東西，叫做 spread parameter，

    表示如果有傳入函數的參數，可以用 ... 增加一個參數，other也可以命名別的:

        function greet(firstname, lastname, language, ...other){
        console.log(firstname);
        console.log(lastname);
        console.log(language);
        }

    呼叫時，加其他參數:

        greet('John','Doe','es','111 main st.','new york');

    ... 代表任何東西，然後包進這個名稱的陣列。

9-11 重載函數，表示一個函數，能有不同數量的參數，

    在 JS 行不通，因為函數就是物件，但沒關係，

    一級函數能帶進很多選擇，如果想要用不同方式呼叫 greet，例:

        function greet(firstname, lastname, language){
            language = language || 'en'

            if(language === 'en'){
            console.log('Hello ' + firstname + ' ' + lastname);
            }

            if(language === 'es'){
                console.log('Hola ' + firstname + ' ' + lastname);
            }
        }
        greet('John','Doe','en');
        greet('John','Doe','es');

    不同寫法版本，不用傳入這麼多資訊:

        function greetEnglish(firstname, lastname){
            greet(firstname,lastname,'en');
        }

        function greetSpanish(firstname, lastname){
            greet(firstname,lastname,'es');
        }

        greetEnglish('John','Doe');
        greetSpanish('John','Doe');

9-12 加強對於語法解析器的觀念，

    寫的程式不會直接被電腦執行，

    有個中介的程式在所寫的程式與電腦之間，
    
    轉換所寫的程式為電腦懂的東西，例:JS 引擎，

    它包含很多東西在裡面，其中之一是語法解析器，

    它會閱讀所寫的程式碼判斷是否有效，逐字的、

    用一些規則去判斷，決定你要做什麼，這是所寫的程式碼執行前發生的事。

9-13 一定要避免的情況，程式碼結尾的分號(;)要打出來，雖然 JS 引擎會幫你補上，

    但自己打是讓自己知道程式碼的樣子，確保最後結果如預期，而不是給 JS 做決定，
    
    避免 JS 做決定導致顯示結果不如自己要的，例:

        function getPerson(){

            return 
            {
                firstname:'Tony'
            }
        }
        console.log(getPerson());

    原本 console 出來結果是 {firstname: "Tony"}，但出來的是 undefined，

    因為 return 後按下 enter，它就會判斷後面要加分號，並幫你加，
    
    為了預防自動插入分號，所以應該寫成:

        return { // 不要斷行
                firstname:'Tony'
            }

9-14 空格，創造空間的看不見字母，例:Enter鍵、tab鍵、空白鍵，

    可讓程式碼可讀性更高，但不會被執行，JS 對於空格規範很自由，

    可利用這點來幫助自己寫程式碼，例:

        var
            // 斜線可用來上註解，語法解析器會忽略
            firstname,

            // 註解
            lastname,

            // 註解
            language;

        var person = {
            // 註解
            firstname: 'John',

            // 註解
            lastname: 'Doe'
        }

9-15 此節關於 IIFE 立即函數:

    函數陳述式:
        // JS 放到記憶體，直到呼叫才執行。

        function greet(name) {
            console.log('Hello' + name);
        };
        greet('John');

    函數表現式:
        // 設定變數，等於匿名函數，

            一開始不會放進記憶體，會先創造函數物件，

            可用指向它記憶體位置的變數呼叫。

        var greetFunc = function(name){
            console.log('Hello' + name);
        };
        greetFunc('John');

    立即呼叫的函數表現式，IIFE:
        在函數後加個呼叫的括號。

        在不加後面括號的情況去  console.log(greeting);

        ，顯示出完整函數。

        在加上後面括號的情況去  console.log(greeting);

        ，回傳值 Hello John
        
        ，如果是 console.log(greeting());

        ，會出現錯誤，console.log 裡的 greeting 是字串，

        因為立即呼叫回傳字串，在傳入 greeting。

        var greeting = function(name){
            return 'Hello' + name;
        }('John');
    
    如果在空白頁，打數字 3;

    ，還是一段字串'Hello'

    ，或是物件{ name:John }

    ，結果沒發生什麼，沒出現錯誤

    ，如果是函數:

        function(name){
            return 'Hello' + name;
        }

    則出現錯誤，原因是語法解析器讀取到 function，

    預期這是個函數陳述式，會想要有個名稱。

    要不出現錯誤，就不讓它成為函數陳述式，

    也就讀取第一個字不是 function，做法是:

        (function(name){
            return 'Hello' + name;
        });

    括號是運算子，通常用在表現式，例:( 3 + 4 )*2，

    因為 JS 知道括號裡是表現式，所以執行沒有出現錯誤，

    放進括號，就是最常見的立即函數，同時間創造並執行:

        (function(name){
            console.log(Hello' + name);
        }('John'));

    執行括號放外面或裡面都可以。

9-16 使用 IIFE 立即函數，全域不會佔記憶體，和別人合作不會有程式衝突。

    也可以取用全域或修改:

        (function(globel, name){
            globel.greeting = 'Hello';

            console.log(Hello' + name);

        }(window, 'John'));

    假設全域有 var greeting = 'Hola';

    ，就會被修改。

9-17 閉包，例:

        function greet(whattosay){

            return function(name){
                console.log(whattosay + '' + name);
            }
        }
        greet('Hi')('Tony');

        var sayHi = greet('Hi');
        sayHi('Tony');

        因為函數是物件，可以當成值回傳。

9-18 閉包二，例:

        function buildFunctions(){

            var arr = [];

            for(var i = 0; i < 3; i++){
                arr.push(function(){
                    console.log(i);
                })
            }
            return arr;
        }

        var fs = buildFunctions();

        fs[0]();
        fs[1]();
        fs[2]();
    
    此章節背後原理不懂。

9-19 閉包三，例:

    function makeGreeting(language) {

        return function(firstname, lastname) {

            if (language === 'en'){
                console.log('Hello ' + firstname + ' ' + lastname)
            }

            if (language === 'es'){
                console.log('Hola ' + firstname + ' ' + lastname)
            }
        }
    }

    var greetEnglish = makeGreeting('en');
    var greetSpanish = makeGreeting('es');

    greetEnglish('John', 'Doe');
    greetSpanish('John', 'Doe');

9-20 閉包與回呼，例:

    function sayHilater(){

        var greeting = 'Hi';

        setTimeout(function() {
            
            console.log(greeting);

        }, 3000);
    }

    sayHilater();

    回呼函數:某個函數執行完，你給它執行函數。

9-21 關於call()、apply()、bind():

            var person = {
                firstname:'John',
                lastname:'Doe',
                getFullName: function(){

                    var fullname = this.firstname + ' ' + this.lastname:
                    return fullname;

                }
            }

            var logName = function(lang1, lang2){
                
                console.log('Logged: ' + this.getFullName());
                
            }

            logName();

        呼叫 logName(); 裡面的 this 是指向全域，所以出現錯誤，

        要控制 this 指向:

            var logPersonName = logName().bind(person);

        函數 logName() 的 this 就指向物件 person，

        也可以寫在函數後面:

            var logName = function(lang1, lang2){
                
                console.log('Logged: ' + this.getFullName());
                
            }.bind(person); // bind 接在後面

            logName(); // 呼叫

        或是指向和帶值:

            var logName = function(lang1, lang2){
                
                console.log('Logged: ' + this.getFullName());
                console.log('Arguments ' + lang1 + ' ' +lang2);
                
            }

            var logPersonName = logName.bind(person);
            logPersonName('en');

        用 call 呼叫，後面帶值:

            logName.call(person,'en', 'es');

        用 apply 呼叫，後面帶值是用陣列:

            apply(person, ['en', 'es']);

        也可以寫在後面，用 IIFE:

            (function(lang1, lang2){
                
                ....略

                }).apply(person, ['en', 'es']);

        運用:

            var person2 = {
                firstname: 'Jane',
                lastname: 'Doe'
            }

            person.getFullName.apply(person2);

        用 person 物件理的函數，帶入 person2 的值去執行。

        運用 2:

            function multiply(a, b){
                reture a*b;
            }

            var multipleByTwo = multiply.bind(this, 2);

            multipleByTwo(4));

            bind 後面帶物件，也可帶值，在這帶值就像是:

            function multipleByTwo(b){

                var a = 2;
                reture a*b;
            }

            如果後面把值帶滿:

            var multipleByTwo = multiply.bind(this, 2, 3);

            multipleByTwo(4);

            顯示仍然是 2 * 3 = 6

            function currying:建立一個函數的拷貝，並設定預設的參數。

9-22 函數程式設計，原先:

        var arr1 = [1,2,3];

        var arr2 = [];

        for (var i = 0; i < arr1.length; i++) {

            arr2.push(arr1[i] * 2);

        }

        console.log(arr1); // 1 2 3
        console.log(arr2); // 2 4 6

    簡潔版:

        function mapForEach (arr, fn){

            var newArr = [];
            for (var i = 0; i < arr.length; i++){
                newArr.push(
                    fn(arr[i])
                )
            };

            return newArr;
        }

        var arr1 = [1,2,3];

        var arr2 = mapForEach (arr1, function(item) {
            reture item * 2
        });

        console.log(arr1); // 1 2 3
        console.log(arr2); // 2 4 6

    好處是可以輕鬆修改:

        var arr3 = mapForEach (arr1, function(item) {
            reture item > 2
        });

        console.log(arr3); // ture flase flase

    在函數中沒用到 this，把 limiter 參數為 1，
    
    mapForEach 則把 arr1 帶進 item 去比較:

        var checkPastLimit = function(limiter ,item){
            return item > limiter;
        }

        var arr4 = mapForEach(arr1, checkPastLimit.bind(this, 1));

        console.log(arr4); // false true true

    覺得寫 bind 會寫太長，可以寫:

        var checkPastLimitSimplified = function(limiter){
            return function( limiter ,item ){
                return item > limiter;
            }.bind(this, limiter);
        };

        var arr5 = mapForEach(arr1, checkPastLimitSimplified(2));

        console.log(arr5); // false false true

9-23 underscore.js，開源教材。
     
     lodash，和 underscore.js 相同性質。