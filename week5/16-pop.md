# 20230523

## [문제](https://www.typescriptlang.org/play?ssl=38&ssc=2&pln=28&pc=1#code/PQKgUABBCMBsEFoIAUD2AHSiE91gRgJ4QCCAdgC4AWqZxAYgK4QAUAAgIaUBmjAlBADEAWwCmAEwCWjYUI4AneR0Jgsg9RACKjUQGcKk2qqgA+CABVC6UQGUAxvMnoKEACwA6AAwRJuiPNE7VGExMnEJHzIIal8IOyoOABtE0TIAc1FjCABJYXQU0JcOCAyyUUc7CAADNHQAHnMTKuiElwoOAGs9CC5SRWVq82aucX9RCkZ5Mj9ekn7iAHdJalRGF2WAcj9Ejn0IUQLUincs+lR5fYAPDjyUrKqHil0sCitRHsVoCABeCABtDYcDYAGggG3wILBdkhG3EGwAui83h95AAmH7-ADMoNRoOgiKR1jGX1+tTqCnk0DMwGAV2sdgoEQoqAg+HeAKBoPBMOhiKgryJAXRpIw5MUqOptNEl3pjNGzNZ7OxEFRfOqDyyIBAAFFLhQlFqAFwQGySYSSHbyRKEUF2XqEVY+W6iQrVGxUSTcChVUE1Ri6KjDMLVACq0w9XuGfgWB0SAH4smYAGqSUQLCC0CAAcWWAAlGPhjVQKBR0LpDTSnvF3AArXTuc5pYBwMAgYCqUAQAD6Pd7fd7EAAmqsLgBhVDhCC58rvftznsQNuqAXvMnmK6MsIzOh-eFmX7r6Wb8R+P7uc+SMjccooUGX68XAAy8Igcf+5-cyBfxt3HZA3fnfsLD0FxR12bpAKApczXQc42mRABvCBtQAR0YJJQV1WUIAAXwgbh5GCME2BXBB4iSFJ0j0YA1gtXQNmXZE7V0bpfj+LAsMCCg6lQ9DEjqMk-mVXEYD3UEhJxPcTGBDiZS4ni0KSATRQ5GEIS5aEuThMT-kBNSeQRExpNk2UFL45T6l3aT-ikmSCU7SC+wgJh5GoG8bEZMsAMcrtF3bUAsDMd0FHeB1JggXRUESWjaHLCBi1LctK10as6wbeQmzgYAuF0GN5ECiAUzTCKopi6YixLMsK2AKsqFretG2bWBgEi6KDFigqAFlzneUcEmSVIMjihKquS1KGoy1t2yAA)

```ts
type Pop<T extends any[]> = T extends [...infer P, infer L] ? [...P] : [];

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<Pop<[3, 2, 1]>, [3, 2]>>,
  Expect<Equal<Pop<["a", "b", "c", "d"]>, ["a", "b", "c"]>>,
  Expect<Equal<Pop<[]>, []>>
];
```

infer 학습하기 좋은 문제인 것 같다.

## 추가 문제

> **Extra**: Similarly, can you implement `Shift`, `Push` and `Unshift` as well?

### Shift

```ts
type Shift<T extends any[], P> = [P, ...T];
```

### Push

```ts
type Push<T extends any[], P> = [P, ...T];
```

### Unshift

```ts
type Unshift<T extends any[]> = T extends [infer F, ...infer P] ? [...P] : [];
```
