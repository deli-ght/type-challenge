# 20230508

## [문제](https://www.typescriptlang.org/play?ssl=44&ssc=1&pln=19&pc=1#code/PQKgUABBAcCc0QLQQJIDsDGAbArgEwFMBnSJRci0gIwE8I0cssIAKAAQGsa0CAzHDgEoIAYgIBDInRHiATrPE0wpEaogBFHMQAuASwD2aZVBQBbAA5YCpgmm0RtACwIQAUuIBu4gMoZZu83sAAwBBeUUAOl1MXEIiIIh+TD1DCGiHZwcacxcpIm1rCIgQrJyHcQ5iDJdtAHd9CDkAcxwbOyIigBVM-Rxtcz6IIkderDwIKhdxCf19K3E0CCDtWS0E-Vkl3nEsIgIgiOMIADENiAIAD3ELKwAuI6DH7RIobWyXXSIABV0mOQBZWwQAC8qBi+GIAB4ANoAcgA0nIiLCADQQWEAUSIujwn10qPRAHVrjgcATYd4FtoFuJYQBdNGwgAiBlhAD4IMBgOcLjkMAVxtoGpMtjs9kFSI8JaQOQA1XQEWoQVIAcV02gAEjgqLcII5tP0iLcuc8MI4IgArDobJrAODQMAgYDKUAQAD6Hs9Xs9EAAmr1NgBhfSECAagiyFze6MeiBO5RvMrobAQoiQzo8gpoPBECCR8R4QxYOgLGjQhkQACqHNBpZdIHdMe9EE6OgggckVSbzfjugsG3siZcAG8IBiAI44HZojG8gj8iAAX0Ssn0pnRbCHiDNOysaCaxGAfV+yIT7wgGE7udB0NIs752khE6nWEhydiULhiNkyMZWJxeLksSpikuSlJ2DS9KMt+yJsmiKxaGycF3nO-JPpOOxvuCcQwgiSLkv+uLYkBJJkoy4HUmgtIVsyrJwYkYoEEhKIoQ+6EvlhKY4dCACMaIAExogAzGiACsaIAGxogA7BW0n0QhTHIVA97zo+z6Ye+qYwnxECCRAIkQOJEBSRAslogALPR2y7EpLEqah6kYa+Wncbp+lCRW-EKasdmsWp7Gadhn7ucJFY8T5iHKWOjmBS5wVptCw6LhWo7iLqsIhLCS7WYxzH+WhGnxVxn5ULM8xoAJwliZJMkVjZey5bZ+UOWxRWcR+iWKVVBk1SZdVomVcwSGgTWNdFqmFc5HXadCDUED1hnGaZ5kMc18G+S1MVtdNrmfmlGVZUuqV5hIhZoMWjSHdli5jX5rUBe1e2JaO+bnZd6XokdKVogdX03XdW2TU5HHPTp4UQAAPnpgMTbFT0JTpUN6eFsP2dtj27Yj0IMEwFY4NmfDRAQeBowVINBSViUE4QvDE3gFa41gZN0vWjbdrGxw4LITgRhA3gFOYuYcz68agDK-OOHILg0AGQxzMehhGnqBpC8awCmuaVoRDadrwMACxELUEYS-Kiry7gKRoMr+qGurmuWtasi2vawBEArVsvBAHL-BsLiBlLTC2AeNuq0aJpEGajs687jrOkAA)

```ts
/* _____________ Your Code Here _____________ */

type Includes<T extends readonly any[], U> = any;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<
    Equal<Includes<["Kars", "Esidisi", "Wamuu", "Santana"], "Kars">, true>
  >,
  Expect<
    Equal<Includes<["Kars", "Esidisi", "Wamuu", "Santana"], "Dio">, false>
  >,
  Expect<Equal<Includes<[1, 2, 3, 5, 6, 7], 7>, true>>,
  Expect<Equal<Includes<[1, 2, 3, 5, 6, 7], 4>, false>>,
  Expect<Equal<Includes<[1, 2, 3], 2>, true>>,
  Expect<Equal<Includes<[1, 2, 3], 1>, true>>,
  Expect<Equal<Includes<[{}], { a: "A" }>, false>>,
  Expect<Equal<Includes<[boolean, 2, 3, 5, 6, 7], false>, false>>,
  Expect<Equal<Includes<[true, 2, 3, 5, 6, 7], boolean>, false>>,
  Expect<Equal<Includes<[false, 2, 3, 5, 6, 7], false>, true>>,
  Expect<Equal<Includes<[{ a: "A" }], { readonly a: "A" }>, false>>,
  Expect<Equal<Includes<[{ readonly a: "A" }], { a: "A" }>, false>>,
  Expect<Equal<Includes<[1], 1 | 2>, false>>,
  Expect<Equal<Includes<[1 | 2], 1>, false>>,
  Expect<Equal<Includes<[null], undefined>, false>>,
  Expect<Equal<Includes<[undefined], null>, false>>
];
```
