5-1 繼承，一個物件取用另一個物件的屬性和方法。

5-2 此節用錯誤範例去理解原型鏈，建議直接觀賞服用。

5-3 此節在說數值、字串、布林、陣列、物件、函數，都有原型鏈，除了基本物件:

        var a = {};

        var b = function(){};

        var c = [];

    chrome 的 console:

        a._proto_.(出現的常用內建函數)

        b._proto_.(出現的常用內建函數)

        c._proto_.(出現的常用內建函數)

5-4 Reflection:一個物件可以看見自己的東西，然後改變自己的屬性和方法。

    例:

        var person = {
            firstname: 'Default',
            lastname: 'Default',
            getFullName: function(){
                return this.firstname + ' ' + this.lastname;
            }
        }

        john._proto_. = person;

        var john = {
            firstname: 'john',
            lastname: 'Doe'
        }

        for (var prop in john){ //類似 for 迴圈，會遍歷物件每個東西
            
            console.log(prop + ': ' + john[prop]);
            
            // prop 是名稱，john[prop] 用名稱取值
        }

    chrome 的 console 顯示 john 物件裡的內容，
    
    和 _proto_ 的 getFullName，如果加上:

    for (var prop in john){
            
            if (john.hasOwnProperty(prop)){

                console.log(prop + ': ' + john[prop]);

            } // 只對基本物件
        }
    
     chrome 的 console 只顯示 john 物件裡的內容。

     後面在說明 underscore.js 框架內程式細節。

