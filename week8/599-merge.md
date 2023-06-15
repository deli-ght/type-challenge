# 20230615

## [문제](https://www.typescriptlang.org/play?ssl=50&ssc=2&pln=30&pc=1#code/PQKgUABBCsCcsQLQQLIFMBOBzNkmIMLwCMBPCALQE0BlAL1IGcIAKAAWvqYEoIBiALZoAJgEsArgP4B7YgCs0AYwAuYPHw0QAiuLSNlo6QDs1UdNjQRlAd2lXSABz0RRR5XYCGEI2mv2nAHQQANJoTBDSAGZWABaWjErGwv6W0gBumBiiws4A1mHMUbGWkaIY+ikBphAAYtIYEGgAHh4CDgA2uHgABr3KjHjKjiXSdgC8EADeeFBGrWgAXBD6WUZYANwzEB44SyuuG3gAvoPDEIqjEBPTUFA7i96SxJibt8vNe8qrWMfVQ04QABKenE7WUV1QmBwAB5IqMADQXaQAPnWEGAwEaTScKhEVjszymcyEn2+8O2u0eAmeGHJCSapIOJygvW61WREAAaqJfBEjBAAOKiZQACXExCWMWUygcjAWGP6ihiATkjAC9SwwDgsDAIGAalAEAA+ibTWbTRAqNJxA0AMLSHIQEWYSzmt0miB6tT-SzmGE1ck0DnXADawRc-PypCKNQgAB8IFGijQIABdCBLcPNZRoIzCZhJ6IpgD8EBoYfTmaxObzBbCMYgpZqFYz3jQGQwJzAhvdbogABU9ODbR4Esxe+bPfrRG16uCfVMIABRACO4g87XJS+xSnBRwgkQw0ikAHI2D7EEqN501npgOIDO1GCfvWc6uMpngPEsjE9MCRGTWMATgXAAhDwGmuACqRpPBFCWYhRk6DwTC7BdFFHZwJhDPBtxxZRoVXdd2mhP00Ghd9yXAjBkXJG5bm-GD-zeCUmIwLZ4IgRDpGQkwoCOZFaLAVMDRAY0JwtGobWUOIGhoHNZXEiSjSnbtwCgDkaBiCDLGjG1lh4h9DCMOUIClGU5QVRglRVNUNS1eBgBQxhrGYiAOW5XlGEMgxjFM8zZXlYBFWVVV1WwBzYGAbz2iMvy8A5FB6ksW1tPaG8cH86VAqsmywo1XV9SAA)

```ts
type Merge<F, S> = {[K in keyof F | keyof S ] : K extends keyof S ? S[K] : K extends keyof F ? F[K] : never}

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type Foo = {
  a: number
  b: string
}
type Bar = {
  b: number
  c: boolean
}

type cases = [
  Expect<Equal<Merge<Foo, Bar>, {
    a: number
    b: number
    c: boolean
  }>>,
]
```

구조가 저번 append to object랑 비슷해서 비교적 쉽게 풀었던 문제

처음에 extend의 순서를 1,2 순으로 작성
`K extends keyof F ? F[K] : K extends keyof S ? S[K] : never`

왜 안되지...?? 하고 예시를 다시 봤는데, 후에 오는 타입이 덮어씌워지는 걸 확인하고 순서를 바꾸니 동작했다!
