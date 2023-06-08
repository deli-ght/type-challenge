# 20230608

## [문제](https://www.typescriptlang.org/play?ssl=30&ssc=2&pln=15&pc=1#code/PQKgUABBBMCcAcEC0EAyBTAdgcwC4AsIB7AMwgGVcAnASx0mSSeYYCMBPCABRuwgDEAhjggAKAALYkABwA2w9AEoIAYgC26ACY0ArmtW50auYMNJZNQ1UGywDFQ4gBFHegDOuGkUx2oAYSJjHUMIAnQIWSw8QlIIQQgPWhELKxsAGggAd3waAGNCVnR8QQA3dwiaAGtwgANKJOwVSJwCGoA6XwgAPggANRp0TOJMCABxSwAJHVYALgh8XFxpNxngYFw3fLaAKzc2oipsYDh4MBBgO1AIAH1bu-u7iABNIh0qCADNcIn0KnCHgG3CDnOy4djScIYFr4ADyJHqdGwAB4GOQIOgAB6GTCaNwJaiItIMAAq6KxWFx+IaAG0ALoQAC8EDpYB6TLRmOxlJqABIAN6JREAX35dBIvwgACUhTUGAB+NBRAhwhE4JGSjLUtra4kZQU4WldBhzYnUgDkzWiZtpAG5LiAboCHhBie5cB9BG5yk7nSCaMYDu6wRCIHyIABRACOOnSEYxENy7qFEBIVECEDN4mD6CQ+RslvcwGCNFkbjNoPB4VynvKTOpDHD8fQiaRUZjsiRUOiKoJarNZq6GQADF1Bw2my22zZO0rYfDe8izZU9FUiAOMgA2UdEqCNhO4VvR6dd5XzhpIs1-OiCdcQACs2-H+8P7Zn0J757N5FeOIAhBGdGkfBvF0NRbwARi3MdaXtR0fSBfg3jCd5KHQZY4Pg4ELlABgenIYo-ggdhXneNwiFkYtvBWeZFmWVZ1k2fAdj2A4jhOYBhDcTJflwvoBiGMiKM8Ki5gWJYVjWDYtl2fZDmOBBgEEyjMDcXiAFkDnCPxilkAtqLEujJMY5jZOwM4LiAA)

```ts
type LengthOfString<
  S extends string,
  T extends string[] = []
> = S extends `${string}${infer R}`
  ? LengthOfString<R, [...T, string]>
  : T['length'];

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type cases = [
  Expect<Equal<LengthOfString<''>, 0>>,
  Expect<Equal<LengthOfString<'kumiko'>, 6>>,
  Expect<Equal<LengthOfString<'reina'>, 5>>,
  Expect<Equal<LengthOfString<'Sound! Euphonium'>, 16>>,
]
```

string 자체에 `extends {length : number}`가 먹지 않음.
따라서 해당 string을 array 타입으로 바꿔주어, `A["length"]` 형식이 가능하도록 만들어 주어야 함.