# Playwright

## How to pass dynamic parameters to Test Fixtures

There are two ways to pass parameters to fixtures:
Example from https://github.com/microsoft/playwright/issues/7065 (url is the dynamic param)
```javascript
const { test: base } = require('@playwright/test');

const test = base.extend({
  url: 'default',
  testedPage: async ({ url }, use) => {
    console.log(url);
    await use();
  }
});

// The scope of use is file or describe
test.use({
  url: 'overridden',
});

test('test 1', async ({ testedPage }) => {
});
```
Second is via making testedPage a function:
```javascript
const { test: base } = require('@playwright/test');

const test = base.extend({
  testedPage: async ({}, use) => {
    await use(url => console.log(url));
  }
});

test('test 1', async ({ testedPage }) => {
  testedPage('url')
});
```
