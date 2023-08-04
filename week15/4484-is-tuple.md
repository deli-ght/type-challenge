# 20230804

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBAs0BzQgWggSQM4BUCuAHANgKaTJJnkkBGAnhAFYCWAhgHYDm6AFqxABQACjVh24sAtoQAuTAJQQAxBIAmDbGIWS8RMCXl6IARWyF0khgHsWOqKjEFCElpIhMIk6rkIQABr4w57X28AGggAd04GAGNONyYAaxMXFggGFlxsZ3dPH19MIOSlCAAnKWxilnRwzika4tzvfN9Uqs17Nw9CADprCAAxc3rCAA8mOyIALl6g7JMo4oZcSRJZiCimdEIARggAXjQsLUIAHgBtFjVKQmKAXQA+CGBgN2LjFc61jcIAJj2DgKIx1KTCUlnwtHOl2u90ez0kr2IUFW602AGY-v4jscLmIrsVTjCnhAAGZMfCbEhBXoPABqDEIYQglggAHEGJIABLYSgTCCcSSSXDoCZPSToGJdOjoLqDNjAWAIMAgYA6UAQAD6mq12q1EAAmuZyhAAMLmJReDnXLw6m2aiDKnSrTH2Y6YB77U6YG4QEaSQgsJRVc6EABu0IgAH4SWTNhBeZgfcM-QGg97Iy9jHGoAnff7AxAAEqEEFg6hnHF4mFR+GZ3mk8nEVUgDW2nUQTAmZzGr5VVtth0MOyDLIfADeEAAogBHbBk0IT4aeKLOAC+JOK5nUAHJ+LMkDEyUR2CZgJkGOSt46Piikh6SAul5JjtPZ-hjs7AQS7qEa4Q7t-70XQhl2fGcyXfQ4XUhXFoW-DM-wAqAH2Ap8X3Aj8TmBUEWHBCBTi2e4fwRf9gkAx9QNfCCAROccjzYSROF5HYVzg+tNhIsiUIo9DIMBCtri-UI2IQ0ikKAkC0LfDDsVDa5WJjESwBuJsWz7O0+nKBjrggABlP0hVUtT7RVUASAeHTuFKCBqENep0HMfAz0sYU+QFIURWAMUJSlGVijlBVoGAVh0DCa4zIgOkGQgezHLMZzeX5QVhVFcVOElaVZXleBApipzKnCgBZQYvGNbh8DokwErc5LPNS9LfLYJUVSAA)

```Ts
type IsTuple<T> = [T] extends [never] ? false : T extends []  ? true :  T extends Readonly<[number]> ? true : false


/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type cases = [
  Expect<Equal<IsTuple<[]>, true>>,
  Expect<Equal<IsTuple<[number]>, true>>,
  Expect<Equal<IsTuple<readonly [1]>, true>>,
  Expect<Equal<IsTuple<{ length: 1 }>, false>>,
  Expect<Equal<IsTuple<number[]>, false>>,
  Expect<Equal<IsTuple<never>, false>>,
]
```

혹시나 더 짧은 답이 있을까 싶어 봤더니 역시 사람 생각하는거 다 똑같다
