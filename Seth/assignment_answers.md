# Assignment for technical support engineer
referrence file: https://drive.google.com/file/d/1QEyuOKCdrA83HkwzID9qcBvcSyCTN6d_/view?usp=sharing

## 1. Explain the use of the browser inspector and its tabs.  
The Browser inspecter also termed as Developer Tools is used to show the technical aspects of the current web page.  

**Elements Tab** - Show the HTML elements and DOM structure of the current web page. When clicking an element, a separate window that shows the CSS rules of the selected element.  
**Console Tab** - Shows the console terminal for Javascript. It shows the logs during JavaScript execution ( if it has logs), also shows the Javascript error. It can also execute JavaScript code and view objects that is being used.  
**Sources Tab** - shows the file structure and source files ( including Libraries) of the current web page.  
**Network Tab** - shows the network activity that is being used by the current webpage. Can be filtered by types of network calls ( example, AJAX, media reference, linked JS and CSS files, etc).
**Performance Tab** - use to record performance. Can simulate various devices' actual parameters.
**Application Tab** - shows the application data of the current webpage. Can view, update and delete information stored in Local Storage, Session Storage and Cookies.

## 2. How do you troubleshoot if a javascript code conflicts with another javascript code where both scripts load dynamically? Explain the process in your words.
It actually depends on the situation, but one possiblity of this conflict is when loading javascript code that is dependent to the other. In this case, I would make sure that the required javascript code is properly loaded then dynamically load the other script. This can be done via script element's `onload` event or if the first script has a callback function when loaded (e.g, jQuery);

## 3. Is there a way to match exact words (not as a substring) in Shopify liquid without using for loop? Please write down the code if you know any.
```liquid
{% if string == searchString %}
    <p>string and searchString are exact match</p>
{% else %}
    <p>string and searchString are not exact match</p>
{% endif %}
```
## 4. What's the difference between the below liquid keywords:
1. Where, Contains, Map

   **Where** is used to filter an array of objects which contains specific property and value. Returns the filtered array.
   **Contains** is used to check whether a certain value is one if the elements in an array. **Contains** can also be used to check whether a value is a subtring of a string.
   **Map** is used to restructure an array of objects based on a given property into an array of values of each of the objects in the array.

2. Include and Render

    **Render** can take parameters that can make a dynamic content. **Include** only display static content.

## 5. What is the use of the “For...else” loop in liquid?
`For...else` is use when you want to return a default output if the array or iterable object has a possibility of unable to loop because of either array is empty or null.

## 6. How should I increment or decrement a variable using liquid?
Using the filter `plus` and assign the result to the same variable.  
Example:
```
// increment by 1
{% assign variable = 0 %}
{% assign variable = variable | plus: 1 %}

// variable = 1
```

## 7. Reverse the given string word by word using javascript: `Welcome to wholesale helper`
```javascript
function reverseString(str){
    const reversed = str.split(" ").reduce(function(result,word) {
        return `${word} ${result}`;
    },"").trim();

    return reversed;
}

reverseString("Welcome to wholesale helper") // 'helper wholesale to Welcome'
```

## 8. What is the difference between null & undefined?
 `null` the object or variable exists but holds no value. `undefined` is when an object or variable does not exist.

 ## 9. Write a javascript that returns true if strings are anagrams of one another. For example, “mary” and “army”.
 ```javascript
function isAnagram(str1, str2){
    // check if the same length
    if ( str1.length !== str2.length ) return false;

    //sort both strings and compare
    return str1.split("").sort().join("") === str2.split("").sort().join("");

}
// actual anagram
isAnagram("mary","army"); // true
isAnagram("phil","hill"); //false
isAnagram("mary","maryy"); //false
 ```

 ## 10. Write down an HTML/CSS code to display an element in the center of the page. Vertically/horizontally.

 ```css
element {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
 ```

 ## 11. What do you prefer to set value, in px/em/rem and why?
 I prefer using `rem` units because of it's flexibility across different types of browsers in various devices.

 ## 12. Using javascript, How to bind an event on a dynamically added element?
 Using Event Delegation. Attaching the event to the `document` and checking if the target element is triggering it.
 ```javascript
 //vanilla
 document.addEventListener("click", function(e){
    if( e.target.closest("#targetElement")){
        // Do something
    }
 });

 //jQuery
 $(document).on("click", "#targetElement", function(e){
    //do something
 });
 ```

 ## 13. Explain passing a variable by value and reference with example codes.
 Passing a variable when calling a function **by value** is that it uses the variables value to process and it returns new value. does not modify the values of the given variable.
 ```javascript
function add(num1, num2){
    return num1 + num2;
}
var a = 1;
var b = 2;

var c = add(a,b);

console.log(a) // 1
console.log(b) // 2
console.log(c) // 3
 ```

 Passing a variable when calling a function **by reference** is that it modifies the value of the given variable after the process. The function does not return any new values;

 ```javascript
function increment(number){
    number = number + 1;
}

var num = 1;
// before function call
console.log(num); // 1

increment(num);

//after function call
console.log(num); // 2
 ```

 ## 14. List out technical differences and limitations between a draft order and a regular order in Shopify.
- Draft orders are manually created in the Shopify Admin. When accepts payment, it will change to a regular order.
- Draft orders can use custom products with custom prices and can also edit products prices.
- Draft orders won't show up on customer's Order history page.
- Regular orders cannot be set as Draft Orders.

## 15.What is the use of a meta field in Shopify? List out different types of meta fields in Shopify and how to use them in the liquid code.
Metafields are use for additional information to be processed by an application or to be displayed in the frontend of a certain Product, Collection, Order, Blog, Article, Customer and Shop.  

There are 3 basic types of metafield, `string`, `integer` and `json_string`. Shopify has expanded it into more types like `date`, `boolean`, `color`, `money` etc., These added types still revolves around the 3 main types.

```
// single_line_text_field
{{ product.metafields.namespace.key }}

// json
// {
//    material: "fiber",
//    length: "25",
//    unit: "cm"
//  }

Length: {{ product.metafields.namespace.key.value["length"]}}{{ product.metafields.namespace.key.value["unit"]}}
Material: {{ product.metafields.namespace.key.value["material"]}}

{% for property in product.metafields.namespace.key.value %}
    {{ property.first }}: {{ property.last }}
{% endfor %}

```

outputs:
```
// single_line_text_field
Don't iron on print

//json
Length: 25cm
Matierial: fiber

material: fiber
length: 25
unit: cm
```

## 16.Are you familiar with the Shopify Ajax API? If yes, please write down an example code to inject an attribute to a line item of the cart.

```javascript
function addMessage(itemId, message){
    const params = {
        'id': itemId,
        'properties':{
            'message': message
        }
    }

    return fetch("/cart/change.js", {
        method: "POST",
        headers: {
            "Content-Type":"application/json"
        },
        body: JSON.stringify(params)
    });
}

const cart = getCartState(); //query cart

addMessage(cart.items[0].variant_id, "Hello World").then( request => request.json())
.then( data => {
    //update cartState
    setCartState(data);
    
    //update display
})
/*
items:
    0: {
        ...
        properties: {
            message: "Hello World"
        }
        ...
    }

*/
```