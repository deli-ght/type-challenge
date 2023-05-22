# 20230520

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCMBMEFoIGEAWBDAlgO3QIwBsBTCAeQAcAXTAe2wGdJEEXWm8BPCAQW0tTpcAYgFcIACgAC6PgDMRASggBiALZEAJphGqV6cuQKYAxump0wTZdYgBFEUXrnslqGiy5CJGlVoMI6ABOJMY0qqp0BFwi9JoQOBAAUugAbuj0xoGYVAB0EABCIpQQAO6oRNilJPQlmJTGqBCUNBAAKhzkRADKmdmUADQQppUcNGLkgT5EgVFNHSR1APyuEACSlfyY9EMYBMTYAOZEg6Ni2ERxzXOdAZU0eABWRMbFNIEBQwTp20hlZkQpaYQU4QIwAaxISCuExoKUwGhIlBKLXk2BefggAAMfM5xBCOIM0gQHApMbcNFijpRxKS8ussTi-JiTmMhjIIEQAB6UCoU-ghESBYJ8IZ0WSYA7XEicJrlCAHTCAyr48kQIkOPIAdWqAhEBAp+DGxSu6GMxkc235EHFuAIEGC9D1xTh6EpREomJyKyEbw5nPQqkMRBWmNDlEYUARxi+wVFDGKoWw4oOAC4UBgcPhiCtE057Y4nRAALxx5NMKA5Rl0cQAclkNBoNcGcAAzApyxBK75qzXcOomxAa5R5ggGug9hUjvQa+2oBWq9ha3gggOAN5q8cONM1gASRD2LU1b31NYgAF9Z3OclSaStgMA-Z0XrLEfMIDRZPnHQRjS08EQUyYHAeUCWRTRIAAlAsfwgVcO3rGg02wHR-0CDs+wAiAnCyQ4O2XQI0zguc53VTDsJwA4OzPJhqKgUNMRWABNVkNDoIcIHOS4WhKLIeVuLgHnoYBw1BGgFWMJoWgwbANGIF8IBhLxdCQB4YmKBJhxuYhAQIL0mGYsRhgCehHXUWUzCxfEyUiLhTXNKhtkxcjDjJGQ+TlTFSLJIz-34zZDkQCBVLzYhUgWYp0gQLY8i6AMSExKzSjY4pfPIb5Llqc09KgAA+CAADVMCIEp30qABxOodxEPA01QShKHIegU3vcMGhyQTK0CA5gDgMAQGASxQAgAB9UaxvGsaIAM95kBoBEID3WMJuW0aIH6yxNJIdxMy8AAeCDi3fR5nkoPKSyI99u2wXaAGk-R5GTtnxD9+MGfKcvEDt8TTO6uQejQnqIUZPwgjsoEWCR8vu3ltgggBtG6AF0IAh85AXeH7L2In7+g7Ui03ypgFDTbbPGIXbSFUOp9sGG68oAMggKDQkCDRbrenKcqYG9iaZsBqLAIaVuWtpHGKZB0kcEbhfGtaBswQM3mNN9124cFjggABRTkn2KM9rUmXQa0kTbR12fYp2AIpMAIadLCjGMQjoPN0BJjMyeDMBc2KB0nWgQ70CYLtcTrBsB1bS9g78JcV0Gdd8cHPcDwgI8Zg0U8LyDhdawwgchxHMcJ0ORwZyDnnLG9r8nXgEtA-nK6c7ivOZBofl3lzy97wgE36AQLldb7oU3izhveybwYay+PMO7L91by952fegygWwDkeQ9zieW7bjim8j7Ox-7ZtYDbWfqXbMBNrZWJthLOGmG13XdrVzAIV2zaXt9n9oEGR+Ts0aAnNcZQD-i8Z+6t37zE-svWAv8db-w0LAIBD94FgJfm-D+n4v4rzgbrTQLZkGIw2m+UBPIND+3OkwBCSEULTHYEEQieNNxkUoDhSiUBaK73UGmZylEBZX1IZoGusEmAYR4awii-NiE3EERoVelCoBiI4rQtCAshYy0mqIQIO8ug8katLDRw05aC3ALlCAXQMCxlOO8egNBiTOCahAOqDUmotQyKgdq9BOrdTgMAGQNQ6FmMKsVLCdjrbO1qvVRqzVhLuM8d4nqsBgC2PsX4CMEA8oAFk3hbXNpORwkSXExNah4jqbxKLrSAA)

```ts
type Chainable<R = object> = {
  option<K extends keyof any, V>(
    key: K extends keyof R ? (V extends R[K] ? never : K) : K,
    value: V
  ): Chainable<Omit<R, K> & Record<K, V>>;
  get(): R;
};

/* _____________ Test Cases _____________ */
import type { Alike, Expect } from "@type-challenges/utils";

declare const a: Chainable;

const result1 = a
  .option("foo", 123)
  .option("bar", { value: "Hello World" })
  .option("name", "type-challenges")
  .get();

const result2 = a
  .option("name", "another name")
  // @ts-expect-error
  .option("name", "last name")
  .get();

const result3 = a.option("name", "another name").option("name", 123).get();

type cases = [
  Expect<Alike<typeof result1, Expected1>>,
  Expect<Alike<typeof result2, Expected2>>,
  Expect<Alike<typeof result3, Expected3>>
];

type Expected1 = {
  foo: number;
  bar: {
    value: string;
  };
  name: string;
};

type Expected2 = {
  name: string;
};

type Expected3 = {
  name: number;
};
```

참고 답안 : https://github.com/type-challenges/type-challenges/issues/15337

1. `get()` 함수는 리턴값 `R`을 가짐

```Ts
type Chainable<R = object> = {
  option(key: string, value: any): any
  get(): R
}
```

2. `option()`은 Chainable 자체를 리턴함

```ts
type Chainable<R = object> = {
  option(key: string, value: any): Chainable;
  get(): R;
};
```

3. 그러면서 동시에 모든 Key-value 값을 기록

```ts
type Chainable<R = object> = {
  option<K extends string, V>(key: K, value: V): Chainable<R & Record<K, V>>;
  get(): R;
};
```

4. 재귀 종료 옵션 추가

```ts
type Chainable<R = object> = {
  option<K extends keyof any, V>(
    key: K extends keyof R ? never : K,
    value: V
  ): Chainable<R & Record<K, V>>;
  get(): R;
};
```

5. 다른 value를 가질 때, key 반복 가능

```ts
type Chainable<R = object> = {
  option<K extends keyof any, V>(
    key: K extends keyof R ? (V extends R[K] ? never : K) : K,
    value: V
  ): Chainable<R & Record<K, V>>;
  get(): R;
};
```

6. `R & Record<K, V>`는 키의 값을 덮어쓰는 것이 아니라 합치므로 R에서 이전 K를 생략해야 합니다.

```Ts
type Chainable<R = object> = {
  option<K extends keyof any, V>(
    key: K extends keyof R
      ? (V extends R[K] ? never : K)
      : K,
    value: V
  ): Chainable<Omit<R, K> & Record<K, V>>
  get(): R
}
```
