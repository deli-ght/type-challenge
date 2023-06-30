# 20230630

## [문제](https://www.typescriptlang.org/play?ssl=35&ssc=2&pln=23&pc=1#code/PQKgUABBBMBsAc8IFoIGUAuBDAThgzgOoCWGAFpCstTZQEYCeEAVsVgHYDm+ZHEAFAAFWHbr3YBbAKbYAlBADE0gCbEArhMUYpEgA4AbLNuT7SUnFn1hKC2xACKaqfgzEA9u2tQAknv06pdgwIAANMXAIScgAeABUAGggAVQA+EIgAdzJiAGMyCGwAa2cCjLcIKQAPLBzglxxiLgKGXRKOZQgcGTUcdnxMshlBnFDY9JcI-ozSfJCkkK8IADE3EaqsPylFkJ2MFuccht0MSj3WiCwIAF50bDwiGeiAciw6HKfEl-eUiGBgCsqrVqUg6GHKdCkEAAZpZ8FsoGdIXRrrdJlEyM9Xu9Pq8nj8-gCgdpQeDIRgcE5TvsIDkUeF7ujMW8PhAXm9lHjfv8qkSQQVSdDYfDQjtFj8AGrEKQZCAeCAAcVIAAk1HQAFwQMgYDC6fBqv4EPIAOmY+CNq04wDgiDAIGA1lAEAA+i7XW7XRAAJpuHoQADCbmUkKV5kh7vDLogdusiNRDMesQB2nYyn69UanESSSTgVTEHTXB+N0TVWTeZCABIAN5JAC+1caUPMEAAQrX0gB+AoUyEamH6OFgR0R8MQWLOYJ+rBw-oj91R+3EPSrYKxqsQACiAEc1JZEhvAVJahBa9CcG5NE9BIjkHlLP4uM5gGpXAOnjHqTlpyUbgBtSgHkS0Tbru+jRPSkSPGy2KsjUeKJP2cIpCk8QAYetTATuljgXckExNBLJsvB3ZOMhqFQIBR4YJhoE4WiUFYoRjEoSRUhkWhQEgdhEEPPhjE4uyxGIWxKEcVRNHcbhvEYgRnzEeSpGiRR6HUVxYE8YysmsqyLHCexymcVh6lSZphHyT27EALoOiAzpzh6Sw9OQzaYFIup2fZToLkO4BQD8aC8F0EAMD6Iz4G4+gvu4fQalqOp6ga+DGqa5o4Ja1rwMAHD4Bk5iUBKUoyuFkWuB4eqatqur6sAhpkCaZoWlaCCZcVUVlflEAALKrJCfq8PoD6cM4sWVQlNVJXVKUWra9pAA)

```ts
type StartsWith<T extends string, U extends string> = T extends `${U}${infer B}`
  ? true
  : false;
/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<StartsWith<"abc", "ac">, false>>,
  Expect<Equal<StartsWith<"abc", "ab">, true>>,
  Expect<Equal<StartsWith<"abc", "abc">, true>>,
  Expect<Equal<StartsWith<"abc", "abcd">, false>>,
  Expect<Equal<StartsWith<"abc", "">, true>>,
  Expect<Equal<StartsWith<"abc", " ">, false>>,
  Expect<Equal<StartsWith<"", "">, true>>
];
```

첨에 엄청 분기로 많이 내면서 고민했는데, 저번 % 생각해보니 그대로 extends로 걸러주면 되겠다는 생각이 들어서 적용하니깐 동작함
