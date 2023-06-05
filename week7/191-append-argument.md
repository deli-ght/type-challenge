# 20230605

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCMCc0QLQQIIAc0FMB2ATVATgOYCuAtjgC6RKJ300BGAnhALICGAxgJaYBWEAMo8A1gHsCHCAAoAAmW59+AZzGSOASggBiCrh7ldHYuSoqwNHdYgBFEphWUe47JagAxSRCI8AbjgQAGYk2FzOrhCUzFgQAAYe2HEANBAceGnYrNGxcShxsumsPNhRABY8KhBcrpSYAB6UEBTpVQDumBC4rgDkTQSOlAQ84eWdOZip6fgAkl29TWUcARAlzSX4RVExnYC8G4CQe9pcAxx1aT44mMNc27FtFVxlEG08ADavURyinQlJaVWUMqdII8AhONKmCjYSipPIFDgAoEQFSYGp4KYZF7vCBoAjiXAkLjA0LhFylCbxADiBXuIyeWI+jHGSJUHAo-3iiQKjBITRegLSGBwuEwm0hVHi+Q50leCKarkwADp3BAvAQIA02WhXpMVXF9RMVMceGhqFAKYkIABeQoALgg2HITIIqUY9qcw2wRG0VoAfA6nVcVRSAEqOEivJo29BYPAocXQgA8iVd4nEOvSvpowGAGvqWHCoogTLtAbIztd7qGJSIqXq9sYaYz2B9-sd5aDUH1cRV-oAKhUqgBHBxOMmrKpoSR1fBBPFkMYQADakh4vmwHA+JmcXB1AF0ZGVKJQ0CpbTmRX5FZRxMBFFw1BIpMAOLg-OkibhEIbjabEA0rl4FEVEQEdBjJRAABYoNgABWLhtBYZcFCUARHw0A8jxPM8c18QESEYRUajIO9UNUdQpE0XsIAANT4NoIEiSkeEoAAJAj7Sw09z2ASgjTKRVVEVSQiGAOBoDAEBgEsUAIAAfQUxSlMUiAAE1xBIdUAGF8U6Virk6ZSjIUiApMsCkY2FeNSChShk2wVIUH9G0ihkkB5OM5SID7QYIC0hFHA8zyVLMngyCnAgmgpABvCAAFER03VI4vzVEmgAX2CecIB6OQJkQR5Nx1L1HGAXk3hUHpzJ2PyAoQaMhTjBM7JkDh7XbCtiyrT1vWtNtAxdYsm0wTMwFDcNI3q0sOquStkWrL06wbYb0lbMtnWq2J-JRAAma1UEa3BrLMJMZDWvxxB4XBUlCEUQWwUUs3GlQI0oPabRkesIFuzB7tFc7LtwTbOi4AKqhtJcaBSgs7ISkhN0TbbMGgVIwxeybfV9ZIodS8JEzhhGkZ21GJrezHsagHMIDykCGhh-8CDxAgaEspqbKoRNQlEbBxDaBzvrwX6Ske7G9zcoLgrk1VNMBK5hDqU8JeC0zpNAGh-SEJYBggZgNPVFR03K1wzwgLicN4-jBJUYTiDE+AX2wFQOmZqB-TozAGIN14jcdzjj24nM+MeK2bdE8TgC9n2LFd9hJE6LSlneHAiEcP3sJ4oOBKEkTJOkoA)

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
