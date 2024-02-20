---
sidebar_position: 3
---

# Mocking APIs & HTTP Requests

Mocking APIs and HTTP requests is a crucial aspect of unit testing in applications that interact with external services. When you test a function or component that makes API calls, you don't want to hit the actual endpoints for several reasons: it can be slow, produce unpredictable results, and you might not have control over the external service's test environment. Instead, you can mock these API calls to simulate their behavior and responses, allowing you to test how your application handles various scenarios.

### Why Mock API Calls?

- **Isolation**: Testing should be isolated to the unit of code under test. By mocking API calls, you can isolate your tests from external dependencies.
- **Control**: Mocking allows you to control the API's responses, enabling you to test how your application handles different response scenarios, including success, error, and edge cases.
- **Speed**: Tests run significantly faster when they don't need to perform real network requests.
- **Stability**: Using mocks makes your tests more stable since you're not dependent on the availability and behavior of external services.

## How to Mock API Calls in Jest

Jest provides several ways to mock API calls. A common approach involves mocking the module used for making HTTP requests, such as `fetch`, `axios`, or any other HTTP client library.

#### Mocking with `jest.mock`

Suppose you have a function that fetches data from an API using `axios`:

```javascript
// dataFetcher.js
import axios from "axios";

export const fetchData = async () => {
  try {
    const response = await axios.get("https://api.example.com/data");
    return response.data;
  } catch (error) {
    throw error;
  }
};
```

To test this function without making real HTTP requests, you can mock `axios` using `jest.mock`:

```javascript
// dataFetcher.test.js
import axios from "axios";
import { fetchData } from "./dataFetcher";

// Mock the axios module
jest.mock("axios");

describe("fetchData", () => {
  it("fetches successfully data from an API", async () => {
    const data = "response data";

    // Configure axios mock to resolve with 'data' when called
    axios.get.mockResolvedValue({ data });

    await expect(fetchData()).resolves.toEqual(data);
  });

  it("fetches erroneously data from an API", async () => {
    const error = "error message";

    // Configure axios mock to reject with 'error' when called
    axios.get.mockRejectedValue(new Error(error));

    await expect(fetchData()).rejects.toThrow(error);
  });
});
```

In this example, `jest.mock('axios')` replaces all `axios` methods with mock functions. `mockResolvedValue` and `mockRejectedValue` are used to simulate successful and failed API requests, respectively.

## Advanced Mocking Techniques

#### Manual Mocks

For more complex scenarios or to mock custom behavior, you can use Jest's manual mocks by creating a mock file in a `__mocks__` directory adjacent to the node module you're mocking. For example, to mock `axios`, create a file at `__mocks__/axios.js` with your mock implementation.

#### Mocking Global Fetch

If you're using the Fetch API, you can mock it globally in your tests setup file:

```javascript
global.fetch = jest.fn(() =>
  Promise.resolve({
    json: () => Promise.resolve({ data: "mocked data" }),
  })
);
```

## Conclusion

Mocking APIs and HTTP requests in Jest allows you to write tests that are fast, reliable, and independent of external services. By simulating API responses, you can thoroughly test your application's handling of various data fetching scenarios. Whether you're using `jest.mock` for quick mocks or setting up manual mocks for complex cases, Jest provides the tools you need to mock HTTP requests effectively in your tests.
