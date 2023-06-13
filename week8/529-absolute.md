# 20230613

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCsBMCcEC0ECCAjAzgewDYFcAXAU0mSQsrPQE80A7AEwCdi6BpZgQxwDdMA1nQAUAAXSsAzAAYB3AGzwAxpgCUEAMQBbYowCW+LZq1dCAC00ktAB1yniSXHpLdcYMhs8QAivmKZCPWx6dygASRtcYh16QghzYggAAwwcAhIk+JprYgA6NCyc+LNTeK4BRIDmPXoAcwAaCHpDdGJmCGx29D1amsJ8gBUzROwiayIITDNR3EYIVoguCGtsTGc9XkTmrVb2qpra0IgAMU6IYgAPLkjSMiT7wkwyQmzEgf84gF5kAEZpaQA3M9XhAAEr+fC4L5oLB4IjEAA87wCAD4ARBgMBzhcckoSHNCNh5okAER-aQku73I4oiAANT0xAA7h16BAAOLOAAS+HQAC4IGZCIRrJg+ZjHkozLkAFaYXKdWrAODwMAgYDuUAQAD6ur1+r1EAAmqN2gBhbCMRJctqJA323UQdWarEvIqpOEkJHYkhMTBNFptCAAH0mhGqdRD8x6fVp3wgAx9xD9yQAJABvGoAMyDqAAvhns0GAEJ5zIAfgKl19jH9ADlA+1K0kM-nW7D0ojiyiyxABS30x7Owju73+xmBmWwG7EkP4d7q8nawGdkHQ-tI6Hur1YnG0+nJ5lFymkkhC-Qc+0AKq9ytXvv7w+akA6h0GhMfCBmnj+V9vw3OnoNidHEM4QOmEAAKIAI74FwuCNJBOLEHiEB5hAWbMNgRgAOSiDOSBSvBUR1P4wBEHouCYDh7hKMEASLA+c5ejh0g4XurE0WBSg-v63wANpkEhuKEAiMFwbgCLMYi0goo0nEonJQnIXiYmwfBUkdvOSCyfJbGKfUykiWpEmaWk85-HJEA4X87FKVAwkoaJ4kadJCJINAVk4dAdmGQ5KnOepkluQpem+UZTkma5WksTp7FhQZEWqS5wUxYiNn6fJtmJf5xkpWZnrpR58XWT5OVQQFUWpeZXpID82r-NIDX-PQXnko1+n2RVeVBQVw7wNq8BDa18lDUN4UALrPn+-7aic+DMAk7QAMokKKM3-k6GqgGQtLLSUrAQDQpqTJ6QT0GKgrCqK4rAJK0pygqzBKiqwBcBdTJtLt9KMiyNXnZdQoimKEqYFKsryoqyoIMA-30d9ACynSJGaJS4CRtT+AKQM3aD4OPYqaoakAA)

```ts
type Absolute<T extends number | string | bigint> =  T extends `${infer A}${infer B}` ? A extends Number ? `${A}${Absolute<B>}` : `${Absolute<B>}` : `${T}`

```

괜히 저번 array 문제처럼 풀려다가 실패함.

문제의 요점은 - 기호를 떼내는 것.
`-` 기호가 있는 경우와 없는 경우로 구분하기

```Ts
type Absolute<T extends number | string | bigint> = `${T}` extends `-${infer U}` ? U : `${T}`

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

const a : Absolute<'0'> = '0'
type cases = [
  Expect<Equal<Absolute<0>, '0'>>,
  Expect<Equal<Absolute<-0>, '0'>>,
  Expect<Equal<Absolute<10>, '10'>>,
  Expect<Equal<Absolute<-5>, '5'>>,
  Expect<Equal<Absolute<'0'>, '0'>>,
  Expect<Equal<Absolute<'-0'>, '0'>>,
  Expect<Equal<Absolute<'10'>, '10'>>,
  Expect<Equal<Absolute<'-5'>, '5'>>,
  Expect<Equal<Absolute<-1_000_000n>, '1000000'>>,
  Expect<Equal<Absolute<9_999n>, '9999'>>,
]

```