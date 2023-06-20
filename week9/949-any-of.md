# 20230620

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCcAs0QLQQIIDsCeB5AZpJihR+ARhhGgK4A21EAFAAIDWGaApjpcwJQQDEAW3YATAJaVBAgIYAnWdIxh8-VRACKldgGcALmID2aZVACSggA7V2wtLogAFDLoAWRiNTHNREAAbTMXwguNABjfXcxNAhXdhiMCzjtDD0bADpUeMSY6W9tGJc4lHlFCACRCFl2XUpZNHzfXVktILEcMswIdmtbewN22NQS8jF8pq0M0wHCoYUR-JsLXQwAGkrq2ujfHGlqbXZfNJMIADEDWS6AD2lLawAuY98n3W18ZeyAZRurdgBGCAAvKhMLgADwAbV+awA5NC1js9uw1uCALprADeAF8UQA+CDAYBXRLhHy6AwQEhxcbsI5Qd5xL63dgAJkBwOwOAhAAYYXDgrt9si0RAsbj8YT2JdibpSeTKfzEbS-E9jniAGpidgAdwg7gA4mJdAAJSgkO4QFy6XQWbR3AkvUIuNIAK20aXOAHNgHBoGAQMBlKAIAB9UNh8NhiAATQMtQgAGEDCI4kb2FUQxHM8GIP7lPT2WCACpXGVoET5KrSERGajkAIYVF4oH1wMgDNZ8MQQs6ezx6T7fIdiM5gNiSznez59EQACiAEdKLs1jOpexwhBMcFZAYpNDGPTEI7dtY0B6dMBKPo9tC8wk4qF+zo2eD8CvpaD54vqKD0ByIVCIGhGU9D5alkV+YVpzQG52HNICe2hDcMQgX44OA3REOxHE1mpHFsNfVdwg-Bddh-EFOUhXl4QFJEIFRDEsJw5p2DwlYCPfT9SN-MFwR5QD0L5BFBToyDGJiZjWPYtddGIr8yL-XiqPErQhQY3EmK0SSoDfaTZK48juSUoTaMhUT1OUlj8O0wiZM479uIovjYWoxFVJFCgYLQhCN3M3CrNnGy9PsgzFMAwSaLc6dUP47yxL8tjrI4kjgoUpzwtckTkOg4QvJApD3Oi+C8riiT-J0oi7Pkni0pc4T6JFTE1koMtOCiUQ1ioWhzOMrSAqSuSHIhbqaMklFW3bIdsxOWpYguD4ZRtCahxHMBQHwPEPhcOQ4gwWMLm0AxqEvQx6nNS1rVte1tEdF03U9b14GAAJtC1NN1ogDVtQgA6joiU6LStG07WAB0nVdd1ZC9H1gB+46jFeKA8QAWXOOJ4y22h2FPHQzsBy6QeusG7shv0AyAA)

```ts
type Falsy = 0 | [] | false | '' | undefined | null | {[key : string| number ] : never}

type AnyOf<T extends readonly any[]> = T extends [infer A, ...infer B] ? A extends Falsy ? AnyOf<B extends readonly any[] ? B : []> : true : false

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

const a : AnyOf<[0, '', false, [], {}, undefined, null]> = false

type cases = [
  Expect<Equal<AnyOf<[1, 'test', true, [1], { name: 'test' }, { 1: 'test' }]>, true>>,
  Expect<Equal<AnyOf<[1, '', false, [], {}]>, true>>,
  Expect<Equal<AnyOf<[0, 'test', false, [], {}]>, true>>,
  Expect<Equal<AnyOf<[0, '', true, [], {}]>, true>>,
  Expect<Equal<AnyOf<[0, '', false, [1], {}]>, true>>,
  Expect<Equal<AnyOf<[0, '', false, [], { name: 'test' }]>, true>>,
  Expect<Equal<AnyOf<[0, '', false, [], { 1: 'test' }]>, true>>,
  Expect<Equal<AnyOf<[0, '', false, [], { name: 'test' }, { 1: 'test' }]>, true>>,
  Expect<Equal<AnyOf<[0, '', false, [], {}, undefined, null]>, false>>,
  Expect<Equal<AnyOf<[]>, false>>,
]
```

빈 객체를 나타내고 싶을 때 주의하기
`{}` 로 나타내는게 아니라 `{[key : string| number ] : never}` 로 나타내기. 특히 value 값 `never`임