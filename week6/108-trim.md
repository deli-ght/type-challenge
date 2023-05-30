# 20230530

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCMAMAcEC0EAqAnAlgW0spBheARgJ4QCCAdgC4AWA9leQGICuEAFAAICGtAMzYBKCAGJsAUwAmmNtnE1J2AA4AbXkqRrMS9LzVg8YkxACKbSQGcamJkagBJVWuWTaEAAYYcAHlQAfJ4QAO50mADGdBA0vADW1hD8EJIAHrwRNBA2WFQA5jGkKpJJVNIQ6JI0bOhUVkkQVJIh2TS5BSG60fQlYbrWKhklAugMCsQM9Cll9ZXYDABuMgB0DhAsDOgp6S6Sa54HNFZ4NEUlbThS5QC8aFjYvgDkUAASkmpqDBAA6ptq5RBHgEIMBgNtipkZDEvsQSo83h8vr90P9HngDp41sCAGqYZoQJgQADiuhebGIAC4IHQaDQVFYKaCjlFlgArKzLTZ5YBweBgEDAIygCAAfTF4ol4ogAE0GDUIABhBjSEpvSqiyWakUQAVGU7FH7hJRWQYREq3ABEAB0qBaIAAfCB2u2O600C0AbjA+pKPmwABlJAIaL4AMrA26h7ZKGZeAAkAG9vkaBkMAL6JzBUASSLYAVTTwQA-HccIHg7488CqaGvT7S9gAEqYPI0sMRiBRtIx6T1TyZ7O5iAFxPJ-om9PFhvN1shqsQGt1s4N9sQW5+mdtv3lkPhgJCkAarUStDWLIK3hWRLHyU6wU4FSbLL1hMQACiAEc2AYADTv1IQlkaYQCMYyAtwPpIFEBiuPk1jAGwthqFYaLesuESXoktwANp4G+AGSJkvift+aj+PcTw5ECf6PFRAQBD+eEEURJEGORfjPHRNF0QxTGAcRX5sX6TxQKJXGAjxjFQPh-GsWRwm0W0onURJbRArx0nMSGcnsQ8zyia0WwGSpinoOpUn-rJgnyRR+kQDaVpZAIDAwrwWyOSZzmuWZ9EWTJhHadZulPCZ5l8QFAmkcFzwOVkoW+WAAC6B5Hje2rsOgPRbKGSj0qlN53mAoB4MCoZ0G5JSkHKWxWAwaiIXYdRUjSdIMkyVgsuynLoNyvLAPwVghLmJUQLi+K1fVthMAy1K0vSjLAMydBshyXI8ggwATQ100jQAspsJQKuVHzuHk1jNXNbWLR1y1dVy-KCkAA)

```ts {0, 4}
type Whitespace = "\n" | " " | "\t";
type TrimLeft<S> = S extends `${Whitespace}${infer U}` ? TrimLeft<U> : S;
type TrimRight<S> = S extends `${infer U}${Whitespace}` ? TrimRight<U> : S;
type Trim<S> = TrimRight<TrimLeft<S>>;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<Trim<"str">, "str">>,
  Expect<Equal<Trim<" str">, "str">>,
  Expect<Equal<Trim<"     str">, "str">>,
  Expect<Equal<Trim<"str   ">, "str">>,
  Expect<Equal<Trim<"     str     ">, "str">>,
  Expect<Equal<Trim<"   \n\t foo bar \t">, "foo bar">>,
  Expect<Equal<Trim<"">, "">>,
  Expect<Equal<Trim<" \n\t ">, "">>
];
```

[TrimLeft]('../week5/106-trim-left.md)와 비슷하게 풀어봄.

```ts
type Space = " " | "\t" | "\n";

type Trim<S extends string> = S extends
  | `${Space}${infer T}`
  | `${infer T}${Space}`
  ? Trim<T>
  : S;
```

extends되는 부분에 분기를 두어 더 다양하게 설정할 수 있다는 점 기억해두기.
