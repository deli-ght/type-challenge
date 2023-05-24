# 20230524

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBBMAMEFoIAUBOB7AtgSwM4FMA6AQwBtTJEFqbKAjATwgEEA7AFwAt1WmAxAK4QAFAAFiHAGYCAlBADEmfABNsAzAuKpUxJvIAOGHATCV55iAEUB+XO2w9TUACoN9+CFw-TWAY3s8EAAGaFh4+MzkQZ6cxOwQxL6++PrsuAmsCdq6EOiSKEbhADLYANYe6HQAVvj+uAA0MR6o+OwCqKzYrADmEABuZDYQuNwCpMoQdB4hhQQAPM4AfNEA7pz4LcHO0XhNEC246KR9Kvu2Y-FaOgyETsFBQWmUvjx2EIZhBACMEAC8BZ8iAcjidhABmGQAbmer3iH2M+GgfwgABZoNCoC9WG94eEwcjWPgVgCEXM7Kgut1FsJhMDjvhGi0av45L9FhAAN6UKAEdjObBKdACdi02wghkQL6wWCNADkknQ6FlUMoAF8VZRgMAIPgAB7ufyndjoSbTUKkgDarHUU1QjTRjXJlIAussYdi4cjzeFIqRhBbcd9GoHEcHZvgwc6EuksXYZJQHkE7uyAGrYIm5TIAcWw7AAEgI6AAuCCcdjsfS4ItatK+TiEKq4QjoVDdYBwMAgYCmUAQAD6A8HQ8HEAAmkLUBAAMLoZQePMbDzD5cDiBdnvaue+UhabwCPwBTLegi+hY63XsfCsZTpCQMC2u4QDUg2KtnYjKHikJgWwh-5zOjIRZgFqUAkuEcwchAFoANIQF0EDlAweQQABJbOLBUZ6pe17pMe+BzF0kgbBAABK7IAPxkRA6GYRAqqLNCYBbjumw+P4DhHuGp7OOeOE3hk96Ps+r4li0H5fj+f6EABQHgfMXJQBaSHwZkSEoWhLArMQuYqAsyn4AwrpgAxpggSA-YrsOqG2PEU7EAQ6RWdZ64CvoLbxOwbgeFBACiACOAhkI0vn6rU8SqhAkhGBAsqiF57gIHWZCkFe3S2MAwrYKQuCyqYsZwtx5DOLZPz-Phvr+l8jTQI0kbRhABXxgV7xFaQJV2Ei5VtVVNWNPhhB0qCEJRg5jWws1sKtYCvodew+LdTN5C9TA-XhoNYr0uCMiAWALUhrNtkol6bVzMw2QMHM1qYLaEAAD7yQR122osr0rbVECRvGYAJR4vgObYyIWpQoUGuwcwBUFpBzL9KEHcVpVrYCcwWtVq2fa6r31CDYX+BDgVkDD3lw21c0ffhKNox9z0bJjizY1AoPhfjUNE+4JNLe1tlgkjlo03aED840-N0wzEBM3jkOE7D+Tw1zdgorzEH8w+r302Azo9hZzlDhAgioF4k4AMqXpWlk632a7dqAlDskbsSbMh7TDEcWWvCWZYVlWNa4HWDZNi2bZwMAEi4CsGy2xAaYZocL6Hm+nuVtWwC1vWjbNq27awMAsdu9ikcALIth4U6xOQaW2B75ZJz7fvp4HnbdkAA)

```ts
// 오답 ❌
declare function PromiseAll<T extends any[]>(
  values: readonly [...T]
): Promise<{ [K in keyof T]: T[K] extends Promise<infer R> ? R : T[K] }>;

// 정답 ✅
declare function PromiseAll<T extends any[]>(
  values: readonly [...T]
): Promise<{
  [key in keyof T]: Awaited<T[key]>;
}>;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

const promiseAllTest1 = PromiseAll([1, 2, 3] as const);
const promiseAllTest2 = PromiseAll([1, 2, Promise.resolve(3)] as const);
const promiseAllTest3 = PromiseAll([1, 2, Promise.resolve(3)]);
const promiseAllTest4 = PromiseAll<Array<number | Promise<number>>>([1, 2, 3]);

type cases = [
  Expect<Equal<typeof promiseAllTest1, Promise<[1, 2, 3]>>>,
  Expect<Equal<typeof promiseAllTest2, Promise<[1, 2, number]>>>,
  Expect<Equal<typeof promiseAllTest3, Promise<[number, number, number]>>>,
  Expect<Equal<typeof promiseAllTest4, Promise<number[]>>>
];
```

### Awaited

https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-5.html#the-awaited-type-and-promise-improvements

> the way that they recursively unwrap Promises.

내부 리턴값(then으로 반환된 값)이 Promise 객체인 경우가 없도록, 최종적인 결과 타입값을 return 해준다.
