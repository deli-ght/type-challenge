# 20230605

## [문제]()

```ts
type AppendArgument<Fn, A> = Fn extends (...args: infer R) => infer T ? (...args: [...R, A]) => T : never

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type Case1 = AppendArgument<(a: number, b: string) => number, boolean>
type Result1 = (a: number, b: string, x: boolean) => number

type Case2 = AppendArgument<() => void, undefined>
type Result2 = (x: undefined) => void

type cases = [
  Expect<Equal<Case1, Result1>>,
  Expect<Equal<Case2, Result2>>,
  // @ts-expect-error
  AppendArgument<unknown, undefined>,
]
```

배열을 타입으로 치환할 때 `extends {length : number}`나  `[number]` 를 이용했던 것처럼
함수 내부에 사용된 값들을 타입으로 치환할 때 `extends (...args: infer R) => infer T` 구조를 잘 기억해둬야겠다.
