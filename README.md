# Frontend style guide

## General
* Comment, at least, such parts of the code, that are hardly understandable;
* never use transliteration. Always use English words
* do not use inline styles and scripts right inside the html. There are really a few cases when it's necessary;
* include scripts before closing body tag;
* use only spaces (2 or 4) not tabs to shift code;
* write the code as tree-like structure;
* give to classes and variables logical and understandable names.

## HTML/Smarty
* use "===" instead of "==";
* use whitespace between operators in Smarty;
* every element or smarty expression must begin with a new line;
* prevent using an empty line for separating html;
* use double quotes inside attributes;
* attributes order must be the following: [xmlns, id, class, width, height, viewBox, fill, src, href, type, name, value, maxlength, checked, selected, readonly, disabled, other attributes, data-attributes, custom attributes];
* always close tags event if it is self-closing element;

## CSS
* Follow a cetrain order of properties in your stylesheets. For example, block model properties (display, margin, width), positioning properties (position, top, left), font properties (font-family, font-size), etc. So the idea is not to mix properties that are not related to each other.
* every pair of property-value must begin with a new line;
```css
// Wrong (all on one line)
.selector {font-size: 1rem; position: relative; text-align: center;}

// Wrong (no logic order)
.selector {
    font-size: 1rem;
    position: relative;
    text-align: center;
    font-weight: bold;
}

// Right
.selector {
position: relative;
    font-size: 1rem;
    font-weight: bold;
    text-align: center;
}
```
* group properties by their similarity. This means that if you have, for example, text properties and font properties, group them. Don't separate them by positioning or floating or something else, because they are really similar to each other;
```css
// Wrong (text-align comes after margin)
.selector {
    font-family: Arial;
    font-size: 1rem;
    margin: 0;
    text-align: right;
}

// Right (text-align comes after font properties - this is more logic than the wrong example)
.selector {
    margin: 0;
    font-family: Arial;
    font-size: 1rem;
    text-align: right;
}
```
* use 1 space after colon;
* always use semicolon after the last pair of property-value;
* use "border-box" model by every element;
* form element must be inline;
* by default, separate classname by "-" (this does not concern BEM).

## BEM with mutations
Use BEM with mutations. What does it mean? For css use block-element-modifier conception but with some changes, which are convenient for online-stores.
The first change is that we have `grid classes` such as "container", "row", "col-", etc.
The secong change is that we have `routine classes` that are constant through all of the media queries. These classes describe some common and constant behavior. For example, .text-center class centers text and this behavior is unchangeble. You cannot overwrite such a rule by custom selector or change it on a certain media query, because it breaks the idea of `routine classes`.
`Grid classes` and `routine classes` don't influence on a BEM flow in HTML. This means that you can use these classes everywhere.

## Javascript
* Don't use global variables, except for such cases as plugin, library, framework or third-party API that makes impossible using local variables;
* use "use strict" directive everywhere it is possible;
* use single quotes instead of double quotes;
* always use "===" instead of "==";
* constants must look like "CONST_NAME";
* declare variables at the top of a function (bacause of variable hoisting) and separate them by comma;
```javascript
// Wrong
function func () {
    var name = 'name';

    if (/*condition*/) {
        var age = 0;
    }
}

// Wrong
function func () {
    var name = 'name';
    var age;

    if (/*condition*/) {
        age = 0;
    }
}

// Right
function func () {
    var name = 'name',
        age;

    if (/*condition*/) {
        age = 0;
    }
}
```
* use camelCase notation for variables names;
* prefer "function declaration" over "function expression";
* functions constructors must begin with a capital letter;
* prefer "forEach" over "for" loop;
* use literal for creating new arrays or objects instead of using constructors;
```javascript
// Wrong
var arr = new Array();
var obj = new Object();

// Right
var arr = [],
    obj = {};
```
* save a value into a variable if you use it more than once;
* every function have to do only what it is supposed to do. This means, if a function gets the given element height, it doesn't have to it's background color. If a function opens a modal window, it doesn't have to validate form inside the window. How you name a function so it works, no more no less;

## jQuery
* use event delegation pattern for adding event listeners. The closer parent element, the faster event occurs. Because by default almost every event bubbles from the most nested element to the document;
```javascript
// Wrong
$('.selector').click(function () {
    // some code here
});

// Right
$('body').on('click', '.selector', function () {
    // some code here
});

// Right
$('.container-that-contains-selector').on('click', '.selector', function () {
    // some code here
});
```
* use "done", "fail", "always", "then" methods instead of "success", "error", "complete";
* it's really cool to remove inline styles after jQuery method have finished it's work, because this makes us ease to style element by css.

## Recomendations
### Stylesheet
* Use SASS preprocessor and Autoprefixer plugin because this simplifies writing styles and makes possible to separate styles;

### Javascript
* Using Requirejs library makes possible to load all scripts asynchronously, write modular encapsulated code with dependencies and makes us ease to include scripts only needed by a certain page.

### Other
* It's excellent if you use Gulp or Grunt and npm packages, because it accelerates developing, makes developing automatic and solves a lot of common tasks.
