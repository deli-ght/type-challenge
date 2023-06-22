# 20230622

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCMAMCcB2CBaCBJAzgVQHYEsB7XSVFci0gIwE8JcBXAGyYgAoABKgU1wGNCAJwCUEAMQBbbgBN8DCeIYFiYUmPUQAig26YALkRKl0EgA5NuU3HogBDCHpqnuEAAZY8h1wBoIAdwALfD4Ah1sAa107XAh8XFMGG0dnNwAVV2jpCEFuPQZBXEx-ANySwTSMnMxCJgA3KL1COwglQwcnbgA6VSgAMSEIbgAPWzMLAC4eqDdXVz1MUihklz5bTG5oCABeDBxlXAAefUE4gHMAPihgYAgAM1smdcX2lNX1gCZt3c9iI70T3CnAA+jAkPEElwg1wcgh0z2WEDe3AAzF8PPsDgBtY5nEHycEAXUh0Puj24z1mrimlwAavhuH4IMQIABxfB6AASDCo4wgAT0elMmHG13mIU6ACtMJ0hKdgHAkGAQMBVKAIAB9TVa7VaiAATUI+QgAGFCNIXBzuDkNTrbeqIMrVAj0YYDqlLjtbLgaKqQDa7dqIKldDZjWsogGdQ6VfgzEIkh0IABvCAAUQAjgwHr5U0NnHwbABfO6CQgKADkHGWKBCDwsgN0wES+Ee5adiaRRR2mNIufzegOGazTAOLt+OMB518pPW5ynvbz3ALg8zD1He1dE9OECB9HxVqnMJ0c+8C-7K+H65+h3LtnLO4g5ao9935b4L8f0nLh-+x-nUD7JcByHNcx0OJRzVuOIZAfRgWAfWpCHwLJX2-Xxf24E8zyAi9QI3X4U1sXktwgYtd0I3lQXBUif1hTD-zTRdlxAkcwIOCiIBI3cqKtGjpweWcGMA5jV1Y-DDmxf4zlg-dBCJfiySwq4bjDdYikCK0XFSbJdBqeoikaZpcGIFBWmZZZugApjgNEq8MS4+huHqCEFME08rPPFi7M3KTAQfJRwmMvxcEPGd6PcxjPNstiHK9GhQoE8LsJEy8Yt87dXzvBLFKE6zcLE68DlwJyD1cpKCV9f1I3tXp8j0MoIAAZT0bghSqyNozAUBSEuRqAlsa0aENcpqiYZtiGFPkBSFEVgDFAJJWlWV5QQRBgC9TA-CtHqIDpBlOJqcbCl5flBWFUVMHFKUZUEOUFTW0ajoWKBLgAWSEFxjX6lheFOXQTum865suhbrtlJUVSAA)

```ts
type IsUnion<T, B = T> = [T] extends [never] ? false : T extends B ? [B] extends [T] ? false : true : never

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type cases = [
  Expect<Equal<IsUnion<string>, false>>,
  Expect<Equal<IsUnion<string | number>, true>>,
  Expect<Equal<IsUnion<'a' | 'b' | 'c' | 'd'>, true>>,
  Expect<Equal<IsUnion<undefined | null | void | ''>, true>>,
  Expect<Equal<IsUnion<{ a: string } | { a: number }>, true>>,
  Expect<Equal<IsUnion<{ a: string | number }>, false>>,
  Expect<Equal<IsUnion<[string | number]>, false>>,
  // Cases where T resolves to a non-union type.
  Expect<Equal<IsUnion<string | never>, false>>,
  Expect<Equal<IsUnion<string | unknown>, false>>,
  Expect<Equal<IsUnion<string | any>, false>>,
  Expect<Equal<IsUnion<string | 'a'>, false>>,
  Expect<Equal<IsUnion<never>, false>>,
]

```

어제 배운거 활용하기
```ts
[T] extends [never] // 타입이 never인 경우 걸러 내기

Expect<Equal<IsUnion<never>, false>>,
```

T와 같지만 다른 타입군을 비교하고 싶을 때

```ts
IsUnion<T, B = T>

// 그냥 T로 비교하는 경우,
T = string | number

T extends T ? [T] extends [T] ? false : true : never
== string extends string ? [string] extends [string] ? false : true : never;
== number extends number ? [number] extends [number] ? false : true : never;

// Union 타입이어도 전부 동일한 타입으로 잡히게 됨.
```


