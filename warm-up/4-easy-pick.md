# 20230425

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBAsELQQAoEsDGBrS8491gRgJ4QCCAdgC4AWA9mcQGICuEAFAAICGlAZkwJQQAxAFNOAZ2JCmZZHWH4myADYU4yMmCxCdEAIpMR4inM1YAkgFsADspGWRlCNRERFKtRogADFBgA8ACoANBAA0gB83hAA5o4iAE5oEADuyNQ0TBQQTOIaMRDpAHRaUADCdMYJTKgU4hCczoTWrkQQ1mjo+c5UruIi2TQ87Qk0LQkmRj5h0Tyjlj6B3qUQDDQJECIAHpw2dgBcK97HdVgaFIk8nKiugTQAJjQQAN5YUCYUBxBV+W8Q90ZUElrCY6PtvhQkmQYn9UDQ9gMRPdwfgaDQ7NwsABfFYUZq3B40RAJEQAN2QIhSEAAvBAALKEPzoIKE0IAcg+djZEAAPhA2XCERd7myIis4WRjM5CeC7o9iWSKVTaa8oGrnOkvmyyhiyBBRvC2cE-lBBbZEciIFdlP1jVAcVBjsssBEIAA1JUQeQAcXSAAkmPhwVQKBRrOJ9sBgHVUFQigArcRFdYxYDQMAgYBaUAQAD6+YLhYLEAAmpkNhUARA-YlXEX6-mIJmtHiWvTGZ0gqFIjSGvRsyA8w2ixBAkZsmUJFNhyPm8gbOtsq3XM8IABRACOTE4ylCa62LVqECxVvm-PYy7gsZ3dmhRmAWRU4jZLfxEFQU-qtIA2lh94eKH8Tdt2UICDxEWokQARlCBkmRZR52U5ERRQiCI7XXcDaiArcdzAgCkQAJlgjsAjlGgkM1FDeX5M07GFVD0KwKMIAvcQ4G2ACOISUYEiwODO3IyjPmovkBXhc0GJotkNFJHdkBFJiAF0tHOS5rgJR4XiwZDwR+aEsABcQgWQEFTD0yFflNCT6KRFE0V1MAcTANSEiuG5MII+4oO094qIsqEYWc1z3Ncf8IOFQjfI1ESAqs98bItez0TETRnJzGdC1WJgJl6DYAGULnDIdMtzJss1AF0IHyqhOBJCBCHLb50UfSpg1DcNI2jYy40TZMElTaBgG4cQUkSKqPUpZrlFayV2rDCMoxjXqkxTNNgHEFrQUlKq6XWVwylq5RbziCMIBDBauuWhNVoGjMsyAA)

Pick을 사용하지 않고 Pick 구현하기

```typescript
/* _____________ Your Code Here _____________ */

type MyPick<T, K extends keyof T> = { [k in K]: T[k] };

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<Expected1, MyPick<Todo, "title">>>,
  Expect<Equal<Expected2, MyPick<Todo, "title" | "completed">>>,
  // @ts-expect-error
  MyPick<Todo, "title" | "completed" | "invalid">
];

interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

interface Expected1 {
  title: string;
}

interface Expected2 {
  title: string;
  completed: boolean;
}
```
