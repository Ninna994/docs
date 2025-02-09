# JavaScript CheatSheet

## by Ninna

### Table of Contents

- [JavaScript CheatSheet](#javascript-cheatsheet)
  - [by Ninna](#by-ninna)
    - [Table of Contents](#table-of-contents)
    - [Shortcuts Atom and Browser](#shortcuts-atom-and-browser)
    - [Variables and Comments](#variables-and-comments)
    - [Data types-Primitive](#data-types-primitive)
    - [Truthy and Falsy values](#truthy-and-falsy-values)
    - [Operators](#operators)
    - [Decision making if/elseif, switch](#decision-making-ifelseif-switch)
    - [Functions](#functions)
    - [Arrays](#arrays)
    - [Objects](#objects)
    - [Loops](#loops)
    - [Hoisting Scope and This](#hoisting-scope-and-this)

### Shortcuts Atom and Browser

1. **Ctrl+Shift+J** otvara console u Chrome-u
1. **cl** - console.log(obj);
1. **al** - alert('msg');
1. **pm** - prompt('msg');
1. **fun** - function block

### Variables and Comments

* Single line comments _//_
* Multi line comments _/**/_
* Always use **camelCase**
* Only can start with _letter, $_ or _underscore_
* Cannot give variables reserved names
* Declare **multiple variables** in one line and assign values later

    ```JavaScript
      var job, isMarried;
      job = 'programmer';
      isMarried = true;
    ```

* When we want to **change value** of any variable we don't need to use var keyword, but only name and new value
* Concatenation is done with _+_ sign
* Multiple assignment of value can be done by simply typing

   ```JavaScript

    var x, y;
    //Check Operators, Table of Precendece for Assignment Operator '='
    x = y = (3 + 5) / 2;

   ```

### Data types-Primitive

1. **Number** - floating point, decimals, integers
1. **String** - sequence of characters used for text
1. **Boolean** - true/false
1. **Undefined** - variable does _not have a value_ yet
1. **Null** - _non existant_

### Truthy and Falsy values

1. Falsy values - return false when evalueted in if/else conditions
   * **Undefined**
   * **Null**
   * **0** - avoid by adding condition that _variable === 0_ when true
   * **''**
   * **NaN**
1. Thruty values - return true when evalueted in if/else conditions
   * all **not falsy** values

### Operators

1. **Math** Operators - returns result
   * _+ - * /_
1. **Logical** Operators - returns true, false
   * <, >=, <=, >
1. **typeof** Operator - returns type of variable
1. [Table of precedence of operators][table_of_precedence]
1. **Assignment Operators** Short version for adding same variable _+-*/_ and _=_

   ```JavaScript
      x = x + 2;  ==> x += 2;
      x = x * 2;  ==> x *= 2;
      x = x / 2;  ==> x /= 2;
      x = x - 2;  ==> x -= 2;
   ```

1. **Increment** Operator _++_ or _--_

   ```JavaScript
      x = x + 1;  ==> x++;
      x = x - 1;  ==> x--;
   ```

1. **Boolean** logic
   * AND **& &** _true if all are true_
   * OR **||** _true if one is true_
   * NOT **!** _inverts true/false value_
1. Ternary operator used for making **if/else statements** in **one line**. Can be assigned to variable.

   ``` JavaScript
    condition ? //statement_if_is_true : //statement_if_is_false;
    var name = condition ? //statement_if_is_true : //statement_if_is_false;
   ```

1. **==** vs **===**
   * == is less strict, it transforms data type in order to make it true _23 == '23';_
   * === does data type comparison -> data type must be same in order to be true _23 !== '23';_

### Decision making if/elseif, switch

1. **If/elseif** has this structure:

  ```JavaScript
    if (condition1) {
      //statement1;
    } else if (condition2) {
      //statement2;
    } else if (condition3) {
      //statement3;
    } else {
      //statementN;
    }
  ```

1. **Switch** statements, if we work with _ranges_ we need to put _true_ instead of valiable

   ``` JavaScript
      switch (variable) {
        case expression1:
        case expression2:
          //statement1
          break;
        case expression3:
          //statement2
          break;
        default:
          //statement default
      }
   ```

### Functions

1. Declaring a function **statement**(they do actions- don't produce any immediate value):.

   ``` JavaScript
      function functionName(arg1, arg2){
        //what function does
        //return
      }
   ```

1. Calling the function

   ``` JavaScript
      functionName(arg1, arg2);
   ```

1. Declaring a function **expression** (anything that produces immediate result):

   ```JavaScript
      var functionName = function(arg1, arg2) {
        //what function does
        //return
      }
   ```

### Arrays

1. Two ways of **creating** an array

    ```JavaScript
      var arrName = [element1, element2];
      //or
      var arrName = new Array(element1, element2);
     ```

1. **Accessing** the array or its [elements]

    ```JavaScript
      arrName[index];
    ```

1. Usefull **array functions and methods**

   ```JavaScript
    //number of elements
      arrName.length;
    //add to end of array
      arrName.push(element);
    //or
      arrName[arrName.length] = element;
    //add to the begining of the array
      arrName.unshift(element);
    //remove element from the end of the array
      arrName.pop();
    //remove element from the begining of the array
      arrName.shift();
    //return the position of the argument that we pass inside array -> **returns -1** if there is no such element
      arrName.indexOf(element);
   ```

### Objects

1. Used for grouping variables which go together in _no particular order_

1. **Defining** object

   ``` JavaScript
    var objName = {
      keyString: 'value',
      keyNumber: 192,
      keyArray: [],
      keyObject: {
        keyOfInsideObject: 'value'
      }
      funct: function(Arg){
        return something;
      }
    }
    //or
    var jane = new Object();
    jane.name = 'Jane';
    jane.birthYear = 1992;
    jane[''lastaAme] = 'Austin';
   ```

1. **Defining** objects as function constructor, _always_ Capital Letter

   ``` JavaScript
    var Name = function(arguments){
      this.arg1 = arg1;
      this.arg2 = arg2;
    }
    //popunjavanje
    var objName = new Name(arg1, arg2);

    //dodavanje metoda na prototip
    Name.prototype.functionName = function () {
      //do anything
      };
    // dodavanje propertija na prototip --> Svi se prezivaju smith! Not common
    Name.prototype.lastName = 'Smith'
   ```

   * **new** creates new empty Object and **this** se odnosi na ono u novom praznom objektu
   * Da li ima SVOJ property **Name.hasOwnProperty()** ne vraca inherited
   * **name.instanceof Object** da li je instanca
   * **console.info(element)** vraca prototip sa svim metodima

1. **Object.create** metod

1. **Accessing** object and values and **editing** it by declaring it with =

   ``` JavaScript
    console.log(objName.objKey);
    //or -->without '' if it is a number
    console.log(objName.['objKey']);
    //or by declaring a variable with keyName
    var a = 'keyName';
    console.log(objName.[a]);
    //edit object
    objName.keyName = newValue;
    //access function
    objName.funct(Arg);
   ```

1. Usefull **objects methods**

   ``` JavaScript
      //this je trenutni objekat
      this.keyName;
      //example-> napravi ili edituj age key i daj mu vrednost 2018- godina rodjenja tog objekat
      this.age =  2018- this.birthYear;
   ```

### Loops

1. **For Loop**

   ``` JavaScript
    for(initialCounterValue = x; condition; counterUpdate){
      //what to do if all 3 conditions went well
    }
   ```

1. **While Loop**

   ``` JavaScript
    var counter = innitialValue;
    while(condition){
      //do while condition is true
      counterUpdate;
    }
   ```

1. **Continue and Break Statements**

   ``` JavaScript
    continue //-> kada se stavi pored if statementa za neki uslov,ako naidje na slucaj kada nije ispostovan uslov samo ce da nastavi dalje, nece nista raditi sa tim slucajem
    break //-> kada se stavi pored if statementa za neki uslov,ako naidje na slucaj kada nije ispostovan uslov sne nastavlja dalje nego prekida izvrsavanje
   ```

### Hoisting Scope and This

1. When we declare function we can use them even **before** they are declared in code because it is _hoisted_ in JS.

   ```JavaScript
    funcName(arg);
    function funcName(arg){
      //what it does
    }
   ```

1. When we try to use **variable** before its declaration in code it will be _undefined_, but it will exist. That is beacause on the execution start code scans all variables and sets them to undefined.

1. **Scoping** works from bottom to top. Not in _opposite direction_. Local definitions are never accessible to global ones if they are not returned from functions.

1. Where does **this** _point_
   * **regular function call** -> on global object
   * **method call** -> object that is calling the method, method is function inside an Object
   * **in function call** -> on global object -in case of browser -_Window_

[table_of_precedence]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#Table
