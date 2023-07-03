# 20230703

## [문제](https://www.typescriptlang.org/play?ssl=35&ssc=2&pln=22&pc=1#code/PQKgUABBBMBsCcBmCBaCBRAdgEwM4HUBLAFwAtJUUrqKAjATwgCtCBDTAc11PYgAoAAi3ZcemALYBTYqwCUEAMRTshAK7jFxSeIAOAG1ZaUekpIBOrPWAoLbEAIqrJuYoQD2ma1ACSuvdslMYggAAyw8IjIAHgAVABoIAFUAPhCIAHdSQgBjUggZAGtnfPS3CEkAD1Zs4JczQk58+h1i9mwIM2lVM0xcDNJpAbNQmLTAvAySPJDEkK8IADE3YcrWP0kALnmQneJm52z6nWIKPZaIVggAXgwcAimogHJWWmzHhMfXx+SIYGByiotGqSdrEMq0ST5MxOU77CC0a63CIPZ5fD4vN4-P4AoFaUHgyHEaGSWHnbKI8L3aKot4fbDfX7-Sq4kH5AkQABmllwJKgOzmFB+ADVCJJ0hAPBAAOIkAASqloGwgpGIxB0uA2f2IuFyADomLhdcsOMA4EgwCBgNZQBAAPr2h2Oh0QACabm6EAAwm5sJDZeZIU6g-aIJbrGdIZTIqRYgCtHcIHUGhwEok4+M+knOD8bjF0wmQgASADeDQ55kWAF8S4lK2kAPxQpwQJVcvQ860gO3Bp0QGLOYKe1g8vo93thwi6ZbBCMQYsYACOqksCXQgMkNQglc5ZjcGkeAgjKFyln8nGcwFUrnbj3DcOyw+KNwA2hQ17iougl5ZP3do08MXeCBPkxBIiScZJkjiN91xqT9vz0X9kWpQD0S+KCm0kSDoKgd8N2IeDl0QqMUVQ4D6QwtseWwmCPy-IikKpGMaSA55QM5bksKg2j8MIn8SJQtFgO+MDiRo3DYII+j+L-UihMeYDKM4miAF1O27McQwWboyArABlLR1Q0zTQytUBBQgPSeE6CB6HdYZcDcPQr3cXolRVNUNS1HVSH1Q1jVNBBEGAdhcHScwLJFMVEyclyPA1ZVVXVTVgG1PUDSNMwTTNYLHOc1x4osgBZZZIU9Hg9DPDhnHcpKvNSny-MyjgLStIA)

```ts
type EndsWith<T extends string, U extends string> = T extends `${infer F}${U}`
  ? true
  : false;

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<EndsWith<"abc", "bc">, true>>,
  Expect<Equal<EndsWith<"abc", "abc">, true>>,
  Expect<Equal<EndsWith<"abc", "d">, false>>,
  Expect<Equal<EndsWith<"abc", "ac">, false>>,
  Expect<Equal<EndsWith<"abc", "">, true>>,
  Expect<Equal<EndsWith<"abc", " ">, false>>
];
```
