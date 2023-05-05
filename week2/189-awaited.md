# 20230504

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCMAcCcEC0ECCB3AhgSwC4FMATSZJM8kgIwE8IBZTAY23wCsIBlbAawHsAnTBAAUAAQC2TFqwDOPAZgCUEAMT5MM2ioAO-XuOwz8qygFdsAG1xJsAOzAkVTiAEVT+Gbmy97JAJIAZhDoxgAWmABuxkK41NrG6KHYjKEQhsGC2vGEELHxEBY8xgAKegZGAHQQABK86MHGjJi2EADm+LgQMXEJSSlpMmm2coTGuKEJmdm5PQD8DlAAYgIQ+AAemOLaFvgAXGlBIRDhURAABqX6hvgAPACiG1s7ACo9AHxnx3W5vG0dEA9Ntt8K94vMSGdIbgZCQ8sZAU8QT0IABeCCXcq3Tz8OytN4LGb5ABKHlMVlR9GoGBwBEI90ewNB+DeEGAwAg2NxEMhBJZzySgwAju5PN4WultAJaRAAmVchMIABtATYVp2TAWLr8LyMHYAXWEoVwuG0Ml2bNGEQquF4wEkjDkfEEwEwhAizUYRCQcJkjBx2ms63w-GYRhkSGFHi8PiQ0CQABYAKzcePKGhKiRSNiOhQGo0ms1stXjUyUCqMfR2rOyeSCRS8iAANRY9R8EAA4nhqqX9vnTebgNCUhVZBUBK1gHB4GAQMAHKAIAB9Zcr1criAATV4pn4EAAwrxRjVg8Y12flxBZw44ZTqXgiDdniy0XfaY-8WAF+ezxBnlH9xoHhLt+q6XnO2BbFKhLGAA3gCwoagANACazxIwnQAL4ynKADkohwkgKQajstjtDIwCmF4FgyDh17IgAGhSGLXDcnKkfiN4bkxZQsXBAQsBYhD7LYpjiJQwYQBhHHIgAWtxVxGDczGKWxrQQAAPhAIlicGbzSfkMnQPJmJKTxinKViuA4qRGkQJQvC8DszR6fpxjPBScHjPgtj7MIPgBGS-EWDsQkiJg-CtMJonifwygoiyzTUHFCW2LQGF0fkTRhhSiokA8aG4PcCEWDcdBUlg950vRbzIapemIXlqH4OhRWmBqpXlTSD4bjVEB8QJoXaTFkn1Y1BWte1ZWvg+Mm9aptlDbpNVjc1hV3MVHXTXShlzVZuK2fZjnqLYo1QPlq0TSVU0VW+T7IYt-CjXq87svh4brAVSDBno-BgDe30rGi11dXSD0fl+IHrosO5ebuHAEKawGQ4uYGfuAUAshw4T8MY1DbruMiOZRYpmscxr9myQ6hCOMhjhFk4IC6wwhL9GNNi2HJE9Gwy9uThaDr61OjuODPwMAhMWMTPgwmzdACMYe7hMF3lkbzBYDlTNN060M5zkAA)

```ts
/* _____________ Your Code Here _____________ */

type MyAwaited<T> = Awaited<T>;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type X = Promise<string>;
type Y = Promise<{ field: number }>;
type Z = Promise<Promise<string | number>>;
type Z1 = Promise<Promise<Promise<string | boolean>>>;
type T = { then: (onfulfilled: (arg: number) => any) => any };

type cases = [
  Expect<Equal<MyAwaited<X>, string>>,
  Expect<Equal<MyAwaited<Y>, { field: number }>>,
  Expect<Equal<MyAwaited<Z>, string | number>>,
  Expect<Equal<MyAwaited<Z1>, string | boolean>>,
  Expect<Equal<MyAwaited<T>, number>>
];
```

다른 정답

```ts
type MyAwaited<T extends PromiseLike<any | PromiseLike<any>>> =
  T extends PromiseLike<infer V>
    ? V extends PromiseLike<any>
      ? MyAwaited<V>
      : V
    : never;
```

[Await type](https://www.typescriptlang.org/ko/play#example/async-await)
[Promiselike](https://microsoft.github.io/PowerBI-JavaScript/interfaces/_node_modules_typedoc_node_modules_typescript_lib_lib_es5_d_.promiselike.html)
