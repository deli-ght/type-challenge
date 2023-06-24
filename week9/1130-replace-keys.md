# 20230623

## [문제](https://www.typescriptlang.org/play?ssl=47&ssc=16&pln=47&pc=20#code/PQKgUABBCM0MwAYIFoICUCmAHANgQwGMMBpDATwGdIVla7qAjMiQRliWIAKAARwFcd8TAFa8AdhgCUEAMQBbDABMAlr1kyA9gyEYCAF2QBrclWrSzEAIq8MFXUvWiw1AJKzcGeaN0Q8EXWSwMdGx8IlJKABo-AAs8bwAnEMIgo0oIJVEIMXtM-0CKKKUAMwgKdXk-AKDYighRdW9daKVa1KiRW1KDJSwIRNxCDIBzCOoAQUrAvzwjWqbEoLx4odUMLwoAOidqADF1eIgMAA88NxwMAC4nKAADO90qKDyggDl1BQwJgF4IAG9qJ5VC4QADkYxBALqp0upV08WGkKK+CGwNEqgYGHi1AAvtdJq93hgAEIQH7-KCAwLAkFEiEU9IKVHozGI5FM2QYrFQXHUZ4QN4fADCpL+kOe1MFdIpomhwNs8NEQ1ZeBRdWZXIgPN5VX5hNqPwFnwgAB9dR8SabDYK8XzMAMiApDfrgvaSMYADxOqIgmXyEEm0FIlUgqK-X0wtEczFRIOq+XDbEAPggwGAf3FoPBUXD7M5MbZsIVQ2xAd+GZpIYZuejEFjcrhCdL5cl2dlaqj8XzKvrRZLqYgAHd1PwFH0kkQoRUivFyoXhn51O282PXbXkbWZ2pI5yF3PFVttVM7aFFG9dABRI4tXThZ3H5K3z1673hyu-PB4avxJMptNloGZpWOZ1BgABuNZ1kumIlpahIWumAEgi2k4RmBEEFtu0G-oOw44KO-Qnihu7iOBGp3DceLJgAakoGADhADgQAA4kougABK8AwwLRLouhYBQFypg8BDRBsQibPsQzALAiBgCAwBOKAEAAPqqWp6lqRAACaw4HIKhIQGxmJBBppmqRA8lOLa45upQ7oAKpRAAKocRy6GsCi1PGioBphBymhQZAcuoOBRFpyZktQADaxDpJkqTqCUHAAPKyKxDnOcmppaRIAC6EDUMCsXHO5oieRACUlKl6WORATnJgA-BA1W6BldWJjF+WFRAxVuR5rTkIl2kQE1WmdRAqJoRqPJKWZpl1TY3iCngFA2Cpc3qRZClKG4+yNDqvwQOeACOvB4KFR1HIEeiahus4glwzzICJ53nIqNjALwdg4BQEJgHyhrfKKlIwmCUrAd5SpQJBflgDyANwSK5L4tStLUEojJQRqMPqnDVk6laSOHqDkrUBDDaKtQOMdnj-06veDqA0TIPUuCZNtrD0MFpDtPWa6jqI5FLOgmjUAY1+VPcxTSrw-TNkC0KzMo6CpNQMBnNrt2e4y-jUxvC80JM0Lytg5LWsa+rU28wT6gG-IhPG82UrU5y7PyJNpHW3reoikzsHmgGVp00e8tOiKDOnoSEymhHCvEgGsdBwjHwUPr0K+7bhtR4Hmf24Swr+8SutBAQK1rT8UXUJe12tSdZ04O6EePl6oKvgGIKxm+KFfgA3JrcbS5qiZRIneqJsPVdXTotenedjc2c3z6t9CXcfl+Q9RE6afyOPoy5YpIDrRt5k7Lw8RNJiEAAMrufxR-H1tYCgNQyZX7EiQQGQumlCFX05AJEAeJ8QEkJCgIkxISWWNJeACBgB4FEBQAcLIoDUVovRMofA7AOAAUA-iglgDCVEuJDYkloGIGABgv+2CX4QAALL7CCIKWIAg1hDBsNxXieDQHgOIZJOSCkgA)

```ts
type ReplaceKeys<U, T extends string | number | symbol, Y> = {
  [K in keyof (Omit<U, T> | Y)] 
  : K extends keyof Omit<U, T> ? Omit<U, T>[K] 
  : K extends keyof Y ? Y[K] : never
  }
```

-> 문제 잘못 이해함

```ts
type ReplaceKeys<U, T extends string | number | symbol, Y> = {
  [K in keyof U] 
  : K extends T
    ? K extends keyof Y ? Y[K] : never
    : U[K]
  }
```

결과값을 어디서 분기처리해야하나 조금 헷갈렸는데, 예시 생각하면서 단계별로 고민하니깐 쉽게 풀린 문제