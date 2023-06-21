# Jest templates

Useful boilerplate for testing various types of class with Jest.

Make sure Jest is installed first: `npm install jest`.

## Testing a view class

Install [jest-environment-jsdom](https://www.npmjs.com/package/jest-environment-jsdom): `npm install jest-environment-jsdom`

```javascript
/**
 * @jest-environment jsdom
 */
 // This JSDoc comment tells Jest our code is designed to run it a browser, 
 // although we're running the tests in Node.

// The built-in Node fs module lets is read non-JS files
const fs = require('fs');
const View = require('./view');

describe('A test for my web page', () => {
    
  // We can use the beforeEach() hook 
  // to set the jest `document` HTML before each test
  // Jest mocks the HTML content internally
  beforeEach(() => {
    document.body.innerHTML = fs.readFileSync('./index.html');
  });

  it('displays a title', () => {
    // 1. Arrange - instantiate our View class
    const view = new View();

    // 2. Act - call any method that modifies the page
    // this method `displayTitle` would dynamically
    // set a <h1> title on the page with the given content
    view.displayTitle('My amazing website');

    // 3. Assert - we assert the page contains what it should.
    // Usually, you will use `.querySelector` (and friends)
    // here, and assert the text content, the number of elements,
    // or other things that make sense for your test.
    expect(document.querySelectorAll('h1').textContent).toBe('My amazing website');
  });
});
```

## Testing a client class

Install [jest-fetch-mock](https://www.npmjs.com/package/jest-fetch-mock): `npm install jest-fetch-mock`

```javascript
const Client = require('./client');

// This makes `fetch` available to our test
// (it is not by default, as normally `fetch` is only
// available within the browser)
require('jest-fetch-mock').enableMocks()

describe('Client class', () => {
  it('calls fetch and loads data', (done) => {
    // 1. Instantiate the class
    const client = new Client();

    // 2. We mock the response from `fetch`
    // The mocked result will depend on what your API
    // normally returns — you want your mocked response
    // to "look like" as the real response as closely as
    // possible (it should have the same fields).
    fetch.mockResponseOnce(JSON.stringify({
      name: "Some value",
      id: 123
    }));

    // 3. We call the method, giving a callback function.
    // When the HTTP response is received, the callback will be called.
    // We then use `expect` to assert the data from the server contain
    // what it should.
    client.loadData((returnedDataFromApi) => {
      expect(returnedDataFromApi.name).toBe("Some value");
      expect(returnedDataFromApi.id).toBe(123);

      // 4. Tell Jest our test can now end.
      done();
    });
  });
});
```
