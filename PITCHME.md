# Codeception

---

Codeception is a test/QA PHP framework built on top of PHPUnit.
By default, Codeception focuses on 3 major test strategies

- unit tests
- functional tests
- acceptance tests

---

### Unit tests

- scope: single PHP classes
- needs access to the code
- no additional tools required
- does not test user interactions
- blazing fast

---

### Functional tests

- scope: PHP Framework (routing, controllers ...)
- needs access to the code
- no additional tools required
- does not test user interactions
- very fast

---

### Acceptance tests

- scope: pages in browser
- does not require access to the code
- additional tools required (headless browser like Selenium or PhantomJS)
- simulate user interactions
- pretty slow

---

### Other possible test strategies

- API tests: to test RESTful APIs / WebServices
- Database tests: to verify DB behaviors (triggers, stored procedures ...)

---

### Working with Acceptance tests

- PhantomJS installed via composer
- Phantoman extension to start PhantomJS automatically
- MultiDB to connect to different databases

---

### Working with Acceptance tests

```
- tests
  - acceptance
    - feature 1
      - cest file 1
      - cest file 2
    - feature 2
  - output
  - support
  acceptance.suite.yml
```

---

### 3 different test formats for PHP files

- Test files: these are standard Unit test files
- Cept files: simple and sequential test execution
- Cest files: scenario driven approach with OOP design

---

### Cept files

```php
<?php
$I->amOnPage('/');
$I->fillField('#input-username', 'John Dough');
$I->click('Login');
$I->see("Welcome");
```

---

### Cest files

```php
<?php
class LoginCest
{
    function _before(AcceptanceTester $I)
    {
        $I->amOnPage('/');
    }

    function login(AcceptanceTester $I)
    {
        $I->fillField('#input-username', 'John Dough');
        $I->click('Login');
        $I->see("Welcome");
    }
}
```

---

### Running tests

```sh
./vendor/bin/codeception run acceptance
Acceptance Tests (1) -------------------------------
✔ LoginCest: Login
----------------------------------------------------

Time: 1 second, Memory: 21.00Mb

OK (1 test, 1 assertions)
```

---

### Running tests

- the `--steps` option prints on screen the steps taken by the test
- the `--debug` option prints in screen additional messages/variables added via the `codecept_debug()` function

---

### Writing tests

- Setup and teardown are performed in Cest files using `_before()` and `_after()`
- The DB configuration allows you to add/remove fake data via
```php
$I->amConnectedToDb('Client'); // see DB config in suite YML file
$I->haveInDb('table', ['data'], 'primary_key_name');
```

_NOTE_: The `haveInDb()` function accepts additional arguments, the 5th is used to automatically remove data from DB when test is done. If set to false, you will have to manually remove the data with `haveDeletedFromDb()`.

---

### Writing tests

The easiest way to write test is to use XPath of elements you want to test. The XPath is a way to parse the DOM as an XML document.
To get the XPath of an element
- use the Chrome extension "XPath Helper"
- open the Chrome inspector, select the element, right click and "Copy > Copy XPath"

---

### Jenkins integration

- produces a HTML report
- all failing tests will be reported in the report with the failing step
- for failing tests, screenshot of the browser are saved in the `output` folder

