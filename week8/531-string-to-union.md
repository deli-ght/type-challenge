# 20230614

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCsDMCMEC0EDKAXATgSwHYHMJ0B7CAVV22N0mSXodoCMBPCAQVwBNMBTNgNKYAhgGdiAN1EBrNgAoAAkz6wADNJEA2AJwBjUQEoIAYgC2vLtgCupk1crUTorHnxhaxzxACKV3s6oaWgBJUwAHABtec1x0IgALXjQXAiJSCkCiFjDeADoIABVspPRhaSTnHFThTHwbXlj8gsSIYit0MPaIUXi2iK4IJiThCHtM4gAzCDxOuKj0dF5MUXcoADFiTAheAA9hcKjViAADU-QVqHRiwv84gF4IAHJ4ACZYR4BuWiuciAAlfxWCL3ZJVfAFYgZagAHgKtwAfB8IMBgNsdjldIsBiRBkkAETwPEQAA+EDxLyJpLxsDxtFOxyO8IgADVsLwAO6tXAQADi2HQAAkrEwAFwQeILMKiEUo866eK5ABWolym3wwDg8DAIGA7lAEAA+kbjSbjRAAJptLYAYWIXCSAqWSVNLqNEB17h+SQwYIhUNwsLRi24om6KXwTIewlwLD1IENrtNN2cEGtYn8CcTZo92HCmziXogAG8IABRACOVmEEQANGX0bxMRAAL4QCaYYi2R4KL1IeXVqIEfzAdrYCKiR6e666dOhh4AbVopYbmOhFarEWhPtcfocAcej3hddwvAkS3hR6XK-Qa8r1a34d3gWhj3Qh7rr8Pl6gy4xN-X97bgQT4wo8iQRBExDvk88SPCSTy8HBpKPBESFPKh8GPFBF41lef63huD6+pCe4vromzUMIEjYJgVgTkeTy6GhWHMZgzFQZhuDMcIzESMx2CscxVjMfRl4ALpxpmWYGhAaxWJg6CJFsGC8FKUlZu6uqgLQTKoPENRJCwVrdMQESjtQ0ripK0qyqI8pKiqaoaggwDRqI7JLDpLJspy4hmeggSWRKHQ2cAcoKsqqq1M58DAH55m4BcEBMgAspsSTWvpEENPg-hisFUoymFdkRY5tTarqQA)

```ts
type StringToUnion<T extends string> = T extends `${infer A}${infer B}` ? B extends "" ? A : A | StringToUnion<B> : never

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type cases = [
  Expect<Equal<StringToUnion<''>, never>>,
  Expect<Equal<StringToUnion<'t'>, 't'>>,
  Expect<Equal<StringToUnion<'hello'>, 'h' | 'e' | 'l' | 'l' | 'o'>>,
  Expect<Equal<StringToUnion<'coronavirus'>, 'c' | 'o' | 'r' | 'o' | 'n' | 'a' | 'v' | 'i' | 'r' | 'u' | 's'>>,
]
```