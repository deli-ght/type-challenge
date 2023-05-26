# 20230525

## [문제](https://www.typescriptlang.org/play?ssl=56&ssc=2&pln=31&pc=1#code/PQKgUABBBsBMEFoIBUCeAHAphAMgezwGsBXdSRBSq8gI1QgEEA7AFwAs8n6AxYiACgACAQ1YAzYgEoIAYgC2mACYBLYnNnEmyzrLnCy5GUYgBFYpgDOLbUzDkAyngXWFFgDQRUePnvoB3URYIFjwIABsCEnQIMTwAJwhhYIxsZSZEiE0bYNC6YLZMZQThFhY45RpiFksAOjsoAEl09mULCABjNmEwsMwmAHNMDz9sP28wxXDlQmwQiEGg9mx2+LjLdE4VAeSsCDyLTGE4zrT+mPj85ac5HQADFhTbmOVMCYg0y8ytO4BhEogAD4QAAieH6txqECaEDwSwSYziincEBGKOUPQgmAAHlh2otQgsILdQeDzglbvgiABVdAAHhJgIgfxYHgA5IowayAHxPUSTW7Mp6xcmUwg0+lgxnMtntErcp4fJbnHp4PynTFY4RydC9OrkW4GlgWchpapxMTCdrYZkQADe5CgDywAC4IKzZSxWQ69mslBZXayGHQLBY0spRKzGaz7Bw4uxhEVI0DWT9iHEwkm3QAhPr9bpeqAAX3q71YmHNluwDPtUEdKQDHP6BdrNF9SIDAAlvExFJnWVnyqVRKg+1niD1G6O8Fjy82oCsInEA63VUw+342Mpqn2aGFLYRm8XyE7sABZVAktC7AC8uEi4ptQJJbMnXIgwGAGtx1Umcxo2GJMFbn1A0SzfAA1F4-BhdIAHEtw7YgaFdNhSnQf0PyNToagAKwsGp4n6YA4DAEBgDsUAIAAfRo2i6NoiAAE1vASH48EUbAO3LbB6N4miIDIuwTzvak6SpDxkA1aoezaKxygGN9bxrCAAG0AGlSxQABdV0qSkvokTtHZMFdSTCwgAB+CA9NdJhMAAN3LMBCxU5AtLsMBKL43iUEsII-gONpvPogTyOUbV4kWFIjIAUQAR2IboPBinFMDxCBzLEOInDdQQTwQTpul6AZLGAKp0QsL0wFNcsLStJl-mUk8Aw9ZtW0wP0AyDVAQzDCMoxjSKukTKNU3TUdc3zZy7Bqit6urY96zdSdaDbf03S7TReyjActxYYdR3HCZOR26dZ3IBd4mXbK-DXKMNy3TAdz3doD2msBhOYcLuggW9HxBMEhOi2VAt+1TyBS79aXixKwlpUVxS+vQwhfTkuQ8EkuXRiHUrxaGEu6eH7zpJGkrdVr0YalgsbcMB3M8kBqOChjeDjAoEnsap0KZ5mqNChnyDfGMjmwLw0wgCw8DCcrOHW1CWHQ51MIsbC8IIuIiLgYBRAsEY4kFiBIMwaDJel6xZZQtCMOALC2Fw-DCOI2BgFNmWmGNKA31PeJrS6Hpc0sS2Fet237fV-pSPIoA)

```ts
type LookUp<U, T extends string> = {
  [K in T]: U extends { type: T } ? U : never;
}[T];

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

interface Cat {
  type: "cat";
  breeds: "Abyssinian" | "Shorthair" | "Curl" | "Bengal";
}

interface Dog {
  type: "dog";
  breeds: "Hound" | "Brittany" | "Bulldog" | "Boxer";
  color: "brown" | "white" | "black";
}

type Animal = Cat | Dog;

type cases = [
  Expect<Equal<LookUp<Animal, "dog">, Dog>>,
  Expect<Equal<LookUp<Animal, "cat">, Cat>>
];
```

lookup이라는 단어에 힌트가 있다..! 객체로 변환해서 값으로 인출하는 방법 익혀두기
