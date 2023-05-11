# 20230511

## [문제](https://www.typescriptlang.org/play?ssl=36&ssc=2&pln=21&pc=1#code/PQKgUABBDM0IwCYIFoIAUCGAnDBbApgC75YDOkKyV1FARgJ4S4CWAJgPZbMBe+LEACgACLDl14sAlBADE+DKUYzmAOwBmJWYQCuABwA2+WbW3N9hZKrAUZtiAEVt+UoWbsV1qAElcBvvhVCCEIACyMTMwtVdGw8IhJSAB4AFQA+CABzAJJmAGMIAHdmUPZtIO1SVQyIYoA6TwgAMU4IfAAPPD8ALgaAA37Ccihc9xcINXZ2CABeQWwMuC6IFy4VDIAaCHmEJZVtXFoSSSWAN3Y2GfSAbwBfBsJ6XSNG7RVc13dMHFxSZMejWYAWXoXzixDIiQeT3YanGk3SwGAEAA2vNFstCKsNlssBkdhA9gcSABdCj9XoNdIANWY+AKEHcEAA4sUABLaWhLEKEQi6UhdRGDXIhWoAK1ItU4GWAsEQYBAwGsoAgAH01eqNeqIABNUpYCAAYXYrCMrJIRk1lrVEAV1ihRmBoII4KSyVabWIKlYpEEtT9835WxU9GRxOk03SGGD6VmTviELSSpAqqtmogyWcQQNCmcKdTWttzF8nCC9ogVwgAFEAI7aDD6TaVtpPd4QG7jLDsXAQADkQntyGF9cMa2cwDKZlIPesIxUYwmU1mAjRSxWVU2212+0OWGOEDOFwj5bus7GtGwMzmuPRtEmhijG9x+IrGCWPYAgj223uD6xLsewFPIJz24S8BB-c4-yPW47X+CBchzH1ZmRCgmxbQhEhrOt9ESR1YmdBJIX+GE4XYVJNmRNc1k2Qkd2JVJyNQ5t8HeTDa3rXCQXw+MkntEjzywciUVvdh7xUTYXzfT823oxioDQliMKwji8O+HiiOhWEQKE0MGPWMBSTAZV8w1JptCwUJNAAZWIPk8xMm1FVACh0iskJsCMeg9WWUSJ1GLkeT5AVgCFEVxUlXEZXgBBgCjUgChIFyIBpOkfP0Py5wC3l+UFUhhTFCUpSixBgFIXyPjnJLAU4IwDXc-QRyyQNuWy4LQoKiKMnlRUgA)

```ts
/* _____________ Your Code Here _____________ */

type MyParameters<T extends (...args: any[]) => any> = Parameters<T>;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

const foo = (arg1: string, arg2: number): void => {};
const bar = (arg1: boolean, arg2: { a: "A" }): void => {};
const baz = (): void => {};

type cases = [
  Expect<Equal<MyParameters<typeof foo>, [string, number]>>,
  Expect<Equal<MyParameters<typeof bar>, [boolean, { a: "A" }]>>,
  Expect<Equal<MyParameters<typeof baz>, []>>
];
```

있는 utility 타입을 활용하는 것도 좋지만, 유틸리티 타입 없이 만드는 방법도 생각해보기!

```ts
type MyParameters<T extends (...args: any[]) => unknown> = T extends (
  ...unknown: infer U
) => unknown
  ? U
  : false;
```
