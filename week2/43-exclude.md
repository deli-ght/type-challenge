# 20230503

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBAsDMEFoIFEAeBjANgVwCYFNJEETSiAjATwgC0ALfRgOwHMIAKAAQC8HmWAlBADE+AIYBnasPLYAlpgAuCOUxHYmcgPZMwRYQYgBFbPgmLtuogEkAtgAdM+W-iaKIihhFkLlqlBg4BAA8ACoANBAAqgB8elAxAVh4+BAAZgBOWrYQoR50WhKpipT2Zvli7mIZqZIScixMYuROHlrR8RAAYloZEPioYg5OAFydAAaTihJEJWUQAEpm2EoQALwQALKUaMkhAORi+xAAPhD75Mdn++j7kYf7icDA55en57dEk+OdiQBqcnwAHcIDoIABxOSKAAS2HIIwgdEUinsEhGz2m6DoADoAFYSbG9FjAOBgEDAPSgCAAfVpdPpdIgAE0tNg+gBhLQECDQ-A1GkMwXUiDkvRzVLbXZBfBhSKxdZJaWy6JxMBUoWC3JmdzsyTlDUMkUUuQOXrucUQADeKAAjtgxJhImgyuh3ABfdJZHL7TjihBYh1OVhmYDYCyYCT7MWlVLoPUSBUAbSIzvwruCyDtDuCksCKWCD3eFyuHzu5yOMXub2utxilZTqBdigzWcwOZ2eYORyL1dL92710uldLdfCDabLftbdzexl5gyqjYZyY2Fs5D573Y7CEa0SADctHJcAJIl0NK7LMP54v3iu13zR2AALqUkACg207pszwbgDKinwVF3w-I01XABIIF-OhqlSShWT6CQtBwCwdDRRFkVRdFgExHF8UJDJiTgYAxCYCQgT5Ih-kBEFEOQyw0KRFE0QxCQsTxAkiRJWBgFosN6MorZelSdloMwIMWDMBFGMwli2LwokyQpIA)

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
