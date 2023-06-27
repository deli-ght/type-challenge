# 20230627

## [문제](https://www.typescriptlang.org/play?ssl=68&ssc=2&pln=35&pc=1#code/PQKgUABBCMCcDsAOCBaCAFApgJwMaYDsAXAQwHNMMTsBnHSVFJ5hgIwE8IBlHgCwFcSASzixYEABQABHlwHDRsAJQQAxAFtMAEyH91aopnUAHADYlDKU0MPYSpsA1XOIARX6YaRIQHsCjqABJE1MjQiIMHHxickx0ajpsAB4AFQhMAA9DAi0aCC9sIQIyAD4AOgYAQVxcH2wdYogiHybeSgADYAA9CQAdAGoAH16UJQB+Pq0Qcb6AUnGAEmB2iGxMMn5zQqJOZoh1C1xeCDSSHIgKCKJeNcoDoiPPCoYUtvyibH5cIn41-N4fJstBBWJgAFwQADa7TM-DydX2RTh7QANBB2gQ9KDsKj0fwCDZ2gBdBiBABmEBslLyBB8EVwJGMPzWWjR10oWkwZJImwiQjyZ3SJh270KxWeUAAYgjMiQQuCAuj2u0iDQGDtjJR0FwPkUyNAIABeCAAchN6vYmowOrFZAATEbTf1EABWWbmqAarU2vUAZkdJpQrvdFqt2t1xQALAHgx6mpbvRGyC6Yy7zaHKAAlA3GrB4cKxeK0HBJcO26AlCDAYDpDKa77aKFmtHN00mkmehMQTMO3NRAsUIuJUs+4p2yvV2v1wzAyEAIn6c7Rc9dS4gc9mc478atmf9ffzMUHCRLZb9E5rmWnjfnKDXK5d9832693ejB+ipGPxeSZ6jF6nTAG1nOd71XZdnwzbsUw-Ac4hPX9R2TACryAmcoVA5dwPXLcGGVdpFUrAA1IRMAAdwgPwIAAcRsAAJfhWAhXgiCIYwaDBatVSOMoACsaDKOoyGAOAkDAEBgEcUAIAAfTk+SFPkiAAE1AWwCAAGEfE5CA6JwShFMMuSIAkxxXzzT9CwQpJKlrbJclFPVK2NWzMnsvJ2gWABvIoyRwCAACEAF9vN8-yNKClYxkCuzCAciQTX6E0IEGU0UBNFRoshAK0TKPKJA02Kcg80KCD89SABEgtmKKoQqlt3SJCAIUhDSW3bFQmpa1s8rKCRPK84LvIilY3LikqfLK-yqpqiAsvq01GuaqEBqGryRvaoklC6psTXazapJAWSjMUk5PAiDSSDoPITtO0yhBMOori7LyIAAUQAR0EUw0Teus0IgIKIDJbAfH0E0pC9FAjnsUJik8YB+G8UwaHTV9LroAAGR1IVbPH2zAdGrswHMmyS-a2xJIm6F7Mm9tNaB6bNKmuwxzB9zpltoExzGmYJ6nMHfTmGZ5pnGsJ1niZg3audFhr+clugADYccDJnud5+WWatNn4FV9LZc1ymJZ14nkGNXGDYZvntcoNnxAt-GtZNu3ie51X1Ztl3NLd0ncfVuXjbAWoCC8CASAhCy4KHEsTQ191nJlkWjZNcXvYZa6cYYP7pyST7vtLfsj3gn8kjNEo0TZzGSgr7P-u+POvvsQvDy-Evh0Sk0K59ugK1rqAc7QxuC6j4uY+SRLGe7tnx379766IYfm9Htvx7L-oNa7yvid9GuUTr3P8+XovV+syeeYT7e6EjPeD6Ho-TBbyzvw7+Ot57zAXVvgeF6Xx+V6sqXQMb9p7EyVt-eeh8m7-xPoAjuKBN6gLoPACBg8G4PyftHM+CD35s0QKg3+GCAEv1jpfD+sACFQJHrAkhE8p5XxJtXOeaDF5EJoe3WOiCGHQD7vvEkYBpK3QUhASUvx2TqR1Jgdix0hEyRMpJUADBKxyGoJQdgal8g+FMEjXwodmKsXYpxYA3FeB8QEkJESCBEDADODQMi9AoDEVIhRGgWidF+A4hAFibEOJcRoDxfiglsDCVEtY1x2jvAeKURAAAsnUO2vBYaEAoJ47xhi-EBPMcE8SkkgA)

```ts
type PercentageParser<A extends string> = A extends `${infer B}${infer C}`
  ? B extends "+" | "-"
    ? [B, ...(C extends `${infer D}%` ? [D, "%"] : [C, ""])]
    : ["", ...(`${B}${C}` extends `${infer D}%` ? [D, "%"] : [`${B}${C}`, ""])]
  : ["", "", ""];

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type Case0 = ["", "", ""];
type Case1 = ["+", "", ""];
type Case2 = ["+", "1", ""];
type Case3 = ["+", "100", ""];
type Case4 = ["+", "100", "%"];
type Case5 = ["", "100", "%"];
type Case6 = ["-", "100", "%"];
type Case7 = ["-", "100", ""];
type Case8 = ["-", "1", ""];
type Case9 = ["", "", "%"];
type Case10 = ["", "1", ""];
type Case11 = ["", "100", ""];

const a: PercentageParser<"100%"> = ["", "100", "%"];

type cases = [
  Expect<Equal<PercentageParser<"">, Case0>>,
  Expect<Equal<PercentageParser<"+">, Case1>>,
  Expect<Equal<PercentageParser<"+1">, Case2>>,
  Expect<Equal<PercentageParser<"+100">, Case3>>,
  Expect<Equal<PercentageParser<"+100%">, Case4>>,
  Expect<Equal<PercentageParser<"100%">, Case5>>,
  Expect<Equal<PercentageParser<"-100%">, Case6>>,
  Expect<Equal<PercentageParser<"-100">, Case7>>,
  Expect<Equal<PercentageParser<"-1">, Case8>>,
  Expect<Equal<PercentageParser<"%">, Case9>>,
  Expect<Equal<PercentageParser<"1">, Case10>>,
  Expect<Equal<PercentageParser<"100">, Case11>>
];
```

왕,, 문제 풀이 짱더럽다..

```ts
type PercentageParser<S extends string> = S extends `${infer A}${infer B}`
  ? S extends `${infer A}%`
    ? A extends `+${infer B}`
      ? ["+", B, "%"]
      : A extends `-${infer B}`
      ? ["-", B, "%"]
      : ["", A, "%"]
    : [A, B, ""]
  : [S, "", ""];
```

```ts
// your answers
type PercentageParser<A extends string> = A extends `${infer L}${infer R}`
  ? L extends "+" | "-"
    ? R extends `${infer N}%`
      ? [L, N, "%"]
      : [L, R, ""]
    : A extends `${infer N}%`
    ? ["", N, "%"]
    : ["", A, ""]
  : ["", "", ""];
```

L, R로 나눠서 풀기
