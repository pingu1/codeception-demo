# Codeception

---

Codeception is a test/QA PHP framework built on top of PHPUnit.
By default, Codeception focuses on 3 major test strategies
+++
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

- tests
  - acceptance
    - feature 1
      - cest file 1
      - cest file 2
    - feature 2
  - output
  - support
  acceptance.suite.yml

---

### 3 different test formats for PHP files

- Test files: these are standard Unit test files
- Cept files: simple and sequential test execution
- Cest files: scenario driven approach with OOP design

---

### Cept files

```php
<?php
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
