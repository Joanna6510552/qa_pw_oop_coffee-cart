# Create a BasePage class for Coffee-Cart testing

## Description

In this task, you'll practice building the page classes hierarchy and applying the OOP principles.  

## Preparation

1. Open the forked repo in VSCode.
2. Create a new branch by running `git checkout -b task_solution`.
3. Run the installation commands:

    - `npm ci`
    - `npx playwright install`

## Task

1. Create a `BasePage.js` file under the folder `./src/pages/`.
2. Create a new class – `BasePage`.
3. Add a constructor to the created `BasePage` class: 
```javascript
  constructor(page) {
    this.page = page;
  }
```
4. Open the `CartPage.js` file.
5. Import the `BasePage` class into it.
6. Inherit `BasePage` from `CartPage`:
```javascript
export class CartPage extend BasePage {...}
``` 
7. Update the `CartPage` constructor method to initialize the parent class constructor:
* 7.1 Remove the line `this.page = page;` - this will now be handled by the `BasePage` class. 
* 7.2 Add `super(page);` as the first line method. This initializes the parent constructor.
8. Repeat steps 4-7 for the `MenuPage.js` class.
9. Run all the tests to make sure nothing is broken.
10. Move the `open()` method to the `BasePage` class:
* 10.1 Add the `_url` protected property to the `BasePage`:
```javascript
export class BasePage {
  _url;

  constructor(page) {...}
}
```
* 10.2 Add the public `url()` method to the `BasePage` class:
```javascript
  url() {
    if (this._url) {
      return this._url;
    } else {
      throw Error(`The property '_url' must be implemented`);
    }
  }
```
* 10.3 Add the `open()` method to the `BasePage` class:
```javascript
  async open() {
    await this.step(`Open page`, async () => {
      await this.page.goto(this.url());
    });
  }
```
* 10.4 Add the protected `_pageName()` method:
```javascript
  _pageName() {
    return this.constructor.name.replace('Page', '');
  }
```
* 10.5 Update the `open()` method to accept the page name parameter:
```javascript
... this.step(`Open ${this._pageName()} page`, ...)
```
11. Assign appropriate values to the `this._url = ` property in the constructors of the `MenuPage` and `CartPage` classes.
12. Remove the `open()` methods from both the `MenuPage` and `CartPage` classes.
13. Run all the tests to make sure nothing is broken.
14. Move the `reload()` method from the `MenuPage` and `CartPage` classes to the `BasePage` class. 
14. Move the `waitForLoading()` method from the `CartPage` class to the `BasePage` class. 
15. Run all the tests again to make sure nothing is broken.

## Task Reporting

1. Add and commit all your updates.
2. Push the code to the origin.
3. Create a PR for your changes.
4. Keep implementing suggestions from the code review until your PR is approved.
