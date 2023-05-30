# 20230531

## [문제](https://www.typescriptlang.org/play?ssl=21&ssc=100&pln=21&pc=1#code/PQKgUABBCM0AwQLQQMIEMAOBLALmgNlgF4CmkSilV5ARgJ4QCCAdjgBYD2zDAYgK4QAFAAE0rAGZ8AlBADEAWxIATLH3lycJeRnxpNiQpoBOBMOVkWIART4kAzjixczUAJLb8WkqwgADdNh4hKQAPAAqAHy+EADubFgAxmwQCVwAbiRGOHYQ7CQQ4lhGDhCeOMYQHOIQaBAORljMAOa5HBB8GBiZCWh2+WJKpSRoGbls+Ub2ODV2iFh2AHQuEDwcRhAkAB5oHmTkvgfZ5Dh0XSmYuATEyhAAvKgXQdchAOTj+PhtMWv4Si8REGAwA2my6CU0gxwbRo+ReAAkSB8vj8-vsDssAQA1LAkGKVZgQADiuDhfBoAC4IGxyhg7OSgdkkgsAFaLNZNYCwOBgEDAMygCAAfWFItFIogAE0OHx1igOEp8gjJkKxarBRBeWYTmcALJ0AKXYIkEIAZRBmmYShy9UaTQB9zNWwtVr8ABIAN6NcSZVAAXw9Xp9YV90QA-G73QBVTrdXrGlARf3u4PRSkvF78kAqtWiiBhKYPPo5HNijV8rDaNbTbX5d0QACiAEc+AQADQN0EkcEQX0FIwcdQvYQ1xBJAieZr2YB8Rz4OwZsA185Fu4QADa5HrnfBISbLfwIT1BqeoRe4g4HBoaCM-3bL1Wl+v-wirc325wu+bBEP+seV1PPAAPKAQAQowABKt4QPewFgZBEQvm+YIfnu35Hn+RqvOe0JPi+0EPhAV43ghr5QFuyGfvuP7Hv+xrpnh9GIWR76UWhv6BLRrxoFBLyMM+pEdhRqEHuhHGYS8NA8SB-FIV2KFfiJ7GGs8LwJDxKAycxQkKdRGEqX8DEACKaYJcmsYpNHiSQPH1iZ5FmcJuliSp4g8TwdksY5onKaeTQ8YSHnaVR3knnRbA8XCgUOTpIWcS8WA8a4UU7l5Smha8zI8QAUsl8nBWlcUANY8QA0rl5lOT5dH4DxAAy5WpZZKnyDxOoNTFBXicwPEAHLtflTWnhwPGAf1bGDXRGA8QACmNFl6aejY8VYc2VelLzEXe8FMaZKUdRNrzzgxJqrbF4k4DxYSnZ1Kl8DxkbXQdLxpDxmKPQtdExDxADq73Oaemw8QAGn9VWvHQPESqD61EDxABaMkALqZtmJbqvwWTjOsJqaLSqMlmWYCgOQAImmw175HQ0rrHYHD4DOTjMHSVI0nSDJ2EyrILOynLwMAYh2DEmQkxA2K4nUdMM1wzPUjgtL0sAjJsCybJGByXLALT9OONLIs6ms+QoOTHzeE09iUrL8vs5zqtNDyfJAA)

```ts
type MyCapitalize<S extends string> = S extends `${infer C}${infer T}`
  ? `${Uppercase<C>}${T}`
  : "";

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<MyCapitalize<"foobar">, "Foobar">>,
  Expect<Equal<MyCapitalize<"FOOBAR">, "FOOBAR">>,
  Expect<Equal<MyCapitalize<"foo bar">, "Foo bar">>,
  Expect<Equal<MyCapitalize<"">, "">>,
  Expect<Equal<MyCapitalize<"a">, "A">>,
  Expect<Equal<MyCapitalize<"b">, "B">>,
  Expect<Equal<MyCapitalize<"c">, "C">>,
  Expect<Equal<MyCapitalize<"d">, "D">>,
  Expect<Equal<MyCapitalize<"e">, "E">>,
  Expect<Equal<MyCapitalize<"f">, "F">>,
  Expect<Equal<MyCapitalize<"g">, "G">>,
  Expect<Equal<MyCapitalize<"h">, "H">>,
  Expect<Equal<MyCapitalize<"i">, "I">>,
  Expect<Equal<MyCapitalize<"j">, "J">>,
  Expect<Equal<MyCapitalize<"k">, "K">>,
  Expect<Equal<MyCapitalize<"l">, "L">>,
  Expect<Equal<MyCapitalize<"m">, "M">>,
  Expect<Equal<MyCapitalize<"n">, "N">>,
  Expect<Equal<MyCapitalize<"o">, "O">>,
  Expect<Equal<MyCapitalize<"p">, "P">>,
  Expect<Equal<MyCapitalize<"q">, "Q">>,
  Expect<Equal<MyCapitalize<"r">, "R">>,
  Expect<Equal<MyCapitalize<"s">, "S">>,
  Expect<Equal<MyCapitalize<"t">, "T">>,
  Expect<Equal<MyCapitalize<"u">, "U">>,
  Expect<Equal<MyCapitalize<"v">, "V">>,
  Expect<Equal<MyCapitalize<"w">, "W">>,
  Expect<Equal<MyCapitalize<"x">, "X">>,
  Expect<Equal<MyCapitalize<"y">, "Y">>,
  Expect<Equal<MyCapitalize<"z">, "Z">>
];
```

```ts
type MyCapitalize<S extends string> = S extends `${infer C}${infer T}`
  ? `${Uppercase<C>}${T}`
  : S;
```

저번에 민경이 풀이에도 있었던 것 같은데, 빈 문자열이 아니라 원본 값을 리턴하도록 하는 게 더 올바른 방법일 것 같다.
하지만 바로 풀어서 기분 좋음 🤓
