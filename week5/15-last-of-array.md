# 20230522

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCMCsEFoIBkCGBnALhA9gMwgEEAnY1AT0kQRtqoCNyiA7TACx2aYDEBXCABQABVKzy8AlBADEAWwCmAEwCWvWTNSkKYKtL0QAir3lZlnHVAB8EACrkADvIDKAY2LL72ACwA6AAwQyugQxPIuOLIKzIpKgcwQ7EEQLmyoADZp8swA5vIWEACSsvaZUdioELnM8u4uEAAGaFgAPDaW9Qmp2JioANYmEKJEWkz1Nh2iiiHymLzEzMHKmMFpGNjypVmYPvncOMQQ8gAeqMWZ+fWXy1SYDvKDpNAQALwQANoA5KgfADQQH-Rfv8XB8ALo3O4PYgAJhe7wAzH9oX9oOCIY4EqhlGknq8mphmppiNBrMBgIcjo4XJhYpgcBB6PcPiD0fcetjYXi1oTSNDSeTjlSaVM6Qz7tAqJd6vlrAA1ZTyADuuHiAHElgAJXj0ABcEDYmEw9nQOrJyxSPgAVugfPtssA4GAQMAdKAIAB9T1e71eiAATRwcwgAGEcDEIBqavcfTHPRBnTpbhj8a0KTTosFROQ3qDrK8s66QB7Yz7bCZsMGMAMS6WE8pivtupCAN4QACiAEdeOk-m3KWFsABfCB4YgRf5CJPyBApdKZHImYC8TDY9AfROQlxV4KvN5UPtC5qd7tpZopt7Q3NIyyWH77-vUo9d9Jn7lvREQZEwK8wG93qAHgOT4nq+LRvAIUjPNY0DQh+raoHqWDuDkECDj+8GIZgyHZKhf5gGibo1t6EB8MQ7A1BATg0saxZEe68YuqAVDWE4qShBA5CBgc6A4Gky5mAseoGkaJpmugFrWraxD2nAwCiOgio1MxEDykqEA8XxK6cCa+qGsaprAOabBWjadoOrAwAafx2nKQAsvs9zBqkGRZLkOnCfpYkSaZ0lOi6QA)

```ts
type Last<T extends unknown[]> = T extends { length: number }
  ? [never, ...T][T["length"]]
  : never;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<Last<[2]>, 2>>,
  Expect<Equal<Last<[3, 2, 1]>, 1>>,
  Expect<Equal<Last<[() => 123, { a: string }]>, { a: string }>>
];
```

T["length"]까지는 알았는데, 여기서 어떻게 1을 빼야할까 고민했다.
그냥 맨 앞에 요소를 하나 더 추가해서 length 인덱스를 만들어주면 되는거였음

```ts
type Last<T extends unknown[]> = [never, ...T][T["length"]];

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<Last<[2]>, 2>>,
  Expect<Equal<Last<[3, 2, 1]>, 1>>,
  Expect<Equal<Last<[() => 123, { a: string }]>, { a: string }>>
];
```

앞에 extends도 필요없다. 어처피 unknown[]에서 파생되었다는거 자체가 배열이기 때문

```ts
type Last<T extends any[]> = T extends [...infer _, infer L] ? L : never;
```

infer를 이용하는 방법도 있다. infer랑 언제 친해지지
