

# Jasmine unit testing

**Jasmine** is one of the popular JavaScript unit testing frameworks which is capable of testing synchronous and asynchronous JavaScript code. It is used in BDD (Behavior-Driven Development) programming which focuses more on the business value than on the technical details.



## Jasmine Setup Configuration

First [download jasmine framework](https://github.com/jasmine/jasmine/releases) and extract it inside your project folder. I will suggest to create a separate folder `/jasmine` under `/js` or `/javascript` folder which may be already present in your application.

You will get below four folders/files in distribution bundle:

1. `/src` : contains the JavaScript source files that you want to test
2. `/lib` : contains the framework files
3. `/spec` : contains the JavaScript testing files
4. `SpecRunner.html` : is the test case runner HTML file

You may delete `/src` folder; and reference the source files from their current location inside `SpecRunner.html` file. The default file looks like below, and you will need to change the files included from `/src` and `/spec` folders.

```html
`<!DOCTYPE html>``<html>``<head>``    ``<meta charset=``"utf-8"``>``    ``<title>Jasmine Spec Runner v2.4.1</title>``    ` `    ``<link rel=``"shortcut icon"` `type=``"image/png"` `href=``"lib/jasmine-2.4.1/jasmine_favicon.png"``>``    ``<link rel=``"stylesheet"` `href=``"lib/jasmine-2.4.1/jasmine.css"``>``    ` `    ``<script src=``"lib/jasmine-2.4.1/jasmine.js"``></script>``    ``<script src=``"lib/jasmine-2.4.1/jasmine-html.js"``></script>``    ``<script src=``"lib/jasmine-2.4.1/boot.js"``></script>``    ` `    ``<!-- include source files here... -->``    ``<script src=``"src/Player.js"``></script>``    ``<script src=``"src/Song.js"``></script>``    ` `    ``<!-- include spec files here... -->``    ``<script src=``"spec/SpecHelper.js"``></script>``    ``<script src=``"spec/PlayerSpec.js"``></script>``</head>` `<body></body>``</html>`
```

In this demo, I have removed `/src` folder and will refer files from their current locations. The current folder structure is below:

![Jasmine Folder Structure](https://cdn1.howtodoinjava.com/wp-content/uploads/2016/07/Jasmine-Folder-Structure.png)Jasmine Folder Structure



## Jasmine Suite and Specs

In Jasmine, there are two important terms – **suite** and **spec**.

#### 1. Suite

A Jasmine suite is a group of test cases that can be used to test a specific behavior of the JavaScript code (a JavaScript object or function). This begins with a call to the Jasmine global function `describe` with two parameters – first parameter represents the title of the test suite and second parameter represents a function that implements the test suite.

```javascript
`//This is test suite``describe(``"Test Suite"``, ``function``() {``    ``//.....``});`
```

#### 2. Spec

A Jasmine spec represents a test case inside the test suite. This begins with a call to the Jasmine global function `it` with two parameters – first parameter represents the title of the spec and second parameter represents a function that implements the test case.

In practice, spec contains one or more expectations. Each expectation represents an assertion that can be either `true` or `false`. In order to pass the spec, all of the expectations inside the spec have to be `true`. If one or more expectations inside a spec is `false`, the spec fails.

```javascript
`//This is test suite``describe(``"Test Suite"``, ``function``() {``    ``it(``"test spec"``, ``function``() {``        ``expect( expression ).toEqual(``true``);``    ``});``});`
```

### It's Just Functions

Since `describe` and `it` blocks are functions, they can contain any executable code necessary to implement the test. JavaScript scoping rules apply, so variables declared in a `describe`are available to any `it` block inside the suite.



```javascript
// suite
describe("A suite is just a function", () => {
  let a;
 // spec
  it("and so is a spec", () => {
    a = true;
    expect(a).toBe(true);
  });
});
```

## Expectations

Expectations are built with the function `expect` which takes a value, called the actual. It is chained with a Matcher function, which takes the expected value.



```javascript
describe("A suite is just a function", () => {
  it("and so is a spec", () => {
 let a = true;
  // Expections
    expect(a).toBe(true);
  });
});
```

### Matchers

Each matcher implements a boolean comparison between the actual value and the expected value. It is responsible for reporting to Jasmine if the expectation is true or false. Jasmine will then pass or fail the spec.



```javascript
describe("The 'toBe' matcher compares with ===", () => {

    // positive Matcher
 it("and has a positive case", () => {
    expect(true).toBe(true);
  });
  
    // Negative matcher
  it("and can have a negative case", () => {
    expect(false).not.toBe(true);
   });
  });
```



Any matcher can evaluate to a negative assertion by chaining the call to `expect` with a `not`before calling the matcher.



Jasmine has a rich set of matchers included, you can find the full list in the [API docs](https://jasmine.github.io/api/edge/matchers.html) There is also the ability to write [custom matchers](https://jasmine.github.io/tutorials/custom_matcher.html) for when a project's domain calls for specific assertions that are not included in Jasmine.





Example:- 

To concentrate on what Jasmine is capable of, We have simple JS file `MathUtils.js`with some basic operations and we will unit-test these functions.

```javascript
`MathUtils = ``function``() {};` `MathUtils.prototype.sum = ``function``(number1, number2) {``        ``return` `number1 + number2;``}` `MathUtils.prototype.substract = ``function``(number1, number2) {``    ``return` `number1 - number2;``}` `MathUtils.prototype.multiply = ``function``(number1, number2) {``    ``return` `number1 * number2;``}` `MathUtils.prototype.divide = ``function``(number1, number2) {``    ``return` `number1 / number2;``}` `MathUtils.prototype.average = ``function``(number1, number2) {``    ``return` `(number1 + number2) / 2;``}` `MathUtils.prototype.factorial = ``function``(number) {``    ``if` `(number < 0) {``        ``throw` `new` `Error(``"There is no factorial for negative numbers"``);``    ``} ``else` `if` `(number == 1 || number == 0) {``        ``return` `1;``    ``} ``else` `{``        ``return` `number * ``this``.factorial(number - 1);``    ``}``}`
```

And after adding file reference in `SpecRunner.html`, file content will be :

```html
`<!DOCTYPE html>``<html>``<head>``    ``<meta charset=``"utf-8"``>``    ``<title>Jasmine Spec Runner v2.4.1</title>``    ` `    ``<link rel=``"shortcut icon"` `type=``"image/png"``        ``href=``"lib/jasmine-2.4.1/jasmine_favicon.png"``>``    ``<link rel=``"stylesheet"` `href=``"lib/jasmine-2.4.1/jasmine.css"``>``    ` `    ``<script src=``"lib/jasmine-2.4.1/jasmine.js"``></script>``    ``<script src=``"lib/jasmine-2.4.1/jasmine-html.js"``></script>``    ``<script src=``"lib/jasmine-2.4.1/boot.js"``></script>``    ` `    ``<!-- include source files here... -->``    ``<script src=``"../MathUtils.js"``></script>``    ` `    ``<!-- include spec files here... -->``    ``<script src=``"spec/MathUtils.js"``></script>``</head>` `<body></body>``</html>`
```



On opening the `SpecRunner.html` file in browser, specs are run and result is rendered in browser as shown below:

![Jasmine Output](https://cdn2.howtodoinjava.com/wp-content/uploads/2016/07/Jasmine-Output.png)



## 3. Setup and Teardown