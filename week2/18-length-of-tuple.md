# 20230502

## [문제](https://www.typescriptlang.org/play?ssl=40&ssc=2&pln=23&pc=1#code/PQKgUABBCMAcEFoIBkCmA7A5gFwBYQHsAzCAFQFcAHAG1UkQUafoCMBPCAZwEt0CD0EABQABHnwEBKCAGJUAQ04cZ2KrTD0ZWiAEVyqTtm4CNUAGIEAThEzcAbhgjyIqmqgA0ENgXIR0qVAATCABjSwVsVCcbDFRLbhCIAAM0LDwkz0oEgGsXXCjaNPxiPKjXdXoLa1QAD3kAWzcALlNkpKTsTnpsNkoyg2pnAF4IAG0AckjOQfHPcfqCQNRqCABmWYh5xeWIAA0NraWVgE1xgF1u3qjOSnkQ1F2IEYmzAEFkAGEAeQA5CABOA5vT6-CAACQAoq8AGqnOYAEQASq8AOK-A4AZVIr0RGLBAEkAAoHMEAVQAsq8-hjCa8PhCzMh8SiwaRzq0en0XAN5KkcPgRny8AAeKaDAB8UGAwAgtT6IUiwQALJcuTc7g8hQKUBh+cL1fddpLpbKavLFRAAKz0dpJVqS6HcVAAd0IghR3GwYPILCaEFw2GwlE4TWlnRCuAAdAArTiRqyYYBwMAgYAaUAQAD62ZzuZzEGOPmsH224LiUTzlezEFTGk5US1wtIpsi6ECnAg4XkgQE1A48nQbFGZ0lI1IE0K-PZYAzVcrZAM2AgH0UBizc9zNbT3EaViX9YgAG8IBCAI7keTUTwQs2oBUQAC+ECIlgI9U2InrCAjl8nBmA5BGNQnDjBoIQCIY3LTMMYyTDyBwLEcawIdsKz7HMiE7KcZxOB24HoIYYD4ZBBoPE8sHAt8fyAnMlGgpCMJwpsSKouicxYjieJEiSFJUhANJ0gyTIsmyOGKKEEHYHWVyhKuHbPPQN7msKZ4XtQwqNvWJRivI4qeEq4p6Ypt4Kip56XhpuoilpJCkUaniWoZ7j0Can6cAgcp3tgHmWK+lj0I2jnOVKMpuR5JneXEfkBVZuDCuM+TUNQBAQM6VjUIE4xGRcM4gOuG7VmY5CWHgcT8ZEwb5QVW65fQkoYrg8jhF4RZcAQ1CAcYBF+gGQYhmGnARjGcYJkmsDAAOnDOnEdUQI6LptR1RgQT1gbBqGwDhlGsbxpYiZwMAnDtZ1EGzeSVhRB8jVJbqBirX1G1bcNu2YCmaZAA)

```ts
/* _____________ Your Code Here _____________ */

type Length<T extends readonly any[]> = T["length"];

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

const tesla = ["tesla", "model 3", "model X", "model Y"] as const;
const spaceX = [
  "FALCON 9",
  "FALCON HEAVY",
  "DRAGON",
  "STARSHIP",
  "HUMAN SPACEFLIGHT",
] as const;

type cases = [
  Expect<Equal<Length<typeof tesla>, 4>>,
  Expect<Equal<Length<typeof spaceX>, 5>>,
  // @ts-expect-error
  Length<5>,
  // @ts-expect-error
  Length<"hello world">
];
```

- 해당 프로퍼티에 대한 타입을 가져오기 위해선, 타입을 **객체**로 바라보기
- readonly를 붙이지 않고 array로 취급하면 에러가 난다.
  - why? 배열의 길이가 수정되면 안됨

다른 해답

```ts
type Length<T extends any> = T extends { length: infer R } ? R : never;
```

infer를 이용해 **포함하고 있는 값**을 타입으로 사용하기
