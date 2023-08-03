# 20230802

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBAs0EwFYIFoIHEBOBTAhgFywwgBUALHAO0hWVruoCMBPCAY1IGZWBrCgVwA2AiAAoAAuy69BAgJQQAxAFssAEwCWfJYpwYMOJmGoKTEAIp8sAZzzqA9lWoBJCiVLqrEAMLkhWCgDmWAA0EACadnwQVqSRAqoQ6koADgJYKhR4EDgQeEzJWBAABpi4BBhklAA8xKEAqgB8RRAC6tyFRcQQDRB1RUZQAHJYAfjqAG6F-EoMhJ6qdhAUdlkUWGq5i7NsDlbqqoRqAHQDEABidkRYAB44KWmnRU94VtSl+ISVFFVwoQCMPWAwBicQS2zwGEsb2wHwq5G+f3+gOBsUEYMKADMcAIrFhoWVPvCqn8AAz-Ekk5EgtEQbZYnF4qDvcpfYl-REQdlU1HxWmFCFQqBPfpvOx2BIAGT4PAAhKcegA1dRYADuEAc6HUeAAEnwGAAuCCkPB4ZJWfVAl7sI4AKysR0uAWAsEQYBAwCMoAgAH1fX7-X7wpEiF5xYVtYcfQHo96IO6jHkCugYSyiV0bgQKKpPNNZhh6hAM-5s0stHmegBeEiF66ZkskiAAfgg9NxEEN6drxc8fybuUhhUNAG0ALo1uueIfqCgYwjZUJHRfT2dEBhj5t1cfdiBTmdzpgLpd7ogAL3XyYJcOqDCHAHI0oE8KRbyPQie7w+Ak+Xz1Da3By22Jtp6IBRjG-okNYWReDguKeOBAZxh6STJJcWSJoUADeEAAKIAI58NioQ4dcBSsFkAC+LYYHY2i3mIGHIOw2KftYwB8LYOK3gm+SFKwsHWBAVZDtQJFkXgVT4YRAhVMyhLVBylKhAKWANA0wSiaRWDkZJBHYrJKbyd8CChNA6n9pYakaVAYnaRJUn6XJV7fNAoQIOZ-5WZp4m6dJBmXqyZIQEpgEMl5NlaTpDkyU5rKkqEACc5kqeFuGRfZekxYZzk-EFcAhZ56neXZvmOdlcVBaSBVAapRURT50X+bCcXsv8ALKQOqW2VFmVNamClwBw0AIAAbAA7AAHAlpKtZyg3DeNU0zSFKVFSOIFgQhsZnHwGBPnOADKBBmptCFIWAoDUD0B3kNgEBMMG0R2AIHH2BQ5pGiaZoWsAVqkLa9qOs68AIMAlBWCqhBXRASqqk9L22LshrGqa5qWlY1p2g6GBOi6oNWM9r27NDACylyFD4LH+EEH0o996OY4DONuh6QA)

```ts
type GreaterThan<T extends number, U extends number> = T extends 0
  ? false
  : T extends 1
  ? true
  : T extends [infer a, ...infer b]
  ? U extends [infer y, ...infer z]
    ? GreaterThan<b["length"], z["length"]>
    : false
  : false;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<GreaterThan<1, 0>, true>>,
  Expect<Equal<GreaterThan<5, 4>, true>>,
  Expect<Equal<GreaterThan<4, 5>, false>>,
  Expect<Equal<GreaterThan<0, 0>, false>>,
  Expect<Equal<GreaterThan<10, 9>, true>>,
  Expect<Equal<GreaterThan<20, 20>, false>>,
  Expect<Equal<GreaterThan<10, 100>, false>>,
  Expect<Equal<GreaterThan<111, 11>, true>>,
  Expect<Equal<GreaterThan<1234567891011, 1234567891010>, true>>
];
```

```ts
  : T extends [infer a, ...infer b]
  ? U extends [infer y, ...infer z]
```

저기에 T, U가 length인 배열 초기화해서 넣어줘야하는데.. 어케함...?

```ts
type Digit = 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9;
type DigitStr = `${Digit}`;

type GreaterThanDict = {
  "0": Exclude<DigitStr, "0">;
  "1": Exclude<DigitStr, "0" | "1">;
  "2": Exclude<DigitStr, "0" | "1" | "2">;
  "3": Exclude<DigitStr, "0" | "1" | "2" | "3">;
  "4": Exclude<DigitStr, "0" | "1" | "2" | "3" | "4">;
  "5": "6" | "7" | "8" | "9";
  "6": "7" | "8" | "9";
  "7": "8" | "9";
  "8": "9";
  "9": never;
};

type GreaterThanDigitVersion<
  D1 extends DigitStr,
  D2 extends DigitStr
> = D1 extends GreaterThanDict[D2] ? true : false;

type NumStrToDigitStrArr<
  NumStr extends string,
  Result extends unknown[] = []
> = NumStr extends `${infer L}${infer Rest}`
  ? NumStrToDigitStrArr<Rest, [...Result, L]>
  : Result extends DigitStr[] // coerce return type into DigitStr[]
  ? Result
  : never;

type NumToDigitStrArr<N extends number> = NumStrToDigitStrArr<`${N}`>;

type GreaterThanDigitArrayVersion<
  TA extends DigitStr[],
  UA extends DigitStr[],
  NumTDigits extends number = TA["length"],
  NumUDigits extends number = UA["length"]
> = NumTDigits extends NumUDigits
  ? TA extends [
      infer TDigit extends DigitStr,
      ...infer TRest extends DigitStr[]
    ]
    ? UA extends [
        infer UDigit extends DigitStr,
        ...infer URest extends DigitStr[]
      ]
      ? GreaterThanDigitVersion<TDigit, UDigit> extends true
        ? true
        : GreaterThanDigitVersion<UDigit, TDigit> extends true
        ? false
        : GreaterThanDigitArrayVersion<TRest, URest>
      : never
    : false
  : GreaterThan<NumTDigits, NumUDigits>;

type GreaterThan<
  T extends number,
  U extends number
> = GreaterThanDigitArrayVersion<NumToDigitStrArr<T>, NumToDigitStrArr<U>>;
```

아니.. 답 무슨일이야...
