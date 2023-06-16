# 20230616

## [문제](https://www.typescriptlang.org/play?ssl=40&ssc=51&pln=40&pc=1#code/PQKgUABBBsCMBMEC0EDSBTARgQ0wYWwGd1JklyLTMBPCAKQHsALAO0IZYjyYFcIAKAAIArZmw4BjBgBN0TANYBKCAGIAtumkBLHmtUAXdGoAOAG2yGkprYYBO2U2FIqXEAIo90hfVo5OoAEroZtgS6BD6TOEABhLYGqYExNEQDLYQ0QAKRHGJROgp3rZaLADmEADuNkwZ8li4SHHJAHT+GQBiDAwAQti2vQBeKUgAfBkAZl1IOLbT2ENtnenoAB7xZiSk0dv6hKT61MbhnT19gxAAvGj1+PkAPABEJ7398w8jANykUmz6EJMMGY4AYALggzzO80uEAeALms2BDy++0O4QAIgwAHIMSIlcpXDA4W7ER7SBhIFg4ph495fKA-bwQMnY3FlMEYlnUsrQh5kilUml0jLbNpjABqWnQFVSnAA4jYABI8TBgpj6fTGQgg4DAXYSJjNYSEZppUrAODwMAgYBOUAQAD6jqdzqdEAAmgweOk8DJwgr0LZwi7g46INanAcjtciUl0HcAMpjK7xiCrQwsaSEDIAEgA3iVxgGIPHYABfPMFovx+CllIAfmLiDT6AzWYAMgwKgGmnHqyNSA3onmO13bD2E7ARuXc4TcLGE-Ap9FSGCh7mR937iWp0g87Pib3F7WV8XkXaQ8GIAAVLx-WNZi8usM2rQmNJ-SPhXMQACiAEceAcAAaX8ViOCQ-lLf5bAYPQAHJBE-RomAcUwW1KLxgB4HxTEIOCI1RCAeyzK4AG1SB-MD0Agu5-0A0w7n3ec4IhV4BjgkYQLguEZjmdiRk4iiqJouiHEYm5mIBF5Bg4rieL6PiOMEqBKPA-RaIAsSmPubiphmWSIF08l9IEoChLUjT6PEmMdIBe0TLkrp7L6JSzJU4T1NEhjtJJFipheAyjPIEzlNAiyvOsucdIAQW6PBAuwaZGlc8zqM8zTvIknSkECnLTNSkSMsig87jgwKUvc8Kip8uM4MAXg3ADg9wLGpSgBdW0QAdR9XXaL1IirQxNS67r7WfMBQFIMZ4xQwMIGoT10nYUxsN8NhVXVTVtV1Qh9UNY1TXNBBgGwNhR0miAJSlCAlpWjgtQgNUNS1HU9QNI0TVsM0LWAG6fDu86AFk0nCbhUPQrx1qerbXr2j7SitG0gA)

```ts
type KebabCase<S> = S extends `${infer S1}${infer S2}` ? S2 extends Uncapitalize<S2>
  ? `${Uncapitalize<S1>}${KebabCase<S2>}`
  : `${Uncapitalize<S1>}-${KebabCase<S2>}`
  : S;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type cases = [
  Expect<Equal<KebabCase<'FooBarBaz'>, 'foo-bar-baz'>>,
  Expect<Equal<KebabCase<'fooBarBaz'>, 'foo-bar-baz'>>,
  Expect<Equal<KebabCase<'foo-bar'>, 'foo-bar'>>,
  Expect<Equal<KebabCase<'foo_bar'>, 'foo_bar'>>,
  Expect<Equal<KebabCase<'Foo-Bar'>, 'foo--bar'>>,
  Expect<Equal<KebabCase<'ABC'>, 'a-b-c'>>,
  Expect<Equal<KebabCase<'-'>, '-'>>,
  Expect<Equal<KebabCase<''>, ''>>,
  Expect<Equal<KebabCase<'😎'>, '😎'>>,
]

```

`Uncapitalize`라는 타입이 있는 걸 처음 알았다. Lowercase로 하면 다음 예시에서 에러남

```ts
  Expect<Equal<KebabCase<'FooBarBaz'>, 'foo-bar-baz'>>,
  Expect<Equal<KebabCase<'fooBarBaz'>, 'foo-bar-baz'>>,
Expect<Equal<KebabCase<'Foo-Bar'>, 'foo--bar'>>,
```
