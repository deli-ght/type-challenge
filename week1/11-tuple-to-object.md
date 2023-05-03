# 20230428

## [문제](https://www.typescriptlang.org/play?ssl=39&ssc=41&pln=20&pc=1#code/PQKgUABBCM0QtBAKgVwA4BsCmEAuB7CAeQCMArLAY10gXnodpIE8IBnASwDt98uIAFAAFOPPgEoIAYiwBDNqyn5yVXPADWWZmzC0p+iAEUUWNrg59dUAOIcAbln6ynAJxezmAGjzuubAGb4LgC2EBy4YVwEEM4QyhTUeMxoOM4AJngAFjiazMB2shgmEMEoZhAkONxZOGgu+HYcaVgZsm4eAHRWEABiQRBYAB6ywZhYAFzdAAYzuDpQlHzluOjYEAC8EADaAOS4phiyO947wfjNGBAAzMcQp+dYlwAat-cXEACaOwC6MWwQiz8NFouGSOBcphQGAim1QYyQ+FICVwAB5QSl8P48KssAA+CDAYADQYpagtCAAbzu+zYhx242pByOJzO7xuDLej2ur1ZXJeHN5zx5D0uXwFIs+OwAvrQZlNuviAGocLAAdzi-FsuAAEigSAzMrhcGg2ONCXNKJkOmQ2B0ggBzYCwMAgYC6UAQAD63p9vp9n3wKBcEAAwg8INqsBCvX7Y56IK7dOicHDsAikaoUUhifsuGl-hDZGk+BhWAIzC5uPaIAAfCBcFDBSoucRbX74zZUrYAaUiyC2DabUd+vwZvZlYA9cdjyFMERD8lMMen-sTHFGQQiycpEAAogBHFCFby7kmqCBSiD+eqhHZCZPwS2FbBce2mYAocwYNg7XSA5Y4hs2x7EywpsmBfIQaKPx-ACSw0P+W44gAco2zZAVs0DeAATN4VzeAALL88hwUCYCIdiYwALIcIMGFYXc2G3PhdwETBJGIUmYIAou-ybFstCnqSqIHkeGBZji6YqNQaJgpilHYLi3hUjShwcqpRwANx3IK3LiuB2mckK+mQYZulijpEpfBeuJKYJZ4yaJhQSfCiLSaiybySsYyoUOLhKTu0AMtA2nYQy2HaVcDJXNpBEMgRNl2VAQmZk54mplgUnIrJGJYt52A0YMAVUkFMCGUxHJMZF0WGWxHJsYlnhgN87pEvebDwEMwmdW4QRgNuUb1MGsKSW52VbJhOHfMpUrfLi7ogMuK7xj0Qa4NkwYAMr7CaS0rgmbqgLQ+KbZkbQ4MwgbBmw+BFOYSwGkaJpmsAFpWjadouI6sDAM4bCqlGx0QMqarsLdn4WH4j3Gqa5psJa1q2g6TrQMAN13ZD8wQPiVFBDgIZnRgL5vqaECGjDL1vYjn32i6bpAA)

```ts
/* _____________ Your Code Here _____________ */

type TupleToObject<T extends readonly (string | number)[]> = {
  [K in T[number]]: K;
};

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

const tuple = ["tesla", "model 3", "model X", "model Y"] as const;
const tupleNumber = [1, 2, 3, 4] as const;
const tupleMix = [1, "2", 3, "4"] as const;

type cases = [
  Expect<
    Equal<
      TupleToObject<typeof tuple>,
      {
        tesla: "tesla";
        "model 3": "model 3";
        "model X": "model X";
        "model Y": "model Y";
      }
    >
  >,
  Expect<Equal<TupleToObject<typeof tupleNumber>, { 1: 1; 2: 2; 3: 3; 4: 4 }>>,
  Expect<
    Equal<TupleToObject<typeof tupleMix>, { 1: 1; "2": "2"; 3: 3; "4": "4" }>
  >
];

// @ts-expect-error
type error = TupleToObject<[[1, 2], {}]>;
```

타입 내부에서 타입 or 연산이 필요한 경우 () 소괄호를 사용해 감싸주기
