# 20230801

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBAsBMBsAGCBaCBBANpgwgewFsAjASwDsBDAFxLzIGdJUUXWmiBPCQW7DAFbUGkdQDPKgW0UIACgAC9AK4BzPACc8Aa2koOASggBiAgFMAJiWkEdVPQQAOmanpSYS5hRUw7yAMz0Kd0srTJgTNrBEACK0nr0NHSBUACSVpgWemRUEFQclnoQAAZ5WLiEpJTRDAA8AMoAfHk56QAW1BAKelTSCmQQLq4AxkXk1P70EHjuEFEK5LLDAO71JD31ENL02YsUzj1Ow+5KprUVtV1pBHhRI2Q9egB0sRAAYooQegAeFIl6AFx3tVSMUBkshhsPhiANSvQAProABCOAgAF5gYUwSUhmUAOSwnAYqoAbiYwGA43qeGkmAMECI2QxGIgAB8IFi6YyMTCWUycQymbCOViuayYeg+XC+ThhdyMTh2ZLsXz0NKRQqReKxbzJdLhUxancqhAAGokPQzC4QADijgAEtIiJ8IPUqFRLPRPkS-otrgArejXRSyYBwJBgEDAQKgCCQyNR6NRiAATTJ3nwBmylq82RjmcjEBDgTAgOyBVBxUGdGGZSYFWeL3MZAMwwmUwANEwAAoAJQAotXa-XxlRJmRZIimRiwHqkVXXr3hjkACQAbw8XggOAAvovl95WwB5CoAFTXOSYAH4mFAoIz5wv14ui-00WWyteO52Nwvdwej1Uj+eL4z71RUtyk-fcm1yRdX3fdcciqJg7VpAkwHDLNMwgfdIjSHAKFWYZUJjHNQxIKxFDSAsIAXCBOwAR2kFxwM7F4si2CA1wgXZCCZCQCxQdZsBSWRImAaQaEwegx3zTI1hwyIRwAbSYRjmKoMoaLozAykAksIUxXFwNpKoqhbKAlL0LZVNolxNJBB9gPoTFhSM0dZVxIzFKYsyVLUqytPBdEsXZJzaRcyUZVZdVBUctyTI88zvI03zH3KAKcSC+URTFeUwp5AUmSFFU1TFbKUvlRVQuVULVQ1CLOXywzjKo2KvMshKbKAnSUoAET05zwoyjU+W62Vioq8KhsigrQvGzkJVZMq5umjFOtmplOuKzrcpK4bFoVEacB2tb5Q2pVNqFRa4RWtl9pFZabs28VivFRbNSK57bo1Q7JWW9bRtW-KvtFL6qtZDaRrhHaYWO2VpR2-aRrWzb0FBk7zqR06npVd7BWW06Nsuh7nqRx6zte-HvrFNbLu+zacfWoUaYuwaHqZuq3IAXTDEAI3w2N7naKh6hXCpzGdbmechQjkPAKA9QqRoWggDhE3GPBMBEoY7QdJ0XTdegPW9X0FH9QNEGACgGBmLwmD1Q1jRVtWIU1x1nVdYB3XqL0fT9AMEFN+hVfVstrYgABZRRshwRp+KHSIne1133c9w3ZGDUMgA)

```ts
type AllCombinations<
  S extends string,
  PRE extends string = ""
> = S extends `${infer C}${infer POST}`
  ?
      | `${C}${AllCombinations<`${PRE}${POST}`>}`
      | AllCombinations<POST, `${PRE}${C}`>
  : "";
```
<details>
<summary>
테스트 케이스
</summary>

```ts
/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<AllCombinations<"">, "">>,
  Expect<Equal<AllCombinations<"A">, "" | "A">>,
  Expect<Equal<AllCombinations<"AB">, "" | "A" | "B" | "AB" | "BA">>,
  Expect<
    Equal<
      AllCombinations<"ABC">,
      | ""
      | "A"
      | "B"
      | "C"
      | "AB"
      | "AC"
      | "BA"
      | "BC"
      | "CA"
      | "CB"
      | "ABC"
      | "ACB"
      | "BAC"
      | "BCA"
      | "CAB"
      | "CBA"
    >
  >,
  Expect<
    Equal<
      AllCombinations<"ABCD">,
      | ""
      | "A"
      | "B"
      | "C"
      | "D"
      | "AB"
      | "AC"
      | "AD"
      | "BA"
      | "BC"
      | "BD"
      | "CA"
      | "CB"
      | "CD"
      | "DA"
      | "DB"
      | "DC"
      | "ABC"
      | "ABD"
      | "ACB"
      | "ACD"
      | "ADB"
      | "ADC"
      | "BAC"
      | "BAD"
      | "BCA"
      | "BCD"
      | "BDA"
      | "BDC"
      | "CAB"
      | "CAD"
      | "CBA"
      | "CBD"
      | "CDA"
      | "CDB"
      | "DAB"
      | "DAC"
      | "DBA"
      | "DBC"
      | "DCA"
      | "DCB"
      | "ABCD"
      | "ABDC"
      | "ACBD"
      | "ACDB"
      | "ADBC"
      | "ADCB"
      | "BACD"
      | "BADC"
      | "BCAD"
      | "BCDA"
      | "BDAC"
      | "BDCA"
      | "CABD"
      | "CADB"
      | "CBAD"
      | "CBDA"
      | "CDAB"
      | "CDBA"
      | "DABC"
      | "DACB"
      | "DBAC"
      | "DBCA"
      | "DCAB"
      | "DCBA"
    >
  >
];
```
</details>
