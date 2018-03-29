# Session 01 Basics

## 1. The birth of JavaScript

- 1994, The **_Netscape_** is in urgent need of a web scripting language that **_allows browsers to interact with the web_**.
- In 1995, the Sun company renamed the **Oak** language as **_Java_** and officially launched it to the market.
  Sun has hyped up and promised that this language can be written in a **_Write Once Run Anywhere_**. It looks likely to become the master of the future.
- The situation at the time was that the entire management of the **_Netscape_** was a believer in the **_Java_** language, and **_Sun_** was fully involved in the decision of the web scripting language.

<br>

<p align="center">
    <img src="img/1.png"/><br>
    <b>Navigator Browser 1.0</b>
</p>

<br>

<p align="center">
    <img src="img/3.png"/><br>
    <b>Brendan Eich - Creator of JavaScript</b>
</p>

In general, the idea of **Brendan Eich**'s design is this:

1. Draw on the basic grammar of the **_C language_**;
2. Learn from the **data types** and **memory management** of **_Java language_**;
3. Using the **_Scheme_** language as reference ———— **_function_** is the "first class citizen";
4. Draw on the **_Self language_** and use the inheritance mechanism based on the prototype (prototype);

<br>

> "The influence of Java to JavaScript is to divide data into two basic types (**primitive**) and object types (**object**), such as **strings** and **string objects**, and introduce **_Y2K Problem_** . It's really unfortunate."

<br>

## 2. JavaScript & Java

<p align="center">
    <img src="img/7.png"/><br>
    <b>The relationship between JavaScript and Java</b>
</p>

<br>

Their similarities include:

1. Their syntaxs are both similar to **C language**;
2. They are both OOP language (Although in a slightly different way);
3. JavaScript refers to the Java naming rules in the design;


The differences include:

1. JavaScript: **Dynamiclly Typed**、**Weakly Typed**
2. Java: **Statically Typed**、**Strongly Typed**


- **Weakly Typed**:

python：

```javascript
> "1"+2
'12'
```

- **Strongly Typed**:

python：

```python
>>> 1+'1'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

- **Statically Typed**:

java：

```java
List<String> name = Arrays.asList("xxx", "yyy", "zzz");
int n = 10;
name.add(n); 
/* Error:(14, 21) java: no suitable method found for add(int)
    method java.util.Collection.add(java.lang.String) is not applicable
      (argument mismatch; int cannot be converted to java.lang.String)
    method java.util.List.add(java.lang.String) is not applicable
      (argument mismatch; int cannot be converted to java.lang.String) */
```

- **Dynamiclly Typed**

python：

```python
>>> a = 1
>>> type(a)
<type 'int'>
>>> a = "s"
>>> type(a)
<type 'str'>
```

node.js:

```js
> a = 1
1
> typeof a
'number'
> a = '1'
'1'
> typeof a
'string'
```

<br>

## 3. Working principle of browsers

There is a very classic topic in the front-end field called：["**What really happens when you navigate to a URL?**"](http://igoro.com/archive/what-really-happens-when-you-navigate-to-a-url/), of course, DNS lookup and how to build TCP/IP connections are not the focus of this session. the focus of this section is know how the browser render the page after getting the HTML page content:


<br>

<p align="center">
    <img src="img/5.png"/><br>
    <b>The basic flow of the rendering engine.</b>
</p>

<br>

So, how do HTML and CSS collaborate?

<p align="center">
    <img src="img/6.png"/><br>
    <b>CSSOM + DOM ===> Render Tree</b>
</p>

<br>
<br>


## 4. Basic concepts of JavaScript

### 4.1 Syntax

- Case sensitive
- Identifier
- Comments
- Strict mode ('use strict')

<br>

### 4.2 Type

- typeof
- Undefined
- Null
- Boolean
- Number
- String
- Object

Object type includes:

- Object
- Array
- Date
- RegExp
- Function

```js
var num = 1;
var isHoliday = false;
var name = 'BOLT';
var teams = ['Dragon Bolt', 'Great Wall'];
var sites = {
  ZA: 'Gumtree',
  MX: 'Vivanuncios'
};

teams[0] // 'Dragon Bolt'
teams[1] // 'Great Wall'

sites.ZA // 'Gumtree'
sites.MX // 'Vivanuncios'

luke // Uncaught ReferenceError: luke is not defined
sites.luke // undefined

typeof num        // 'num'
typeof name       // 'string'
typeof isHoliday  // 'boolean'
typeof teams      // 'object'
typeof sites      // 'object'
typeof null       // 'object'
typeof luke       // 'undefined'
```

<br>

### 4.3 Function & Scope

- **_Fragment 1_**

```js
 function foo(a) {
    var b = a * 2;

    function bar(c) {
      console.log(a, b, c)
    }

    bar(b * 3)
  }

  foo(2)
```

<details>
<summary>Check out the answer</summary>
2,4,12
</details>

<br>
<br>

- **_Fragment 2_**

```js
(function() {
   var a = b = 5;
})();
 
console.log(b); // 5
````

is equal to:

```js
(function() {
   'use strict';
   var a = window.b = 5;
})();
 
console.log(b);
```

<br>
<br>

- **_Fragment 3_**

```js
function test() {
   console.log(a);
   console.log(foo());
   
   var a = 1;
   function foo() {
      return 2;
   }
}
 
test();
```

<details>
<summary>Check out the answer</summary>
2
</details>

<br>
<br>

is equal to:

```js
function test() {
   var a;
   function foo() {
      return 2;
   }
 
   console.log(a);
   console.log(foo());
   
   a = 1;
}
 
test();
```

<br>
<br>


```js
function test() {
   console.log(a);
   console.log(foo());
   
   let a = 1;
   let foo = function() {
      return 2;
   }
}
 
test(); 
```

<details>
<summary>Check out the answer</summary>
// Uncaught ReferenceError: a is not defined
</details>

<br>
<br>



### 4.4 How does JavaScript interact with HTML

```js
var app = document.getElementById('app')
app.innerHTML = '<h1>BOLT</h1>'
```

Global APIs that can be used to interact with browsers：

- window
- document

### 4.5 Event Loop Introduction

<p align="center">
    <img src="img/8.png"/><br>
    <b>Event Loop</b>
</p>


```js
function printing() {
   console.log(1);
   setTimeout(function() { console.log(2); }, 1000);
   setTimeout(function() { console.log(3); }, 0);
   console.log(4);
}
printing();
```

<br>

## 5. Basic concepts of CSS

### 5.1 Basic unit

- px
- em
- rem
- vw
- vh
- %
- number

### 5.2 Selector

- ID Selector：`#id`
- Class Selector：`.class`
- Element Selector：`element`
- General Selector：`*`
- AttributeSelector ：
  - `[attr]`
  - `[attr=value]`
- Children Selector：
  - `>`：Direct child
  - ` `：General child
- sibling
  - `+`：Adjacent sibling
  - `~`：General sibling
- Pseudo classes：
  - `:active`
  - `:first-child`
  - `:last-child`
  - `:nth-child([even/odd/n])`
- Pseudo elements：
  - `::after`
  - `::before`
  - `::selection`

### 5.3 Basic style

- Styling text
  - Basic
    - font-size (px、em、rem)
    - font-style：`normal`/`italic`/ `oblique`
    - font-weight: `normal`/ `lighter` / `bolder` / `100-900`
    - text-transform: `none` / `uppercase` / `lowercase` / `capitalize` / `full-width`
    - text-decoration: `none` / `underline` / `overline` / `line-through`
    - text-shadow
    - text-align：`left` / `right` / `center` / `justify`
    - line-height
    - letter-spacing
  - List
    - list-style
  - Link
    - :link
    - :visited
    - :hover
    - :focus
    - :focus
    - :active
  - Font
    - font-family
    - @font-face

### 5.4 Display

- inline
- inline-block
- block

### 5.6 Layout

- float
- position


<br>
<br>
<br>

## Q & A










