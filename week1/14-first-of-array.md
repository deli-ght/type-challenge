# 20230428

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCMAsEFoIDECWAnAzgFwgewDMIBBddAQwE9JEE76aAjSkgO2wAs9WXkBXCAAoAAuXYE+ASggBiAKblMLGeTJUwNGVogBFPnJypuGqAEkAtgAcANnPNz2EchADmDuelQBjCAAM0WNgAPAAqAHy+EJzkuNjkANYGTqwkaiy+IZFiACYQ6HLYfOismBCo2KUEGDgQcrb27ADkpdiUlnIAdCYoeOi1AB7kVrYAXN2+ExU0re1OZNAQALwQANqN5I0ANBCNjFs7Xo0AutNtcnPoAExLqwDM25fb0CensxwK2QvLAThBqujQMIQYDAAbtLzYOS5bB4CCMc7rRqvc7vcjZa7farBf6XIEgsFyCFQqKw+EQW40Ca+bpAgBqqDkAHd8CkAOLlAASfEYIwgHGw2EsmBGIIqXg4HQAVpgOr0XMA4GAQMANKAIAB9TVa7VaiAATTwRQgAGE8NlzhyPOcdTbNRBlRoZucfsEQgNIaxsqUxJQVkcgcs3XJ+h6vatUKwCB4SNsOnGI1G+vkcEcIAB+EgQXmsOQANw8qpAGttOogIQMuGNiiSJdLDtQVl6sTOEAA3hAAKIARz45Gs2w7-XBuAAvhACOg8OYdsInQhxX3bKw3JhgHxsKhrJgkWAnRAvNXSssVjRB8Ogt3e9Ygi6git7hBHjB-dtbmEwptT0PCcFL32b1id6CNIixAtAlwPu25C8jgnjLhAI4vkIIFgRB76flAZ4-hePb-refofhAOb5ug6Ffuef7XvhfCenIVQ5tkSE0ea9FQmRLx7h4k5YDcJ5QPis6YAgwbDsJZC9DQt6NKweDYKQFCUI0H40AJFTCd+EJidxkmAe2AAMvLrGkAAyqCJI0CHKS8aq1tqKBFJw0YAMqQkKxa2eq9oqqANBAk5HCqOclCGn0mB4NY65GCUvL8oKwqipg4pSjKcoKrAwBiJgjIFlAdIMsyYURRu3DCnyApCiKwBihK0qyug8pwMAhWRSVvkQAAsr05zGgF1hLiuMXlfFVWJTVKX1UqKpAA)

```ts
/* _____________ Your Code Here _____________ */

type First<T extends any[]> = T extends [] ? never : T[0];

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<First<[3, 2, 1]>, 3>>,
  Expect<Equal<First<[() => 123, { a: string }]>, () => 123>>,
  Expect<Equal<First<[]>, never>>,
  Expect<Equal<First<[undefined]>, undefined>>
];

type errors = [
  // @ts-expect-error
  First<"notArray">,
  // @ts-expect-error
  First<{ 0: "arrayLike" }>
];

/* _____________ Further Steps _____________ */
/*
  > Share your solutions: https://tsch.js.org/14/answer
  > View solutions: https://tsch.js.org/14/solutions
  > More Challenges: https://tsch.js.org
*/
```

```ts
type First<T extends any[]> = T extends [infer A, ...infer rest] ? A : never;
```

이게 좀 더 정답에 가까운 답 같음.
infer 사용 방법 익혀두기 - https://blog.logrocket.com/understanding-infer-typescript/
