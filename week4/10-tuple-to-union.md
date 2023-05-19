# 20230518

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCMAMEFoIBUCuAHANgUwgFwHsIBVAOwEsDTJEE76aAjATwgEFS8ALK1gMVQQAFAAEAhpwBmqAJQQAxAFtsAE3KpFC8qUnYATgrwYcC1BSpga86xACKqbAGc8lajQCSirNmWcIYiABzbFJ9cgBjCAADNG9kAjJXAB5kAD4oiAB3LgiuCHCCADd9R3wuXEKxTAdSgkl-fGNcQghyPFLK6qcIM1cAOksoPgIDbAAPMS8cQeioqPaaPGZ0XDY9AwBeCABtAHJoXYAaCF2AJiOTgGZdgF0ZpZWUJzwILdiceMSqJLW9VIhgMAIOMVuE8Kp8ERGLh9rsIAAfE7nBFXXY0OZRGb-ABq5GwmQgVAgAHE2gAJVCMABcEC4eDw6EcVMB7XCXD6ACtHH0RoFgHAwCBgJZQBAAPoSyVSyUQACaBFQBgAwgQVLgyfpcNLtRKIELLA9cO9sJ9zKQUsCxuDSCpSmYANakAiZUjbG7-N7bUgaaF6O5gUU67VPZwQJViRzdIPSvXC8heEYvQ0QADeEAAogBHVBVY7psagl4AXwgkj0BE0uxEhoQbKqOFIwUcwFQLkwjjRYGT4Qj3S22xo+cLSSzOcwKSapuS22gp0ux12ABYAKwANgueD0Dndx1nlxRS7XcMRm4cqVSh0HBewYJH2aqE7iCTNSRnc53MDn58v-sD0ZlAh6Nw+gQAAyuCjLiv+ur6qAND-KBXBiHouDMAqBiOAQ1QuFQTK0vSjLMsArLslyPJ6HycDABIjiZPo8EQLi+IQJh2GuHhdIMkyLKOGynLcry-KwMArGtuxDEALIjLgSpIZgDZNjSnGETxfFkbygrCkAA)

```ts
type TupleToUnion<T extends unknown[]> = T[number];

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<TupleToUnion<[123, "456", true]>, 123 | "456" | true>>,
  Expect<Equal<TupleToUnion<[123]>, 123>>
];
```
