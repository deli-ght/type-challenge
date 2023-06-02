# 20230602

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCM0JwQLQQEoFMAOAbAhgYzQEEstIlELKyAjATwkIDsAXACwHtH6AxAVwgAUAARwsAZrwCUEAMQBbNABMAlrzmzmaOdhybEWZZoBOOUmRkWIARV5oAzs2WcwZAJLasWtCwgADdDoExFgAPADKADQQ3EbsclEAKuwAfL4QAO6synisEEaYuAQQbGgQpljFrKV2vNQORsqMAOZ+MXFp6Ya5vklpjZWlTcoAbt4Q9Y0tvmG+LlDc7EYQaAAeOB5oc36+vsx2ZMy0GKX5gUoQALyoBfhEJCEA5MwQ9BjL4w9RDxCfPw-JEGAwGWK2OeE0imK7Ag1FKTyO9geZB2szIAIAaso0OkIJwIABxQwACVqAC4IKxmMwMHZSUC9jkAHQAKzsjMWTWAsDgYBAwBcoAgAH0RaKxaKIABNdi8JYAYXYilKRLQ+WF4o1QogfJch2O1zOwXCIM0jEUdnGzAazSibXUq1N5st1qaiWhDu8TomzQBVzCJs9Ft8ABIAN6NMSqhgAXzDdtj4cYkaWACFo74APzRWL2laOi0AIgLECzEDC5L8YcICaSCYChTuoRTtpzbuS6Yg5LCApA6s1YogCXszzlODs9j7-ZF2v5ym0i2eetKoYgAFEAI68UxRVegtDgiDRiBiHM-IRLxA5creJr2YC8RxYOxIsBLiB4McTq4AbTIu7BzAhBuW6hPWtxGg8YjsOw1A4EYvwPLB8FfFB7D-Ch0Gof8yQRH+e7gkBm6mCEYFBPckHQUhCGwU0CFYThPyoVRyQ4XhAGESBJE3GRoQUTBcFUV8gmMdB6EiewqH0axUD-vugHAcRpGNo8zyvO8z5fD8XxifCxzPixuEyfh8lEaB3HKXxSHCQ8dGiQxlkCXB2GGWuxkcYp5kQUhWFCU5GFofZkl2dJrnsQpZmGuRTFwdFyE-DB1E6VB3n8fBBlsXJ7kRQ2EHJdBRh5X5PzUGhQlJTBizJU56VGWFplcZFvEIc19nOWAAC6PaTlO0SyiUSxhJoNLdf2M5gKAaJlqwcGlLQMpLHY7BYA+TiMLSFJUjSdLAAyrAsmyHJcvAwCiHY6SqpNmLYuMS0rZw62UtStL0nYTKsuyRictywCLctjj3ZNACyiylHK00kDe9jko9W0vW9B2fby-JAA)

```ts
type ReplaceAll<
  S extends string,
  From extends string,
  To extends string
> = S extends `${infer A}${From}${infer B}`
  ? From extends ""
    ? S
    : `${A}${To}${ReplaceAll<B, From, To>}`
  : S;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<ReplaceAll<"foobar", "bar", "foo">, "foofoo">>,
  Expect<Equal<ReplaceAll<"foobar", "bag", "foo">, "foobar">>,
  Expect<Equal<ReplaceAll<"foobarbar", "bar", "foo">, "foofoofoo">>,
  Expect<Equal<ReplaceAll<"t y p e s", " ", "">, "types">>,
  Expect<Equal<ReplaceAll<"foobarbar", "", "foo">, "foobarbar">>,
  Expect<Equal<ReplaceAll<"barfoo", "bar", "foo">, "foofoo">>,
  Expect<Equal<ReplaceAll<"foobarfoobar", "ob", "b">, "fobarfobar">>,
  Expect<Equal<ReplaceAll<"foboorfoboar", "bo", "b">, "foborfobar">>,
  Expect<Equal<ReplaceAll<"", "", "">, "">>
];
```

처음에 그냥 true 인 경우 전체 재귀를 돌리려다가

```ts
  Expect<Equal<ReplaceAll<"foobarfoobar", "ob", "b">, "fobarfobar">>,
  Expect<Equal<ReplaceAll<"foboorfoboar", "bo", "b">, "foborfobar">>,
```

같은 경우에 중복 제거가 되어버리니깐 그게 아니라는 걸 깨달았고,
결국 조건에 조건을 거쳐 해결. 왜 extends는 not 처리가 안되는걸까.. 타스의 문제인가..
