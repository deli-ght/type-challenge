# 20230621

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCMAMAsAmCBaCBJAzgOQKYDdcAnSVFci0gIwE8IALASyIHsaBDCRxgLwFcA1pwAUAASasO3fkICUEAMQBbXABNGfJYr4A7Rix3aALowA2mMKQXWIART65MJg5ajolAB1O4VOoxE4jGg9cDBwCYgAaCAB3JgBjeggjdgFHLh0PPn8gkIgAAwAVfIA6UnQAM2T6UNzQliqiRxZTQkxklgKdCKJ86KajPiJDfKMiBz6IFiMaohjGTFD8ivZzXFLXCAAxFiIIXAAPdk9vAC5N-MujCyg6iABBCABeMLxCIgAebveAPihgYD7A4heJGNQdCBUWrjXCkO4AIWerx6H10qlwFUY3VUfwBQJBYNUEKhEBWazhwVCAGEkVg3sQvnxTKZcYDDgTwUZOiSyYsKXkACK08LvD4AbQAuqz8bhQZzuaFebDbpSIABRYX0z46TRQojS9mywnExWrPlQS75TZ-ABqjFwMSmhgA4owjAAJPhUU4MIxGDyYU4A66JEoAK0wJV2AHNgHAkGAQMBLKAIAB9DOZrOZiAATRYQwgVJY6Ig7uIoWzVYzECTljudJRhT+L0KQLBOlU7W+xAgAH5kjCID6lSmQOnq9mIIVHP4qexFu1J1O64xPLscqqAN7qgCOfFW0TVwKNEAAvqTWFoAOSiOooRKrbw6aOOYDZMyYa-11XxBfpF4xVIY8CQ+NV91WD5G1FHt9WiMYHB+H5ImAk9QTAiDTCgkUGVgiAAB8ICcIgsWjZDSTNXAkJQqAQKNDCDyw6CGWva9yKVajUNA8DGOwrVUU7DEsTUdjKM42i0KMBjIOY7UmRZaIOOQrj6J4mScM+SVRLWcT1Uk6SmI0j4tzPbTFk4iUxwnZcay2IYZl7ABlMEA2smza2TUBSD+Rz6HYJoIBoAs9kwFoPwMQNfX9QNg0wUMIyjIhY3jRBgHYHRMBiYhvIgO0HSIsLnAyn16D9AMg2AEN6HDSMYzjBBUtC0xwoynKAFldmpPzmVwF9HBKsqYsquLqoSmNE2TIA)

```ts
type IsNever<T> = T extends never ? true : false

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type cases = [
  Expect<Equal<IsNever<never>, true>>, // ❌ never 자체가 빈값으로 처리되는 듯 
  Expect<Equal<IsNever<never | string>, false>>,
  Expect<Equal<IsNever<''>, false>>,
  Expect<Equal<IsNever<undefined>, false>>,
  Expect<Equal<IsNever<null>, false>>,
  Expect<Equal<IsNever<[]>, false>>,
  Expect<Equal<IsNever<{}>, false>>,
]
```

```ts

type IsNever<T> = [T] extends [never] ? true : false

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type cases = [
  Expect<Equal<IsNever<never>, true>>,
  Expect<Equal<IsNever<never | string>, false>>,
  Expect<Equal<IsNever<''>, false>>,
  Expect<Equal<IsNever<undefined>, false>>,
  Expect<Equal<IsNever<null>, false>>,
  Expect<Equal<IsNever<[]>, false>>,
  Expect<Equal<IsNever<{}>, false>>,
]
```

never 자체가 하나의 타입으로 인식되기 위해선, 배열과 같이 하나의 변수 그 자체로 인정 될 수 있어야 함.