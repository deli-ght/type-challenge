# 20230503

## [문제]()

```ts
/* _____________ Your Code Here _____________ */

type MyExclude<T, U> = Exclude<T, U>;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<MyExclude<"a" | "b" | "c", "a">, "b" | "c">>,
  Expect<Equal<MyExclude<"a" | "b" | "c", "a" | "b">, "c">>,
  Expect<
    Equal<MyExclude<string | number | (() => void), Function>, string | number>
  >
];
```

Exclude 타입만 알고 있다면 쉬운 문제

```ts
Extract<T, U> =  T extends U ? never : T`
```

풀어쓰는 방식도 알고 있어야 할 것 같다.
