# Overview

Jest really is the "delightful JavaScript Testing Framework with a focus on simplicity", its creators have described it to be! As a result, teams should leverage as many of the defaults as possible and only divert when necessary.

## Test Fixture File Names and Locations
It is important to be consistent with how test fixtures are named and where they are located. This helps developers quickly locate the code they are trying to use.

All test fixture names should follow this convention `[file].test.js`. Where the [file] is the name of the file which is being tested. Additionally, all test fixtures should be named with `.test.` preceding the file extension. The file extension should match the file extension used by the related file.

**Examples**

```
// Good Examples
ChildComponent.tsx
ChildComponent.test.tsx

store.js
store.test.js

// Bad Examples

// does not use .test.* convention
ChildComponent.tsx
ChildComponentTest.tsx

// file extensions don't match
request.ts
request.test.js
```

All test fixtures should be located in a `__tests__` directory adjacent to their corresponding implementation file.

**Examples**

```
// Good Example
- App
  - /__tests__
    - App.test.jsx
  - App.jsx
  - /components
    - /__tests__
      - component1.test.js
      - component2.test.ts
    - component1.js
    - component2.ts

// Bad Example - component tests are within the App root's __tests__ directory
- App
  - /__tests__
    - App.test.jsx
    - component1.test.js
    - component2.test.ts
  - App.jsx
  - /components
    - component1.js
    - component2.ts
```

## Naming Conventions within Test Fixtures

Good, consistent, conventions within a test fixture are also force multipliers. They help developers read, write, and debug tests more quickly.

[Roy Osherove](https://osherove.com/blog/2005/4/3/naming-standards-for-unit-tests.html) provides fantastic insights into using the following naming convention for all unit test: `UnitOfWork_StateUnderTest_ExpectedBehavior`. This convention works very well for C# and NUnit, and related languages and testing frameworks. One downside to this convention is that descriptive test names can become very long, oftentimes difficult to read.

Luckily, Jest's `describe` and `it` functions allow us to use Roy's concept but place each portion of the naming convention on its own line. The result is test blocks which are very easy to read and reason about! I recommend all unit tests use the following convention. While there is some level of nesting, the code is very easy to reason about and provides excellent reports from Jest when test cases fail.

**Example**

```javascript
// should match the name of the file, minus .test.ext
describe("testFixture", () => {
  // most often this will be the name of the function being tested
  describe("unitOfWork", () => {
    // Describes the state of the input values.
    // Each valid test case for unit of work should have its own
    // corresponding pair of `describe` and `it` methods.
    describe("stateUnderTest", () => {
      // describes the expected result
      it("expectedResult", () => {
        // Test Code here
      });
    });
  });
});
```

Consider the following very simple real-world example...

**util.js**

```javascript
export function add(number1, number2) {
  returns number1 + (number2 ?? 0);
}

export function add(number1, number2) {
  returns number1 - number2;
}
```

**util.test.js**

```javascript
import { add, subtract } from "../util";

describe("util", () => {
  describe("add", () => {
    // Test case #1
    describe("given 1 and 2", () => {
      it("returns 3", () => {
        expect(add(1, 2)).toBe(3);
      });
    });

    // Test case #2
    describe("given 1 and null", () => {
      it("returns 1", () => {
        expect(add(1, null)).toBe(4);
      });
    });
  });

  describe("subtract", () => {
    describe("given 3 and 1", () => {
      it("returns 2", () => {
        expect(subtract(3, 1)).toBe(2);
      });
    });
  });
});
```

**Bad Examples for util.js**

```javascript
import { add, subtract } from "../util";

// does not include the test fixture name
describe("add", () => {
  // Test case #1
  describe("given 1 and 2", () => {
    it("returns 3", () => {
      expect(add(1, 2)).toBe(3);
    });
  });
});

// does not include ystem under test
describe("util", () => {

    // Hard to identify what exactly is being tested
    describe("given 1 and 2", () => {
      it("returns 3", () => {
        expect(add(1, 2)).toBe(3);
      });
    });

    describe("given 1 and null", () => {
      it("returns 1", () => {
        expect(add(1, null)).toBe(4);
      });

    describe("given 3 and 1", () => {
      it("returns 2", () => {
        expect(subtract(3, 1)).toBe(2);
      });
    });
});
```

[Roy Osherove naming standards for unit tests](https://osherove.com/blog/2005/4/3/naming-standards-for-unit-tests.html)

## Arrange, Act, Assert

Test methods should use this pattern to help structure unit tests consistently. The pattern will help readers easily consume the details of the test because the general structure is familiar. This pattern calls for each test to be split into three sections.

Arrange is the first section. It is commonplace for a single test to require multiple statements to initialize the necessary data. This section is where all of the necessary data initialization happens.

Act is the second section. Every test should be testing a single method or function. The method under test should be invoked in the Act section.

Assert is the final section. Every test method must have at least one Assert statement to be considered a true unit test. Assertions should be written at the end of every test to ensure all of the necessary options have been performed.

The use of Arrange, Act, Assert comments between sections is strongly encouraged.

Assertions mixed throughout a test are code smells. It indicates the system under test is likely written in a way the violates the SOLID principles of OOP or needs to be simplified to reduce complexity.

**Examples**

```javascript
// Good example
describe("util", () => {
  describe("add", () => {
    describe("given 1 and 2", () => {
      it("returns 3", () => {
        //Arrange
        const val1 = 1;
        const val2 = 2;

        // Act
        const result = add(1, 2);

        // Assert
        expect(result).toBe(3);
      });
    });
  });
});

// Bad Example - in more complicated tests,
// it may be hard to tell what code is "setup"
// vs what code is really being tested
describe("util", () => {
  describe("add", () => {
    describe("given 1 and 2", () => {
      it("returns 3", () => {
        //Arrange
        const val1 = 1;
        const val2 = 2;
        const result = add(1, 2);
        expect(result).toBe(3);
      });
    });
  });
});
```

## Testing React Components

In some cases, it is not necessary to include a `describe('unitOfWork')` block because the file name matches the name of the only exported function. In these cases, it's preferred to NOT duplicate the name.

**Examples**

```javascript
// MyComponent.jsx

export function MyComponent(number) {
  return <div>number</div>;
}
```

```javascript
// MyComponent.test.jsx
// Good Example
describe("MyComponent", () => {
  describe("given a number", () => {
    it("renders the number", () => {
      // Test Code here
    });
  });
});

// Bad Example - Unnecessary duplication of information
describe("MyComponent", () => {
  describe("MyComponent", () => {
    // This is totally unnecessary
    describe("given a number", () => {
      it("renders the number", () => {
        // Test Code here
      });
    });
  });
});
```

### Using Testing Library

We use React to build user interfaces. As a result, we should try our best to test our React applications as user interfaces! [@testing-library](https://testing-library.com/) will help us do that.

> The @testing-library family of packages helps you test UI components in a user-centric way.
>
> - https://testing-library.com/docs/

**Read the following resources about testing-library**

- [Guiding Principles](https://testing-library.com/docs/guiding-principles/)
- https://twitter.com/kentcdodds/status/977018512689455106
- [Common mistakes with React Testing Library](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library)

#### Prefer `getByRole`, `getByLabelText`... AVOID `.getByTestId`

Accessibility on the web is a thing. Testing Library can help us test the application in a way that is more inclusive of others' accessibility needs. Testing Library will help developers write UI's that can be effectively used by more people!

Learn about all of [Testing Libraries queries](https://testing-library.com/docs/queries/about).
Then learn the [order of priority](https://testing-library.com/docs/queries/about/#priority) so that you test in the most accessible way!

By making our software accessible, we become [force multiplers](https://ardalis.com/becoming-a-developer-team-force-multiplier/) by making our users more productive!

**Examples**

```javascript
// MyComponent.jsx
export function MyComponent() {
  return <Button data-test-name="my-button">Click Me!</Button>;
}

// MyComponent.test.jsx
describe("MyComponent", () => {
  // Good Example
  describe("when 'Click Me!' is pressed", () => {
    it("does something", () => {
      // Arrange & Act
      render(<MyComponent />);

      // Act
      const button = screen.getByRole("button", { name: "Click Me!" });
      fireEvent.click(button);

      //Assert
      // some assertion code
    });
  });

  // Bad Example - uses `getByTestid`
  describe("when 'Click Me!' is pressed", () => {
    it("does something", () => {
      // Arrange & Act
      render(<MyComponent />);

      // Act
      const button = screen.getByTestId("my-button");
      fireEvent.click(button);

      //Assert
      // some assertion code
    });
  });
});
```
