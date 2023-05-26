# 20230526

## [문제](https://www.typescriptlang.org/play?ssl=34&ssc=2&pln=20&pc=1#code/PQKgUABBCMAMBsEC0EAqAnAlgWwgGQFMAzAF0mSUqvICMBPCAQQDsSALAe2YYDEBXCAAoAAgENWRPgEoIAYmwEAJpj65ZJAtgAOAG1EakOzBvSidYcrKsQAinwIBnEpi4WoASW07NBVhAAGGDiEpAA8qAB8-hAA7myYAMZsECSiANaOEOIQBAAeogkkEE5YzADmKXRaBFnMihDoBCR86MwOWRDMBDHFJKUVMcbJ7DVxxo5aBTU0BGWYzMzzFY3YHABuSgB0bhA8HOg5+V4EO-5nJA7kJFU1fThKEAC8aFjYISShAORQABIEOjoOBAAOr7HT1CCfCIQYDAQ7VQoPEhAmaQv4AoGg9DgqCfchnfw7aEANUw3QgXAgAHFjD8+DQAFwQNgkEhaBwM2EXJKbABWDk2+zKwDg8DAIGAFlAEAA+nL5Qr5RAAJocFoQADCHEUNT+jVlisNMogErA12qIPiGgckwSNWenwAOsxvgAfSEe91OkifADcZpuL2CxA+AGVoc9Q4cNHV2v4ACQAb2BVomUwAvkn5kQCAcAKrp6IAfiDbxDoTz0KZof9YGlRsNaEcRQ1ogcmQbipNkpwWn2RXNNUTEAAogBHPhmAA0o9yCKK6YgRHQHFwn2Eg6QSTM3nKjmAfGcOgceIDFoSbcyzwA2uQR3OCIVQuPJzpwq93l8SlCZ59vxEIinO8HyfF8zHfYMwm+f9f3-QDgPnZ8J3AoIyygqAMJgyE4KAqB70QsC31Qz9vgw3oDjIn9sL6MjIQA3DZwI5CiI-ctSIgZ1HSKIgOBRUQDioz4eL4gT6IQx8PkIiC0I+T5BKheC8JAyTmOkkiOOYLj5LEgBdKUQANTs5V2FoRgOUMNHZQyjO7OtwCgaFQzYfiajoNUDgcDgdEPFw2iZFk2Q5LkHB5flBXQYVRWAcQHBiXNyBJMkek87znC4DlmVZdlOWAbk2D5AUhRFBBgBSnz0oSiAAFl9hqDVnIBXwykcfysqC3KQvysKhXFSUgA)

```ts
type Whitespace = "\n" | " " | "\t";
type TrimLeft<S> = S extends `${Whitespace}${infer U}` ? TrimLeft<U> : S;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<TrimLeft<"str">, "str">>,
  Expect<Equal<TrimLeft<" str">, "str">>,
  Expect<Equal<TrimLeft<"     str">, "str">>,
  Expect<Equal<TrimLeft<"     str     ">, "str     ">>,
  Expect<Equal<TrimLeft<"   \n\t foo bar ">, "foo bar ">>,
  Expect<Equal<TrimLeft<"">, "">>,
  Expect<Equal<TrimLeft<" \n\t">, "">>
];
```

진짜 생각치도 못한 풀이 방법,, 공부할게 아직 많군용
