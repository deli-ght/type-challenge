# 20230517

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCcELQQCIFNkAcICVkEMAmA9gHYA2AnpPHNTZQEZkQCCRALgBbGMBiArhAAoAAjjYAzXgEoIAYgC2yPAEtec2QCdchUoxkE6AK2QBjVnADWyMgGdZeVGjCUZLiAEVeya6yXEnUAEk5NBJkBTYIHAgAc2QiZHUlYwgAAxR0bHxicgAeABUAPhSIAHd2JPYIORxLCGQANwTGNBx1HAVWBIgCMUiibsMTVng+vAglVltrXjo4fSNTW01jXnVrJUbyEc0snQA6fwgATQJ+Y1FI62mFCA4cYZLkSM1unQh7HBIlImjSicqAPKDRbjfocJS2YzsT6hH7IPbMdRtGwAGggfCIpl8RGsaIAwiQcFcvKMINYCK93hSiARhvFFLcKXQnqwanFQawKcZiOt7G0fMQEQAJAiPRrqNFkU4Qc79bxKEgkGXQxVxWIQKWrazIEi9Bgygji76-IlVUSMZRiMQJOLDc7a2ymtAEK5KOihA6UbgEdR1AAe7RCyAAXIcUuHJpRWGQ0E8ABoQAC8EAA3pQoH7g6n01BIlmAIw5qB0LMAcnKpZzAF8c2Qy+wrJWoDWozGngBRP2x0wM5Np3MQHbaLaZ7MDqBD7KMHAFouDrRTiAliDlpRN3M1geTt51lcNsjrltQaOxiB5AiEJNIByZYdkHJxgoQYDAMmcXgkMbMsntJ6mlKdt2nR4CklDhqBlBPgAakoyAlJSADiExCjMWbsKwrBoNYwYvpMUJ7AY1h7D60TANAYAgMATigBAAD69EMYxDHHKcvp4heTxCjadFMbxtEQJRTgnk86RoLeU75E+faUNuWwANoANKghAlhSr0eQALpZqpPRnopGn+p0RB4LY8TihAAD8ekKQZWaieJOj5PpBRgC2NF8bxZ5eMMeJEiSHlMQJVFKMEPrDMJqYQO2ACOvCfGigFDBAVYQGI6gEGopZCMJcBQjCapeMAvA+CQ1iVmAEX2iSyZyZQiWmDkMVxSQOT2QujlxvmBQJV2QyKF13V1b1DVNZ8rU3u1uRxgATN1UXDcBs2DRpQlthAnVXv2eaCNIiZPtN030Fm3iJD8lDGFmW1QHgWZ0AQBChKIOYhmO47RJdc5QOwH3juOShZqw6ieJ9uYGGWJ3Guuv2br9Kn1jqJAEFDG5ziQWa1bDe5riiINXbDcjo+WjYrZjVY479JMo82rmraeM2bdtEM-MlEAAD6RcuRCqMyvothF9XAfmm0yZN05ZgIu37YdE6i0ux2A8aIu7FsF2vTLysWrd92PUQOayYwL14+rd4xD9sP6xA31q+bsv-bcQPICDxuLmDK5M9EyMDjDv0W+Y8OKkjc7e7mFto-OGsQBjsOrqW5Ow0b44WwT4cm3JRMHpT0NxwOmfJZQNZ82tAuKNNDMWzOZIK8zKXsymKeLpz3NdG5IA8QF9HoqsHBdAAyp0WFt+3QVgKAkEQD30IvJqvrkiQxXYthlsYVhOHAHh7AEURJFkcAojWI86hjzBcFkg9888mhy-Ybh1j4YRxHqKR0DALP584mPACyPpPHiKqwrEi90KYWvmvW+G974kQolRIAA)

```ts
/* _____________ Your Code Here _____________ */

type DeepReadonly<T> = {
  readonly [K in keyof T]: keyof T[K] extends never ? T[K] : DeepReadonly<T[K]>;
};

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<DeepReadonly<X1>, Expected1>>,
  Expect<Equal<DeepReadonly<X2>, Expected2>>
];

type X1 = {
  a: () => 22;
  b: string;
  c: {
    d: boolean;
    e: {
      g: {
        h: {
          i: true;
          j: "string";
        };
        k: "hello";
      };
      l: [
        "hi",
        {
          m: ["hey"];
        }
      ];
    };
  };
};

type X2 = { a: string } | { b: number };

type Expected1 = {
  readonly a: () => 22;
  readonly b: string;
  readonly c: {
    readonly d: boolean;
    readonly e: {
      readonly g: {
        readonly h: {
          readonly i: true;
          readonly j: "string";
        };
        readonly k: "hello";
      };
      readonly l: readonly [
        "hi",
        {
          readonly m: readonly ["hey"];
        }
      ];
    };
  };
};

type Expected2 = { readonly a: string } | { readonly b: number };
```

[`keyof T[K] extends never` 의 의미](https://stackoverflow.com/questions/68693054/what-is-extends-never-used-for/68693367)

`never`는 타입스크립트의 `bottom type` (모든 타입의 서브 타입이 되는 타입)

```ts
type Hmm<T> = keyof T extends never ? true : false;
type X1 = Hmm<{ a: string }>; // false, "a" is a known key
type X2 = Hmm<{}>; // true, there are no known keys
type X3 = Hmm<object>; // true, there are no known keys
type X4 = Hmm<string>; // false, there are keys like "toUpperCase"
type X5 = Hmm<{ a: string } | { b: string }>; // true, unions with no common keys have no known keys
```

`keyof T[K] extends never` 이 알려진 키가 없는 경우를 의미하기 때문에, 객체이더라도 빈 객체인 경우 true가 나온다.

반면에 `string`과 같이 우리가 생각하는 object 타입이 아니더라도 기본적으로 프로토타입 구조이기 때문에 true가 나오게 된다.
