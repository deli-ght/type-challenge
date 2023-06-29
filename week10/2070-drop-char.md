# 20230628

## [문제](https://www.typescriptlang.org/play?ssl=37&ssc=2&pln=21&pc=1#code/PQKgUABBBMAMDssIFoIBEBOB7ADhAwgBYCGGkKylV5ARgJ4HE4AuxAlgHYDyAZgAqEAQhAAUAAXxNWnXgMEBKCAGIAtgFMAJmwCuK5czUqcAG2IHkxtgYzFjyzjzVlyS1xACK2tQGdmbLBxg5Ji4EMQQ3jhqAMZsPGyaENEkGBA82HrhvhicAOYAdEFQAGJYqWoAHsRGxmoAXEUQAAYtzN7kzHRREILazNY8xgwAvOjYOESkADwA5BA0ENoQzMsQahCpPBB2DACEEDMANAcHAHwQwMAHNH0DQ7sz5C1NjecAagkA7hABEADiVgAEtoaHUIIR+jhvHVLm1kvkAFbefJlXLAOCIMAgYBBUAQAD6hKJxKJEAAmlhtKl8FgNOtAU51iTmYSINigp1uiEJikpgBlY74c6jPlrCoGDgabzNAAkAG8HE4IABBAC+8sVqUEqqaEAA-CqxRKpQR9WNcJMMFNBILzmCmvK1fLuZbrbadRAwXzcSACSySRAACo+FaSbw+P3+0nsthGMorTnrOUQACiAEdtLZjimKlFoitVWkMgcxInkMlbLUOLkfMA+mxjN5HmBogFfGFPeaedM5lB5rclYM6Ps+6OjicZsLrgOMEOHhyuutosRw9LRgBtciXCCl7zISp55j7jDYMhQHOHqbpzPGKYu3kzG79Qf3cczSfHR8zueT06HcgXjEzBXhmth3uMrpfs+myvp+Zyfk+dzDr+-7nrmQEgTe4EWg+iEvshn4PH+07QWkQwoQB6H5phYH3j2o54TBw6jmOcEfiRSFEX+lGXtetEQQ+8yLKsKzrJs2wQHsBxscRUGcRRaG8aBt50VacwLEsCZrBsaQSVJb40OxvaaasYm6TsED7ApqZUcBfEqQJ9EaSJ2niRZVmfswRlCUsUBmVs7lnNxAC6PqRlG+IQMUVLMIQSp8gYULhVGbI4qA5DnHyKTrHQlKpN4WDGPWbZghCzBQjCwBwoQiLIqi6IILAwDEBw3ifE4GUQB8ajfAVRV+CV4KQtCsLePCSIohgaIYk1fXFa1nUALJlOskzGFWNbQkN5UjVVY01RNqJYjiQA)

```ts
type DropChar<S, C> = S extends `${infer A}${infer B}`
  ? A extends C
    ? DropChar<B, C>
    : `${A}${DropChar<B, C>}`
  : S;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

const a: DropChar<"    butter fly!        ", " "> = "butterfly!";

type cases = [
  // @ts-expect-error
  Expect<Equal<DropChar<"butter fly!", "">, "butterfly!">>,
  Expect<Equal<DropChar<"butter fly!", " ">, "butterfly!">>,
  Expect<Equal<DropChar<"butter fly!", "!">, "butter fly">>,
  Expect<Equal<DropChar<"    butter fly!        ", " ">, "butterfly!">>,
  Expect<Equal<DropChar<" b u t t e r f l y ! ", " ">, "butterfly!">>,
  Expect<Equal<DropChar<" b u t t e r f l y ! ", "b">, "  u t t e r f l y ! ">>,
  Expect<Equal<DropChar<" b u t t e r f l y ! ", "t">, " b u   e r f l y ! ">>
];
```

easy~
