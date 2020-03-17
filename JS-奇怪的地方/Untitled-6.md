6-1 用不同方式建立物件:

        function Person(){

            this.firstname = 'John';
            this.lastname = 'Doe';

        }

        var john = new Person();
        console.log(john); // { firstname : 'John', lastname : 'Doe' }

    用 new 就建立空物件，小括號 () 呼叫函數，

    函數裡的 this 指向 Person 物件，並建立名稱/值，

    如果在函數加上:

        retrun { greeting: 'i got in the way' };

    就回傳 { greeting: 'i got in the way' }，

    但不寫 retrun，也有 new，空物件就被創造也呼叫，設定 this，
    
    this 會指向空物件，就成了函數建構子，多寫一個也是:

        var jane = new Person();

        console.log(jane); // { firstname : 'John', lastname : 'Doe' }

    但 firstname 和 lastname 的值想要不一樣，可加上:

        function Person(firstname, lastname){

            this.firstname = firstname;
            this.lastname = lastname;

        }

        var john = new Person('John','Doe');

        console.log(john); // { firstname : 'John', lastname : 'Doe' }

        var jane = new Person('Jane', 'Doe');

        console.log(jane); // { firstname : 'Jane', lastname : 'Doe' }

        函數建構子:一個正常函數用來建立物件。

6-2 當使用函數建構子，就已經設定好原型。

    原型鏈是每個物件都有這個特殊屬性指向其他物件:

        Person.prototype.getFullName = function() {
            return this.firstname + ' ' + this.lastname;
        }

        console.log(john.getFullName()); // John Doe

    如果每個物件都使用功能一樣的函數，每個物件都加入一個，會很占記憶體，

    如果放在原型鏈，從原型鏈取用就能節省記憶體。

6-3 如果沒加 new，會出現 undefined 和錯誤，避免忘記，

    可以在建立時開頭大寫，沒加 new 也比較容易發現。

6-4 只要使用函數建構子，就是在建立物件。

        String.prototype.isLengthGreaterThan = function(limit){
            return this.length > limit;
        }

        console.log('john'.isLengthGreaterThan(3)); // true

    ---------------------------------------------------------

        Number.prototype.isPositive = function(){
            return this > 0;
        }

        3.isPositive(); // 錯誤

        var a = new Number(3); 這不是數值，是物件

        a.isPositive(); // true

    原因是會轉成字串，但不會轉成物件，

    不該用內建的函數建構子在純值上。

6-5 

    var a = 3;

    var b = new Number(3);

    a == b // true，一個純值，另一個物件，因為會轉型，所以 true

    a === b // false，嚴格模式就是 false

    如果有要做一堆函數處理日期或日期運算，可以使用 moment.js。

6-6 

    Array.prototype.myCustomFeature = 'cool!';

    var arr = ['John', 'Jane', 'Jim'];

    for (var prop in arr){
        console.log(prop + ': ' + arr[prop]); 
        
        // 得到陣列裡的東西，包含原型 myCustomFeature: cool!
    }

    如果沒有要使用到原型，可用 for 迴圈。

6-7 Object.create:

        var person = {
            firstname: 'Default',
            lastname: 'Default',
            greet: function() {
                return 'Hi ' + this.firstname;
            }
        }

        var john = Object.create(person);
        console.log(john);

    顯示空物件，但 person 裡的名稱/值，在原型裡，

    裡面的名稱/值是可以覆蓋:

        john.firstname = 'John';

        john.lastname = 'Doe';

        console.log(john);
    
    原型還在，但呼叫相同名稱是 john 新增的物件。

    如果專案需要較舊的瀏覽器或舊的環境，JS 引擎無法支援 Object.create，

    可以用 polyfill: 是引擎缺少的增加功能到程式中，

    讓舊瀏覽器有新型瀏覽器的功能，填補舊引擎所沒有的空缺:

        if (!Object.create){
          Object.create = function (o) {  
            if (arguments.length > 1){
                throw new Error('Object.create implementation'
                + ' only accepts the first parameter.');
            }
            function F(){}
            F.prototype = o;
            return new F();
            };
        }

6-8 關於 class 。

    sytactic sugar:很多方法做到一件事。