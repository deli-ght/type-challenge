# 20230607

## [문제](https://www.typescriptlang.org/play?ssl=36&ssc=1&pln=19&pc=1#code/PQKgUABBBMCcBsEC0EAKBTATgWwK4BcBDfASwHsA7SZJWu6gIwE8IA5Qs-MiASQGtcFbgAoAAgAdCFACZSyJTAEoIAYmzppJXNlWDyVaiqMQAirnQBnUpTDUe2cQBt06ivgjiseItYoR8TJ7+ABbE-phSFgBmZDgWEHqU-oGWECRu3PjB6BCEmBEsWWHpAMaOuNKpnjgExPrxZFEJFPUAdLZQAAbdAZ4WJZgk4vjUvTnVOgC8aF61vgA8AOQAgosQAD4QiwBCa5uLAMKLAHwA3BDAwBAA2iuLADRbu4+HiwC6Gzd3L0cvux+bW7PLarH7vT5Ah5bX4g8GA14vUFPOFfGE7KF3N7UbqdDoQY4QABqJHQAHcIEkAOIkfAACVwDAAXBBgvh8OILIzLvh+sFWgArCytWIAc2AcHgYBAwFsoAgAH1FUrlUqIABNMi4TAQA5kSoQWlYHIqk2KiDS2xjGY1Hz6eYAFUeAGlJvaCZNqFBrvaPugAB74dAyeLXCjoABuWCxUBjEAA-Ddo7GIMynRB-YHgxAnZ7kwnrk7Hq1ixgbXVKPMAKJ+soVdAO53HY5J5MpiBhyOYWUgBWmlUQe2WdwHQgWVJ9-sWkgOWLuK0AbwglYAjrhCI5HtXPCV3ABfCBRTBkHSLURjJAlUKOZwUEWWYAEEiOCyLS0pCAlUepabXahb9A7lWq7rvMpbeOWFBLKsxyPLcqxvE29x-n6274EBa6OKBsy2hWdyfOi+FHDBXxIuiYIAiRGJov8EJkbC5G0cCCKwhRtxoqRNHwtRGLwYhyGoehIFgXMdoEfsqyEScsHfMiDHwqR3GsXRMmvEpTHsSibE8RinGojp2kITB-EAWhK4YVhZYLAwZBkM4UjEdcUTrmOjz4Jg5isW55iPE5z7oIZSFQP+gFmUJ2EQfMHZYA5AVgFiYByhOyoQAAYlqWRYBAADKgYcr2SXyuaMqgNQBJZaEmA5EwmrahYtmPpQnIsmyHJcsAPKXgKQqiuKCDAJEpJYKVRIkuSdXlL4TWsuynLcryXXCpgYoSsA40NRQFjDQAsrEOQHFeN53lNLWze182CotIpSjKQA)

```ts
type Permutation<T, K=T> =
    [T] extends [never]
      ? []
      : K extends K
        ? [K, ...Permutation<Exclude<T, K>>]
        : never

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type cases = [
  Expect<Equal<Permutation<'A'>, ['A']>>,
  Expect<Equal<Permutation<'A' | 'B' | 'C'>, ['A', 'B', 'C'] | ['A', 'C', 'B'] | ['B', 'A', 'C'] | ['B', 'C', 'A'] | ['C', 'A', 'B'] | ['C', 'B', 'A']>>,
  Expect<Equal<Permutation<'B' | 'A' | 'C'>, ['A', 'B', 'C'] | ['A', 'C', 'B'] | ['B', 'A', 'C'] | ['B', 'C', 'A'] | ['C', 'A', 'B'] | ['C', 'B', 'A']>>,
  Expect<Equal<Permutation<boolean>, [false, true] | [true, false]>>,
  Expect<Equal<Permutation<never>, []>>,
]
```

와...진짜 모르겠다