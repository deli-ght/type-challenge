# 20230601

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCM0GwQLQQEoFMAOAbAhgYzUiURNKICMBPCAQQDsAXACwHs7qAxAVwgAoABHIwBmXAJQQAxAFs0AEwCWXaVIZpp2HGsRYFagE44sYIpLMQAilzQBnBgrYmoASQ1Z1aRhAAG6TQQAeAGUAGggOfRZpMIAVFgA+bwgAdyYFPCYIfUxcAghmNAg7fQU6AHMfCKik5L1M7ziktjzS-KZCsoUAN08ihhLynyDvJ3CWfQg0AA8cN0Iib0WGGyIGSgxC7P95CABeVBz8NACAcjWNmwgcbIhROgBCE7CTu6eIE5xk2yi0E-iIYDASZTDZ4NRyfIsCDkQpnda2K43T7fWSPBaLUb-ABqCjQyQgbAgAHE9AAJLjkABcECYDAYGBslMBywyADoAFY2VnjMrAWBwMAgYAmUAQAD6EslUslEAAmiwuBMAMIsOSFUloG7S7USiBCkVA86FPy5Y5BYFqOhyS7FUplMJVFTTS3WvoDe0QOIWzyu23lf77c3On2XbwAEgA3qVhJrwgBfSOOhNRugxiYAUTjSQA-D5E8m4snM0lqUEDRB0yC0GCAumAI5cIwBE1HU7CFgscjXLv6N4nPvtlh-Z6Dns9v7xMKAGXITEaDttgt6rTb+naHZEnVMXSv3bEocHl267QGIEGtyG8ym0-HExul66AEQPiC5uhoHoTalJyPR2PFl+XhwBYsEWWYQKWIogOKOrSp6tgMBASo4DYCIwbB+oKBo4wIXOEYVg2RhhJWoIIXGtx3ic-BGogGRGO45S2MAXD2FgNgnLO8IQHgyEIvsADaRDEdWDC1gRWDNocgQvB247PLJ7yDsOCkdop8SToJVY1vWjbiS2Umjt21x9vJ0lDpOyksAZvZqSEGkkaJOkSQupljkZzwDh2SkuYZ1nqVAQlaWJTmmm2Mk+cZbnvF5VkTrZ-maSJ2lNnpxzefoJnkIYHlmSOYXpUZNl2cJDnJZJqV9hV5n9oVAC6kHQWhurcPoBQTEEagMg1jV6sKoBEP8QRMNchSUAqEw2CwWDMQ4dCMjSdIMkywAskwHJcjyfLwMAQg2F8+j9RAOJ4kUk3TWwc20vSjLMjYbKcty+i8vywATVN9jnQdACy4yFEqQ1YPRZS2NSl2LTdd3rY9grCkAA)

```ts
type Replace<
  S extends string,
  From extends string,
  To extends string
> = S extends `${infer F}${From extends "" ? never : From}${infer E}`
  ? `${F}${To}${E}`
  : S;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<Replace<"foobar", "bar", "foo">, "foofoo">>,
  Expect<Equal<Replace<"foobarbar", "bar", "foo">, "foofoobar">>,
  Expect<Equal<Replace<"foobarbar", "", "foo">, "foobarbar">>,
  Expect<Equal<Replace<"foobarbar", "bar", "">, "foobar">>,
  Expect<Equal<Replace<"foobarbar", "bra", "foo">, "foobarbar">>,
  Expect<Equal<Replace<"", "", "">, "">>
];
```

처음에 다음과 같이 작성했다가, 빈 배열을 넘겨주는 케이스일 때 실패했다.

```ts
type Replace<
  S extends string,
  From extends string,
  To extends string
> = S extends `${infer F}${From}${infer E}` ? `${F}${To}${E}` : S;

// Expect<Equal<Replace<'foobarbar', '', 'foo'>, 'foobarbar'>>, ❌
```

그래서 빈 배열이 있는 경우에 대한 케이스를 추가해줌.

```ts
 `${infer F}${From extends "" ? never : From}${infer E}`
```

근데 너무 길어져서 이게 맞나 싶었는데 다른 답변 보니깐 결국 분기를 어디에 두느냐의 차이인 것 같다.

```ts
// https://github.com/type-challenges/type-challenges/issues/354

type Replace<
  S extends string,
  From extends string,
  To extends string
> = S extends `${infer U}${From}${infer V}`
  ? From extends ""
    ? `${U}${From}${V}`
    : `${U}${To}${V}`
  : S;
```
