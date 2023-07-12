# 20230712

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBDMCMAc8IFoIBUCuAHANgUwgBcB7CAOTwGdC8ATCAeQCMArPAY0MhWV7+6YBPCCwCWAQwB2Ac0oALKRAAUAATFTZCyQFs8hcQEoIAYl21RGbSeKsOhE4Wz4w3Y24gBFDFUKjiklygAcVEANzxJCHEiJwJCQSwCAAMUtBSkogV7fxxhdn99UUlKCGoAJyLpIgS8ABooyXpo+MSIdIBVdPqmDFEcJsibNk4IMo4MMsowvFyAOkC2lJaqdgqsLihlqIgAXnRYtGIKajpmYcIAHgBtAHJxG4BdevLKgD4IYGAIAG9xAC5SoQKjIAL7cLZMXb7XB4Q7HGi0M52a53G71G5MR71SSWJh4MrvT4-f4-JgAnHaPFlEFgzY1CDsKGYGFwnynWyca5PCBMYjEfBSQlfXn8vBSWYQUQAM0ycVikpKeG060E9RYGGooz0E0ihDkBHa1US3HSC3eADVRHgAO4QfwQEKEAASGDJEDkhEIWEof0+hEo7DksxYlFmxDK0mAcEQYBAwBcoAgAH0U6m06mIABNYgTCAAYWItAITvxBHT5ZTEDjLi2zPwrJOiI5lzQ9Xa7z2UkECZAyYr6fQPnz4koVD7-Yz1dEyvD9i23wgAFEAI4YcQ4eqLgAeiRGIIgUrKxCsNxUy2QgfX+BkVGAGF8OEoNxr9PYI7Heyu3G3u8uK7XOAXHWsJHGyTbnCi9zci8MivPUC4kjBVQgq8cHfjuyL-uuQEHKBjZIpytz3OimLchSVJwT8UQAgubrkfiED7ihaFQD+mGrthwENgiBGXERaIQBiAk3OwWI8nyAqSJRCE0TysnsACIqSYxKnMbU6G-hcWGAVxeE8c2XLdBJYpSUZoqCmhDw9uOE5JhAABiEx6gxADKNDejZE5VvGoDcO8LkKGMECCDmZSlPy95+MUAIel6Pp+gGQYhmGEZRgg8DAFIlDWvifkQJaNrhTgkX+D67qet6vrAP6gbBqG4aRtGGWUBFvilXlACy4YEHmCg4Ne0hUDFFXxdViV1Sl0ixvGQA)

```ts
type TupleToNestedObject<T, U> = T extends []
  ? U
  : T extends [infer A, ...infer B]
  ? A extends string | number | symbol
    ? { [K in A]: TupleToNestedObject<B, U> }
    : never
  : U;
```

```ts
type TupleToNestedObject<T, U> = T extends []
  ? U
  : T extends [infer A, ...infer B]
  ? {
      [K in A extends string | number | symbol
        ? A
        : never]: TupleToNestedObject<B, U>;
    }
  : never;
```

```ts
type TupleToNestedObject<T, U> = T extends [infer F, ...infer R]
  ? {
      [K in F & string]: TupleToNestedObject<R, U>;
    }
  : U;
```

`A extends string ? A : never` 를 `F & string` 이렇게 표현할 수 있다고 함. (Narrowing type)

https://www.typescriptlang.org/docs/handbook/2/narrowing.html
근데 공식문서에는 따로 얘긴 없는듯..한데...
& 가 interfaced의 extends와 같은 역할을 하고 있다고 보면 되는듯

테스트 코드를 추가한 뒤 다음과 같이 변경하면 잘 통과함

```ts
type TupleToNestedObject<T, U> = T extends [infer F, ...infer R]
  ? {
      [K in F & (string | number | symbol)]: TupleToNestedObject<R, U>;
    }
  : U;

// Expect<
//   Equal<
//     TupleToNestedObject<["a", "b", "c", 4], boolean>,
//     { a: { b: { c: { 4: boolean } } } }
//   >
// >;
```
