# 20230512

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBBMELQQOIFMAuEBKaCuAnAdhACoCeADspPHDbVQEYkQCC+qAFgPb5MBi2EABQABAIZsAZtgCUEAMQBbZABMAltgXzV+Cclzz62VQBtUcbWCpzrEAIrZkAZ1SrulqAEkFZY8iVsIDmQIQxMzbQgAAyxUPHxSCgAeIgA+SIgAc2R8PVUAYwgAd1UOTmx0bEdtDIgSgDp3CF5OfWQAD1FvX0bI3tRHKjzuZwgJQgBeIQA3AC4Qzk5fcVlxlIgAbyooVQlp6S2oCFwcAggARgPkY0dKQ8Pj2NPoKgBfRtRyYNEISYBZEhicQSyESHwonF2YzWwGAEEcXGwxmUIWCACIzhAAD4wVFUXqRRprABqqmQhQg3CQJQAEth6HN2KhUGRHDMYf08uw6gArRx1FoZYDPEDASygCAAfSl0pl0ogAE0yvoAMKcZTBal6YKynVSiAisWwsHBf6AgjA5JrSZECDtVDZZSOIQrNbaXT6RAQAD8SAgc3wiOMYBhEAAom0KHlUIlQwBHbCiYyJDHY6AAGggppO8U+oM+ENG+BSxbTwdh4cj0bjCaTKZgGazjxzSWNBbGZ2LKVLZcCn0zAOzFtSP0wg9zqR7NoiZubIOH7FETr0uBaht7FH7M6HVuItra9vwjqEdRPolwNTm4hILtqOj0mG9D7mU04qmUlmNm7HSRtdodTsEE86jPDJWQgK8b2wfAAGt8E4QoixHLdxxSMUQElXVZWIJx0GVRcnAwzC5QNVRvBadBP3WMN40TDMK2QKMIBeUYV00AByYRjTgTlE18fAskcYByhMRw2I-Ps8nwp1JgAbSoeioxjGik2cXBqgbAcmwtQQb1U6pO1LKAFKrZTk2gABmDTkKSHSfjWM4LIM+SIwYkya0SVUunaAB5ehuVcqzvxBWzVggTyfB8vzXKcoyXMU6tE0SAAFVjVBuRJ6AWJYi0CrTcxCtYUs4BQ0pBTLFmQcROy7ZzKyU9yCogNiJAWNjcqBfKb0a5rWpisM4rcxK63TL88pbfNISLEtatc+qhqxetRo68bwUmjtpoAXXEjdwt8NpfP8xjJk2KBRDmGSHIzHrODYraoHoM85jY9grmMG6qDIY4ph0-0NHoPQwDeMAhnwEYxhHQRZnmCrljsiApkfDE5meEGwfwDFJkhuZyuyjNCkvHgbwRn0kZgNDCKIiUmjwIJ9AAZXtFkKaI-VRVAKg1jphdjggEglThRZhOGBkmRZNlgA5LleX5c8hWAcRHEKAGoGJUlyUcQWXGFiBGWZVl2UcTkeT5AU5Y14whdBjnMxaYJlQXYw+IEkW9fFyXjZljIwANIA)

```ts
type MyReturnType<T> = ReturnType<T>;
// T in ReturnType<T> has error
```

처음에 utility 타입을 이용해서 그냥 작성하려고 했더니 T가 함수인지에 대해 에러가 뜸
`ReturnType`을 사용하려면 **T가 함수인지** 에 대한 정의 필요

```ts
type MyReturnType<T extends (...args: any) => unknown> = ReturnType<T>; // ⭕️
```

any랑 unknown의 정확한 차이점을 모르겠다. 왜 args의 타입으로 unknown을 작성하니깐 에러가 나지..

[함수는 argument 타입에 대해 `contravariant`한 성질을 지님.](https://stackoverflow.com/questions/66410115/difference-between-variance-covariance-contravariance-and-bivariance-in-typesc)

`T`가 `U`에 할당 가능하다면, `(...u : U) => void`가 `(...t : T) => void`에 할당 가능하다는 말
그래서 argument에 unknown 할당 불가

```ts
type MyReturnType<T> = T extends () => infer G ? G : null;
// Expect<Equal<1 | 2, MyReturnType<typeof fn>>>,
// Expect<Equal<1 | 2, MyReturnType<typeof fn1>>>,
```

utility 타입을 사용하지 않고, 직접 작성해본 타입에서 파라미터에 대한 정보를 입력하지 않으니 함수로 받는 경우 에러 발생

```ts
type MyReturnType<T> = T extends (...arg: any) => infer R ? R : void; // ⭕️
```

여기도 마찬가지로 argument에 대한 정보를 넘겨줘야 함.

```ts
/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<string, MyReturnType<() => string>>>,
  Expect<Equal<123, MyReturnType<() => 123>>>,
  Expect<Equal<ComplexObject, MyReturnType<() => ComplexObject>>>,
  Expect<Equal<Promise<boolean>, MyReturnType<() => Promise<boolean>>>>,
  Expect<Equal<() => "foo", MyReturnType<() => () => "foo">>>,
  Expect<Equal<1 | 2, MyReturnType<typeof fn>>>,
  Expect<Equal<1 | 2, MyReturnType<typeof fn1>>>
];

type ComplexObject = {
  a: [12, "foo"];
  bar: "hello";
  prev(): number;
};

const fn = (v: boolean) => (v ? 1 : 2);
const fn1 = (v: boolean, w: any) => (v ? 1 : 2);
```
