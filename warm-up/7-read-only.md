# 20230426

## [문제](https://www.typescriptlang.org/play?ssl=32&ssc=1&pln=50&pc=2#code/PQKgUABBDsELQQEoFMCGATA9gOwDYE9J44TSiAjfCAQWwBcALHKgMQFcIAKAAVXoDM2ASggBiNAGcqo8mwCWuOnDnYxAJzRY80zOQBWyAMZKA1snwSwRUTYgBFNsgl05OK1ACSAWwAOuZF7I9BCMyBCyCkoqEAAGKBg4BAA8ACoAfDEQAOZByGpyhhAA7nKMmGx0EGwSKlkQpQB07hAAwjjOamzGEhCoIfg+YSWMvbi4ED5qmINqLk4QmPwQKRASyJV0mBAaCdoANBCBfLUhDGGT03lzPYunYYbtdJ3GyOj9gxCGfNiYleRhOwkNSy2FeTSILEwaggyAAHqhfP4AFzNGJouiWKAqOh5fioQxhFKYLAQADeRCgLjoyNWT1qFIg6CchnyPhcOCRtPy2CyRAAvs0HthnCFiZhOQBZfDxLTJIlYNIQAC8ZIZVJpACIABLmDV7BlMiQsuRs1zYTka-iYXSoNQa-nNTZYBrqsIq7XIMaYDUQYDACAAUTUUzUnK+2B+lUBwNUfR2sqoFxmdEIlLFDUNxtNOGVEA15FtkO9vv9QZDYe+v22khjvWruwIEymydTsTRzUVADU5MgigtVABxUpatjkTkMOh0HwSJF+jGGBgNPQSBpQrLAaBgEDAKygCAAfUPR+PR4gAE1ytC2kyIDqNAeT4-9xBt1YUx8pTLEvhUoqVaT6wTCAAG0AAV6lUMx8FuFIAF0IE5FIwPggUwD3J9H2WJxKhaVA1h6DCTxfHc5F8KENgGMIAIDABHNhUFwA4A1hQZjAgPkIH4KYvAgABybh32QOAFwY-weScYAKgUCReLfSjPjw+YVWAohmNYugklo+jcCST9NG-VIxQARjSA4v20QysBMtJTLAWCrGxXF8UJYzVUpUoaQ6ekoEzVl2XNLlvM+TBEXWV5OXIa1-D4IhAjoVBOXJKAoFQComFDQKeQdVD0MI092FmM5oQAZRxacHzy59X1AIhFWKhhbTCaC2GhCRMFwKT2nHSdp1nYB50XZdVzUddoGAPgJCKPJaogbte1WdrOuFbqpxnOcjUGlc1w3YA2o6-zMQgRUJShMIWgasYghyGcIAnVa+oGpctpGrcdyAA)

```ts
/* _____________ Your Code Here _____________ */

type MyReadonly<T> = { readonly [P in keyof T]: T[P] };

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [Expect<Equal<MyReadonly<Todo1>, Readonly<Todo1>>>];

interface Todo1 {
  title: string;
  description: string;
  completed: boolean;
  meta: {
    author: string;
  };
}
```

- readonly를 key 앞에 작성하기
- Readonly<T> 와 같은 방식으로 사용
