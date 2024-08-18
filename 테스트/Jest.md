# Jest

Jest는 메타에서 만들어 배포하는 자바스크립트 테스팅 프레임워크입니다. 많은 자바스크립트 커뮤니티의 라이브러리와 프레임워크가 Jest를 테스팅 라이브러리로 채용하고 있습니다.

- [React](https://ko.react.dev/blog/2022/03/29/react-v18#react-dom-test-utils)
- [Next.js](https://nextjs.org/docs/app/building-your-application/testing)
- [NestJS](https://docs.nestjs.com/fundamentals/testing)
- [Angular](https://angular.dev/roadmap#improve-tooling)

## Jest의 특징

Jest는 **프레임워크**인 만큼 기존의 자바스크립트 테스팅 라이브러리(Mocha, Chai, Jasmine)과 달리 Jest만을 통해 Test Runner, Matcher, Mock 전부 사용할 수 있습니다.

## describe()

describe는 여러 관련 테스트를 함께 그룹화하는 블록을 생성합니다.

```tsx
describe("Basic arithmetic operations", () => {
  it("addition", () => {
    expect(1 + 1).toBe(2);
  });

  it("subtraction", () => {
    expect(2 - 1).toBe(1);
  });

  it("multiplication", () => {
    expect(2 * 3).toBe(6);
  });

  it("division", () => {
    expect(6 / 2).toBe(3);
  });
});
```

## **test()**

`it()` 별칭으로도 사용가능합니다.

첫 번째 인수는 테스트 이름이고, 두 번째 인수는 테스트할 기대값을 포함하는 함수입니다. 세 번째 인수(선택 사항)는 중단하기 전에 대기할 시간을 지정하기 위한 시간 제한(밀리초)입니다. 기본 시간 제한은 5초입니다.

```tsx
test("division", () => {
  expect(6 / 2).toBe(3);
});
```

## Matchers

### [Common Matchers](https://jestjs.io/docs/using-matchers#common-matchers)

값을 테스트하는 가장 간단한 방법은 정확한 동일성을 사용하는 것입니다.

```tsx
test("two plus two is four", () => {
  expect(2 + 2).toBe(4);
});
```

이 코드에서 expect(2 + 2)는 `기대(expectation)` 객체를 반환합니다. 일반적으로 이러한 기대 객체에서는 `일치자(toBe)` 를 호출하는 것 외에는 많은 작업을 수행하지 않습니다. 이 코드에서는 `.toBe(4)`가 `매처`입니다. Jest가 실행되면 실패한 모든 일치자를 추적하여 멋진 오류 메시지를 출력할 수 있습니다.

`toBe`는 `Object.is`를 사용하여 정확한 동일성을 테스트합니다. 객체의 값을 확인하려면 toEqual을 사용합니다.

```tsx
test("object assignment", () => {
  const data = { one: 1 };
  data["two"] = 2;
  expect(data).toEqual({ one: 1, two: 2 });
});
```

`toEqual`는 객체 또는 배열의 모든 필드를 재귀적으로 확인합니다.

`toEqual` 는 정의되지 않은 프로퍼티, 정의되지 않은 배열 항목, 배열 희소성 또는 객체 유형 불일치가 있는 객체 키를 무시합니다. 이러한 사항을 고려하려면 대신 `toStrictEqual`을 사용하십시오.

`not`을 사용하여 일치하는 항목의 반대를 테스트할 수도 있습니다.

```tsx
test("adding positive numbers is not zero", () => {
  for (let a = 1; a < 10; a++) {
    for (let b = 1; b < 10; b++) {
      expect(a + b).not.toBe(0);
    }
  }
});
```

### [**Truthiness**](https://jestjs.io/docs/using-matchers#truthiness)

테스트에서 `undefined`, `null`, `false`를 구분해야 할 때도 있지만, 이들을 다르게 처리하고 싶지 않을 때도 있습니다. Jest에는 원하는 것을 명시적으로 표현할 수 있는 헬퍼가 포함되어 있습니다.

- `toBeNull`은 널만 일치합니다
- `toBeUndefined`는 정의되지 않은 것만 일치합니다
- `toBeDefined`는 `toBeUndefined`의 반대입니다
- `toBeTruthy`는 `if` 문이 참으로 취급하는 모든 것을 일치시킵니다
- `toBeFalsy`는 `if` 문이 거짓으로 취급하는 모든 것을 일치시킵니다.

```tsx
test("null", () => {
  const n = null;
  expect(n).toBeNull();
  expect(n).toBeDefined();
  expect(n).not.toBeUndefined();
  expect(n).not.toBeTruthy();
  expect(n).toBeFalsy();
});

test("zero", () => {
  const z = 0;
  expect(z).not.toBeNull();
  expect(z).toBeDefined();
  expect(z).not.toBeUndefined();
  expect(z).not.toBeTruthy();
  expect(z).toBeFalsy();
});
```

### [Numbers](https://jestjs.io/docs/using-matchers#numbers)

숫자를 비교하는 대부분의 방법이 jest에 존재합니다.

```tsx
test("two plus two", () => {
  const value = 2 + 2;
  expect(value).toBeGreaterThan(3);
  expect(value).toBeGreaterThanOrEqual(3.5);
  expect(value).toBeLessThan(5);
  expect(value).toBeLessThanOrEqual(4.5);

  // toBe and toEqual are equivalent for numbers
  expect(value).toBe(4);
  expect(value).toEqual(4);
});
```

부동 소수점 같음의 경우 테스트가 작은 반올림 오류에 의존하는 것을 원하지 않으므로 `toEqual` 대신 `toBeCloseTo`를 사용합니다.

```tsx
test("adding floating point numbers", () => {
  const value = 0.1 + 0.2;
  //expect(value).toBe(0.3);         반올림 오류로 인해 작동하지 않습니다.
  expect(value).toBeCloseTo(0.3); // 작동합니다.
});
```

### [Strings](https://jestjs.io/docs/using-matchers#strings)

`toMatch`를 사용하여 문자열을 정규식으로 검증합니다.

```tsx
test("there is no I in team", () => {
  expect("team").not.toMatch(/I/);
});

test('but there is a "stop" in Christoph', () => {
  expect("Christoph").toMatch(/stop/);
});
```

### [Arrays and iterables](https://jestjs.io/docs/using-matchers#arrays-and-iterables)

배열이나 이터러블에 특정 항목이 포함되어 있는지 여부는 `toContain`을 사용하여 확인할 수 있습니다.

```tsx
const shoppingList = ["diapers", "kleenex", "trash bags", "paper towels", "milk"];

test("the shopping list has milk on it", () => {
  expect(shoppingList).toContain("milk");
  expect(new Set(shoppingList)).toContain("milk");
});
```

### [Exceptions](https://jestjs.io/docs/using-matchers#exceptions)

특정 함수가 호출될 때 에러가 발생하는지 테스트하려면 `toThrow`를 사용하세요.

```tsx
function compileAndroidCode() {
  throw new Error("you are using the wrong JDK!");
}

test("compiling android goes as expected", () => {
  expect(() => compileAndroidCode()).toThrow();
  expect(() => compileAndroidCode()).toThrow(Error);

  // You can also use a string that must be contained in the error message or a regexp
  expect(() => compileAndroidCode()).toThrow("you are using the wrong JDK");
  expect(() => compileAndroidCode()).toThrow(/JDK/);

  // Or you can match an exact error message using a regexp like below
  expect(() => compileAndroidCode()).toThrow(/^you are using the wrong JDK$/); // Test fails
  expect(() => compileAndroidCode()).toThrow(/^you are using the wrong JDK!$/); // Test pass
});
```

> 예외를 던지는 함수는 래핑 함수 내에서 호출되어야 하며, 그렇지 않으면 `toThrow` 어설션이 실패합니다.

## # Setup and Teardown

테스트를 작성하는 동안 테스트 실행 전에 수행해야 하는 설정 작업과 테스트 실행 후에 수행해야 하는 마무리 작업이 있는 경우가 종종 있습니다. Jest는 이를 처리하기 위한 헬퍼 함수를 제공합니다.

### [Repeating Setup](https://jestjs.io/docs/setup-teardown#repeating-setup "Direct link to Repeating Setup")

여러 테스트에서 반복적으로 수행해야 하는 작업이 있는 경우 `beforeEach` 및 `afterEach` 훅을 사용할 수 있습니다. 예를 들어 여러 테스트가 도시 데이터베이스와 상호 작용한다고 가정해 보겠습니다. 각 테스트 전에 호출해야 하는 초기화 `CityDatabase()` 메서드가 있고, 각 테스트 후에 호출해야 하는 `clearCityDatabase()` 메서드가 있습니다. 이 작업을 수행할 수 있습니다:

```ts
beforeEach(() => {
  initializeCityDatabase();
});

afterEach(() => {
  clearCityDatabase();
});

test("city database has Vienna", () => {
  expect(isCity("Vienna")).toBeTruthy();
});

test("city database has San Juan", () => {
  expect(isCity("San Juan")).toBeTruthy();
});
```

`beforeEach`와 `afterEach`는 [테스트가 비동기 코드를 처리하는 것](https://jestjs.io/docs/asynchronous)과 같은 방식으로 비동기 코드를 처리할 수 있으며, 완료된 매개변수를 받거나 프로미스를 반환할 수 있습니다. 예를 들어,`initializeCityDatabase()`가 데이터베이스가 초기화될 때 해결된 프로미스를 반환하는 경우 해당 프로미스를 반환하고 싶을 것입니다:

```ts
beforeEach(() => {
  return initializeCityDatabase();
});
```

### [One-Time Setup](https://jestjs.io/docs/setup-teardown#one-time-setup "Direct link to One-Time Setup")

어떤 경우에는 파일을 시작할 때 한 번만 설정하면 됩니다. 이는 특히 설정이 비동기식이어서 인라인으로 수행할 수 없는 경우 번거로울 수 있습니다. Jest는 이러한 상황을 처리하기 위해 `beforeAll` 및 `afterAll` 훅을 제공합니다.

예를 들어, `initializeCityDatabase()` 와 `clearCityDatabase()`가 모두 프로미스를 반환하고 테스트 간에 도시 데이터베이스를 재사용할 수 있다면 테스트 코드를 다음과 같이 변경할 수 있습니다:

```ts
beforeAll(() => {
  return initializeCityDatabase();
});

afterAll(() => {
  return clearCityDatabase();
});

test("city database has Vienna", () => {
  expect(isCity("Vienna")).toBeTruthy();
});

test("city database has San Juan", () => {
  expect(isCity("San Juan")).toBeTruthy();
});
```

### [Scoping](https://jestjs.io/docs/setup-teardown#scoping "Direct link to Scoping")

최상위 수준의  `before*` 와 `after*` 훅은 파일의 모든 테스트에 적용됩니다. `describe` 안에 선언된 훅은 해당 `describe` 내의 테스트에만 적용됩니다.

예를 들어 도시 데이터베이스뿐만 아니라 음식 데이터베이스도 있다고 가정해 보겠습니다. 각 테스트에 대해 다른 설정을 할 수 있습니다:

```ts
// Applies to all tests in this file
beforeEach(() => {
  return initializeCityDatabase();
});

test("city database has Vienna", () => {
  expect(isCity("Vienna")).toBeTruthy();
});

test("city database has San Juan", () => {
  expect(isCity("San Juan")).toBeTruthy();
});

describe("matching cities to foods", () => {
  // Applies only to tests in this describe block
  beforeEach(() => {
    return initializeFoodDatabase();
  });

  test("Vienna <3 veal", () => {
    expect(isValidCityFoodPair("Vienna", "Wiener Schnitzel")).toBe(true);
  });

  test("San Juan <3 plantains", () => {
    expect(isValidCityFoodPair("San Juan", "Mofongo")).toBe(true);
  });
});
```

최상위 level `beforeEach`가 `describe` 블록 내의 `beforeEach`보다 먼저 실행된다는 점에 유의하세요. 모든 훅의 실행 순서를 설명하는 데 도움이 될 수 있습니다.

```ts
beforeAll(() => console.log("1 - beforeAll"));
afterAll(() => console.log("1 - afterAll"));
beforeEach(() => console.log("1 - beforeEach"));
afterEach(() => console.log("1 - afterEach"));

test("", () => console.log("1 - test"));

describe("Scoped / Nested block", () => {
  beforeAll(() => console.log("2 - beforeAll"));
  afterAll(() => console.log("2 - afterAll"));
  beforeEach(() => console.log("2 - beforeEach"));
  afterEach(() => console.log("2 - afterEach"));

  test("", () => console.log("2 - test"));
});

// 1 - beforeAll
// 1 - beforeEach
// 1 - test
// 1 - afterEach
// 2 - beforeAll
// 1 - beforeEach
// 2 - beforeEach
// 2 - test
// 2 - afterEach
// 1 - afterEach
// 2 - afterAll
// 1 - afterAll
```

### [Order of Execution](https://jestjs.io/docs/setup-teardown#order-of-execution "Direct link to Order of Execution")

Jest는 실제 테스트를 실행하기 전에 테스트 파일에 있는 모든 기술 핸들러를 실행합니다. 이것이 `describe` 내부가 아닌 `before*` 와 `after*` 의 핸들러 내부에서 설정 및 해체를 수행하는 또 다른 이유입니다. `describe` 블록이 완료되면 기본적으로 Jest는 수집 단계에서 발생한 순서대로 모든 테스트를 연속적으로 실행하고, 각 테스트가 완료되고 정리될 때까지 기다렸다가 다음 단계로 넘어갑니다.

다음 예시 테스트 파일과 출력을 살펴보세요:

```ts
describe("describe outer", () => {
  console.log("describe outer-a");

  describe("describe inner 1", () => {
    console.log("describe inner 1");

    test("test 1", () => console.log("test 1"));
  });

  console.log("describe outer-b");

  test("test 2", () => console.log("test 2"));

  describe("describe inner 2", () => {
    console.log("describe inner 2");

    test("test 3", () => console.log("test 3"));
  });

  console.log("describe outer-c");
});

// describe outer-a
// describe inner 1
// describe outer-b
// describe inner 2
// describe outer-c
// test 1
// test 2
// test 3
```

`describe` 및 `test` 블록과 마찬가지로 Jest는 선언 순서대로 `before*` 및 `after*` 훅을 호출합니다. 둘러싸고 있는 범위의 `after*` 훅이 먼저 호출된다는 점에 유의하세요. 예를 들어 서로 의존하는 리소스를 설정하고 해제하는 방법은 다음과 같습니다:

```ts
beforeEach(() => console.log("connection setup"));
beforeEach(() => console.log("database setup"));

afterEach(() => console.log("database teardown"));
afterEach(() => console.log("connection teardown"));

test("test 1", () => console.log("test 1"));

describe("extra", () => {
  beforeEach(() => console.log("extra database setup"));
  afterEach(() => console.log("extra database teardown"));

  test("test 2", () => console.log("test 2"));
});

// connection setup
// database setup
// test 1
// database teardown
// connection teardown

// connection setup
// database setup
// extra database setup
// test 2
// extra database teardown
// database teardown
// connection teardown
```

### [General Advice](https://jestjs.io/docs/setup-teardown#general-advice "Direct link to General Advice")

테스트가 실패하는 경우 가장 먼저 확인해야 할 것 중 하나는 테스트가 실행되는 유일한 테스트일 때 실패하는지 여부입니다. Jest로 테스트를 하나만 실행하려면 해당 `test` 명령을 `test.only`로 일시적으로 변경하세요:

```ts
test.only("this will be the only test that runs", () => {
  expect(true).toBe(false);
});

test("this test will not run", () => {
  expect("A").toBe("A");
});
```

더 큰 제품군의 일부로 실행할 때는 자주 실패하지만 단독으로 실행할 때는 실패하지 않는 테스트가 있다면 다른 테스트의 무언가가 이 테스트를 방해하고 있을 가능성이 높습니다. `beforeEach`와 일부 공유 상태를 지우면 이 문제를 해결할 수 있는 경우가 많습니다. 일부 공유 상태가 수정되고 있는지 확실하지 않은 경우 데이터를 로깅하는 `beforeEach`를 사용해 볼 수도 있습니다.

## Mock Functions

모의 함수를 사용하면 함수의 실제 구현을 지우고, 함수 호출(및 해당 호출에서 전달된 매개변수)을 캡처하고, 생성자 함수가 새로 인스턴스화될 때 인스턴스를 캡처하고, 반환 값의 테스트 시간 구성을 허용함으로써 코드 간의 링크를 테스트할 수 있습니다.

모의 함수를 만드는 방법에는 두 가지가 있습니다: 테스트 코드에서 사용할 모의 함수를 만들거나 모듈 종속성을 재정의하는  [`manual mock`](https://jestjs.io/docs/manual-mocks)를 작성하는 것입니다.

### [Using a mock function](https://jestjs.io/docs/mock-functions#using-a-mock-function "Direct link to Using a mock function")

제공된 배열의 각 항목에 대해 콜백을 호출하는 `forEach` 함수의 구현을 테스트한다고 가정해 보겠습니다.

```ts
export function forEach(items, callback) {
  for (const item of items) {
    callback(item);
  }
}
```

이 함수를 테스트하기 위해 모의 함수를 사용하고 모의 상태를 검사하여 콜백이 예상대로 호출되는지 확인할 수 있습니다.

```ts
const forEach = require("./forEach");

const mockCallback = jest.fn((x) => 42 + x);

test("forEach mock function", () => {
  forEach([0, 1], mockCallback);

  // The mock function was called twice
  expect(mockCallback.mock.calls).toHaveLength(2);

  // The first argument of the first call to the function was 0
  expect(mockCallback.mock.calls[0][0]).toBe(0);

  // The first argument of the second call to the function was 1
  expect(mockCallback.mock.calls[1][0]).toBe(1);

  // The return value of the first call to the function was 42
  expect(mockCallback.mock.results[0].value).toBe(42);
});
```

### [`.mock` property](https://jestjs.io/docs/mock-functions#mock-property "Direct link to mock-property")

모든 모의 함수에는 함수가 호출된 방식과 반환된 함수에 대한 데이터가 보관되는 특수한 `.mock` 프로퍼티가 있습니다. `.mock` 프로퍼티는 각 호출에 대해 이 값을 추적하므로 이 값도 검사할 수 있습니다:

```ts
const myMock1 = jest.fn();
const a = new myMock1();
console.log(myMock1.mock.instances);
// > [ <a> ]

const myMock2 = jest.fn();
const b = {};
const bound = myMock2.bind(b);
bound();
console.log(myMock2.mock.contexts);
// > [ <b> ]
```

이러한 모의 멤버는 이러한 함수가 호출, 인스턴스화되는 방식 또는 반환되는 결과를 확인하는 테스트에 매우 유용합니다:

```ts
// The function was called exactly once
expect(someMockFunction.mock.calls).toHaveLength(1);

// The first arg of the first call to the function was 'first arg'
expect(someMockFunction.mock.calls[0][0]).toBe("first arg");

// The second arg of the first call to the function was 'second arg'
expect(someMockFunction.mock.calls[0][1]).toBe("second arg");

// The return value of the first call to the function was 'return value'
expect(someMockFunction.mock.results[0].value).toBe("return value");

// The function was called with a certain `this` context: the `element` object.
expect(someMockFunction.mock.contexts[0]).toBe(element);

// This function was instantiated exactly twice
expect(someMockFunction.mock.instances.length).toBe(2);

// The object returned by the first instantiation of this function
// had a `name` property whose value was set to 'test'
expect(someMockFunction.mock.instances[0].name).toBe("test");

// The first argument of the last call to the function was 'test'
expect(someMockFunction.mock.lastCall[0]).toBe("test");
```

### [Mock Return Values](https://jestjs.io/docs/mock-functions#mock-return-values "Direct link to Mock Return Values")

모의 함수는 테스트 중에 테스트 값을 코드에 삽입하는 데에도 사용할 수 있습니다:

```ts
const myMock = jest.fn();
console.log(myMock());
// > undefined

myMock.mockReturnValueOnce(10).mockReturnValueOnce("x").mockReturnValue(true);

console.log(myMock(), myMock(), myMock(), myMock());
// > 10, 'x', true, true
```

모의 함수는 함수 연속 전달 스타일을 사용하는 코드에서도 매우 효과적입니다. 이 스타일로 작성된 코드는 실제 컴포넌트의 동작을 재현하는 복잡한 Stub이 필요하지 않으므로 값을 사용하기 직전에 테스트에 직접 주입하는 데 유리합니다.

```ts
const filterTestFn = jest.fn();

// Make the mock return `true` for the first call,
// and `false` for the second call
filterTestFn.mockReturnValueOnce(true).mockReturnValueOnce(false);

const result = [11, 12].filter((num) => filterTestFn(num));

console.log(result);
// > [11]
console.log(filterTestFn.mock.calls[0][0]); // 11
console.log(filterTestFn.mock.calls[1][0]); // 12
```

대부분의 실제 사례는 종속 컴포넌트에서 모의 함수를 가져와서 구성하는 것이지만, 그 기법은 동일합니다. 이러한 경우 직접 테스트하지 않는 함수 내부에 로직을 구현하려는 유혹을 피하세요.

### [Mocking Modules](https://jestjs.io/docs/mock-functions#mocking-modules "Direct link to Mocking Modules")

API에서 사용자를 가져오는 클래스가 있다고 가정해 보겠습니다. 이 클래스는 [axios](https://github.com/axios/axios)를 사용하여 API를 호출한 다음 모든 사용자를 포함하는 `data` 속성을 반환합니다:

```ts
import axios from "axios";

class Users {
  static all() {
    return axios.get("/users.json").then((resp) => resp.data);
  }
}

export default Users;
```

이제 API를 실제로 호출하지 않고(따라서 느리고 취약한 테스트를 생성하지 않고) 이 메서드를 테스트하기 위해 `jest.mock(...)` 함수를 사용하여 axios 모듈을 자동으로 모의할 수 있습니다.

모듈을 모의한 후에는 테스트에서 assert할 데이터를 반환하는 `.get`에 대해 `mockResolvedValue`를 제공할 수 있습니다. 사실상, 우리는 `axios.get('/users.json')`이 가짜 응답을 반환하기를 원한다고 말하는 것입니다.

```ts
import axios from "axios";
import Users from "./users";

jest.mock("axios");

test("should fetch users", () => {
  const users = [{ name: "Bob" }];
  const resp = { data: users };
  axios.get.mockResolvedValue(resp);

  // or you could use the following depending on your use case:
  // axios.get.mockImplementation(() => Promise.resolve(resp))

  return Users.all().then((data) => expect(data).toEqual(users));
});
```

### [Mocking Partials](https://jestjs.io/docs/mock-functions#mocking-partials "Direct link to Mocking Partials")

모듈의 하위 집합은 모킹할 수 있고 나머지 모듈은 실제 구현을 유지할 수 있습니다:

```ts
export const foo = "foo";
export const bar = () => "bar";
export default () => "baz";

//test.js
import defaultExport, { bar, foo } from "../foo-bar-baz";

jest.mock("../foo-bar-baz", () => {
  const originalModule = jest.requireActual("../foo-bar-baz");

  //Mock the default export and named export 'foo'
  return {
    __esModule: true,
    ...originalModule,
    default: jest.fn(() => "mocked baz"),
    foo: "mocked foo",
  };
});

test("should do a partial mock", () => {
  const defaultExportResult = defaultExport();
  expect(defaultExportResult).toBe("mocked baz");
  expect(defaultExport).toHaveBeenCalled();

  expect(foo).toBe("mocked foo");
  expect(bar()).toBe("bar");
});
```

### [Mock Implementations](https://jestjs.io/docs/mock-functions#mock-implementations "Direct link to Mock Implementations")

하지만 반환값을 지정하는 기능을 넘어 모의 함수의 구현을 완전히 대체하는 것이 유용한 경우도 있습니다. 이 작업은 모의 함수의 `jest.fn` 또는 `mockImplementationOnce` 메서드를 사용하여 수행할 수 있습니다.

```ts
const myMockFn = jest.fn((cb) => cb(null, true));

myMockFn((err, val) => console.log(val));
// > true
```

다른 모듈에서 생성된 모의 함수의 기본 구현을 정의해야 할 때 `mockImplementation` 메서드가 유용합니다:

```ts
module.exports = function () {
  // some implementation;
};

jest.mock("../foo"); // this happens automatically with automocking
const foo = require("../foo");

// foo is a mock function
foo.mockImplementation(() => 42);
foo();
// > 42
```

여러 함수 호출이 서로 다른 결과를 생성하는 모의 함수의 복잡한 동작을 다시 만들어야 하는 경우 `mockImplementationOnce` 메서드를 사용합니다:

```ts
const myMockFn = jest
  .fn()
  .mockImplementationOnce((cb) => cb(null, true))
  .mockImplementationOnce((cb) => cb(null, false));

myMockFn((err, val) => console.log(val));
// > true

myMockFn((err, val) => console.log(val));
// > false
```

모의 함수에 `mockImplementationOnce`로 정의된 구현이 부족하면 `jest.fn`으로 설정된 기본 구현(정의된 경우)을 실행합니다:

```ts
const myMockFn = jest
  .fn(() => "default")
  .mockImplementationOnce(() => "first call")
  .mockImplementationOnce(() => "second call");

console.log(myMockFn(), myMockFn(), myMockFn(), myMockFn());
// > 'first call', 'second call', 'default', 'default'
```

일반적으로 연쇄적으로 연결된 메서드가 있는 경우(따라서 항상 `this`를 반환해야 하는 경우)에는 모든 모의에 배치되는 `.mockReturnThis()` 함수 형태로 이를 간소화하는 달콤한 API가 있습니다:

```ts
const myObj = {
  myMethod: jest.fn().mockReturnThis(),
};

// is the same as

const otherObj = {
  myMethod: jest.fn(function () {
    return this;
  }),
};
```

### [Mock Names](https://jestjs.io/docs/mock-functions#mock-names "Direct link to Mock Names")

선택적으로 테스트 오류 출력에 `'jest.fn()'` 대신 표시될 모의 함수의 이름을 제공할 수 있습니다. 테스트 출력에서 오류를 보고하는 모의 함수를 빠르게 식별하려면 `.mockName()`을 사용하세요.

```ts
const myMockFn = jest
  .fn()
  .mockReturnValue("default")
  .mockImplementation((scalar) => 42 + scalar)
  .mockName("add42");
```

### [Custom Matchers](https://jestjs.io/docs/mock-functions#custom-matchers "Direct link to Custom Matchers")

마지막으로, 모의 함수가 어떻게 호출되었는지 확인하는 데 부담을 덜기 위해 몇 가지 사용자 지정 일치 함수를 추가했습니다:

```ts
// The mock function was called at least once
expect(mockFunc).toHaveBeenCalled();

// The mock function was called at least once with the specified args
expect(mockFunc).toHaveBeenCalledWith(arg1, arg2);

// The last call to the mock function was called with the specified args
expect(mockFunc).toHaveBeenLastCalledWith(arg1, arg2);

// All calls and the name of the mock is written as a snapshot
expect(mockFunc).toMatchSnapshot();
```

이러한 matcher는 `.mock` 속성을 검사하는 일반적인 형식에 대한 설탕입니다. 취향에 더 맞거나 더 구체적인 작업이 필요한 경우 언제든지 직접 수동으로 수행할 수 있습니다:

```ts
// The mock function was called at least once
expect(mockFunc.mock.calls.length).toBeGreaterThan(0);

// The mock function was called at least once with the specified args
expect(mockFunc.mock.calls).toContainEqual([arg1, arg2]);

// The last call to the mock function was called with the specified args
expect(mockFunc.mock.calls[mockFunc.mock.calls.length - 1]).toEqual([arg1, arg2]);

// The first arg of the last call to the mock function was `42`
// (note that there is no sugar helper for this specific of an assertion)
expect(mockFunc.mock.calls[mockFunc.mock.calls.length - 1][0]).toBe(42);

// A snapshot will check that a mock was invoked the same number of times,
// in the same order, with the same arguments. It will also assert on the name.
expect(mockFunc.mock.calls).toEqual([[arg1, arg2]]);
expect(mockFunc.getMockName()).toBe("a mock name");
```

전체 matcher 목록은 [여기](https://jestjs.io/docs/expect)에서 확인하세요.

> [공식문서 번역본](https://mulder21c.github.io/jest/docs/en/next/getting-started)
