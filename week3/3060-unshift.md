# 20230510

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBDMAMBssIFoIFUB2BnAFgSwDMAXSFZci0gIwE8IArPAQwwHNcWIAKAAUZfY4WAWwCmRJgEoIAYlFMsdGUwBOKpjTCkZOiAEUArqKxE8AewxaoASWEAHADaixGIhCI5R7mna8A3URUscwwIMwIIAANogEE1DQA6A2x8YmjIqwgAMTMVCFEADyZ7JwAuTPSiH2MAYxU8OxIoKt8IACVjAwc3AF50FMIiAB4AbQBGABoIACYAXSnYAD4IYGAIEdgpyZmJ2dJ0zOWANTxRAHcw0IBxPCIACQMqUogcIiI7LFLVoiwanAT6FgErlWMA4IgwCBgFpQBAAPoIxFIxEQACaZgMeQAwmYACZeO6BLzIkkIiBQrQtLyYXCDIYAFXyBSIogwuKwEGSAGsMGYzhgRvN0Ms+iM0FMEpL6XswLDSSSIPTjG4sQpjPD5UjydC8PZcm4qRAAN4QACiAEcDEwHFNTQVfDU3ABfCAEFRmYQQADkPCpyD+1qcbGMwAMpgcWC9lOqEBqao5otIdodwwtVocQxpqWGgq2iym41mi3zSftokdQzT1szA2Io22cwW+fWmwgDaLJagyfLqct1azdJGXrGXqm0ymXugXqFVDMZicLGbI1n8-kGAnI7HE6nHYmYBlcs1KKymI8gQgAGUWR8NUe4drZeAoMsL0IVF4aBi8lh52GQp8XjeD4vmAH4-gBIEQTBBBYGAFgsDOQJSGOU4Lh-Bw-wsADXneT5vl+f5AWBFRQXBWD0Mw7BkIgABZXIvCxIQHCDVhjGeHDgPw8CiJBSFoSAA)

```ts
/* _____________ Your Code Here _____________ */

type Unshift<T extends unknown[], U> = [U, ...T];

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<Unshift<[], 1>, [1]>>,
  Expect<Equal<Unshift<[1, 2], 0>, [0, 1, 2]>>,
  Expect<Equal<Unshift<["1", 2, "3"], boolean>, [boolean, "1", 2, "3"]>>
];
```

`readonly` 안붙여도 잘 동작하네..?
