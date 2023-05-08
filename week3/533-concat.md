# 20230508

## [문제](https://www.typescriptlang.org/play?ssl=21&ssc=30&pln=21&pc=47#code/PQKgUABBCsDMsQLQQMIHsB2BjAhgF0iUWJMICMBPCAQQwBMAnAUyoGkGcBnNAN04GsqACgACZZrAAM-DgDYAnFk4BKCAGImXKmpwMOFMITXGIARQCuTTngCWmQ1ACSAWwAOAGybOmGPBDwAFkwQAFI4PDgAylgMNq5+AAbUejgUAHRYmLh4CRAAZubYtpgQNhj+Qf4UrsGcFNZeaTRVNf44-FYVwXgA7mgQugDm5t6+nE0AKpVo5niusxCcATPudBBkwTgQGEw9AylUgfil2O7mdJ1l83icJxDueAwQaAwXDA4QAGIvEEwAHjg3J4AFwfBLgm6EPDVYIAJSs5geEAAvKgsvgADwAbQAjABdAA0ECxACY8QA+CDAYC-P41LB4JhrPD9DbEnFEsmEcEJD6UgBqNl2z3KAHEbHgABLmMjAiABPBzTjA6k3LABNIAK3GL0GwDgsDAIGAhlAEAA+pardarRAAJozJ7oC4QSVMZgWm1e80QY2GaGtdDYTETIkAVUpqImtMZ9FuzBwdEw7iohX4GDQPQwWLxEAA-BAwzGfHR45okxgUxA0xmszn88S0k3QxAm2kw7m5Vi2xNO8S8aaaQHgkHshjo-9Y6WBhgKDnw8W4zO5xSUY3m0S2x3TSBPd7rRAJlY-CguJ19zbfSabG4Xn5hxAAN4QACiAEdzDh3ESX3SmAyIAAX3yBg0GcCAAHIRGHRB1S-TwMEGKxgFmGx3E4CD-RhCBcE4TpUSxQhf3pPAMXfT93AxUdMXnftySJHNyXooi-wZMiPy-Kj0VI2jcQpBj8SYgkWJI9iKK44MeI5CAyQY2AiQAFn49lOSJeSICUoSRP-UjyM46ieIgnEINUyDYAgwliTyL88KJMg0DQTwcAwIkIIUiz6OJIyTJk1zzKJaz0KYOyHKclzIPcilmIHMAzQvA9PnMBhAndCBIkZVxbni20-VAQhKUiAJdGCChHUWRzUMwZV5UVTKVWANUNW1NJdX1eBgGczgendfKIEFYVuDOYoMGqhUlXqxqtR1Bg9QNYBBsqkbeoAWReEcivcBCkNG2rlVVTh1SmlqZqNE0gA)

```ts
// type Concat<T, U> = T extends [] ? U extends [] ? [...T, ...U] : [...T] : [] (❌)
type Concat<T, U> = T extends any[]
  ? U extends any[]
    ? [...T, ...U]
    : [...T]
  : [];

type Concat<T extends any[], U extends any[]> = [...T, ...U];

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<Concat<[], []>, []>>,
  Expect<Equal<Concat<[], [1]>, [1]>>,
  Expect<Equal<Concat<[1, 2], [3, 4]>, [1, 2, 3, 4]>>,
  Expect<
    Equal<
      Concat<["1", 2, "3"], [false, boolean, "4"]>,
      ["1", 2, "3", false, boolean, "4"]
    >
  >
];
```

처음에 왜 [] 로 extends 해줬는데 동작하지 않지?? 하고 고민했던 문제
extends [] 하더라도 단순히 array로 취급되는게 아니라 어떤 타입의 array 인지 명시해줘야함.

any[] 로 표기하긴 했지만 `readonly unknown[]` 도 똑같이 동작하는 듯

왜 `readonly unknown`은 동작할까?

- readonly가 붙는건 [length-of-tuple](/week2/18-length-of-tuple.md)에서 언급했듯 길이가 변경되면 안되기 때문인 듯
  - 그렇다면 unknown 과 any의 차이점은??
    - 일단 둘 다 해당 타입 변수에 어떤 값이던 할당이 가능
    - 하지만 역순으로 할당할 때,
    - `any`는 `number` 타입 변수에 `any` 타입 값 할당 가능
    - `unknown`은 `number` 타입 변수에 `unknown` 타입 값 할당 불가능
