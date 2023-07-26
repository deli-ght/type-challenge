# 20230726

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBDM0EwDYIFoICECiBZCBnALgJ4A2ApnvgE4CWAdgOaQrIutMBGhEAygPYMALWhAAUAAVz96QuLACUEAMQBbUgBNqAV2VL8pZQAdiAQz3Ji1PZWPElm2tX67NR0mCaLPEAIqbSBR1p3KAAVAXI0Yl4AYwBrABoIDDJVWnxErF4NADNqUkoIVXwBLN4o+i4RTCwFalwIYwgDXgNNEwLaY2U6egho-gA3UjTAiGzeAuiTXFx-CDoIAGFubgA6YIgAMQmIUgAPLtdE4vJ2KLi+3kN+YfwIAHdeNrUIdnJKUgMP2bT1BvqAAbsfC0AGJUgpW4QYqmCBqT7DNT1FxOE6vc6xB5PYgvN4QD5ffy3P7GQHA2gAfQpX2o0VIYMKWWouXy0IEsOi7IYczRBBI5F42TZpwxWOer3en2+xJepIgQJBLHY1HoAIgOwVlOpNDpLHuxkoDgYAPWTAAkoZIWl5dUADxoRIYDIAPjV9wEtIEEHow3ypnIBBoDAg9lG2UoV2FszZH3IBgNXVIVlwqwgAHVwh8bWq6g0KEHehYrDZEgCMGrjLQXgCsBWs4Geg1KNZCPURNFKxLdoYiHJTVBnRAAGp5e7q4QAcUsAAlNOwAFwQAT4fAGXDz4DAfC4TmrABWKYm9GAsEQYBAwHcoAgVNvd7vEAAmk8CossuRp-lyPef1SIBf3CIAwImwe1dj2PQq3qBsGEdcDIKRfMegAbQAXQyeDEWgqgUNQwcAF55QAEgAbzQABfUiMEwqCIDQiAAH4IAAcmYiBFwBKkqOQ2htDeShUPIgFKJInB9gQ+p6KY1j2PlFhSKwHi+PyQThIBK8QBvX97wgEJ-DuRZSTmbSdIA6hrkoO4gPIEikgAR00Eskj2YDojucixgjHRmLEazkE5GwyG5XBgE0fBqGIXBmMAwhgL6Iz6kI5CmAwFzSDc20MAcmx7VA5jyWYxJkOYmk6WY9C6LwxJ8pBKlStIZjnWdeIUrSjKssc4hcqwW0atoQq6JKnUGoq4r9UNHoBuY3BNGiOkZnK5qWPJOrhr1A0jXoNiAB9ltq7VaVIFgZrm-woogJqWqgVLXPwTLsq6u0+oGtCium5RAqm1QNG0Kb2h9RbqvJY6PuIYgdr22gWG+rRlAhvqWH+hqLuasBUI0rSTL-TZNEszMeD0NdMax-9L1AJhB24dks0IF88DKMLAnXJcVzXDctx3AR90PShj1PBBgErXB7nyCnh1HeniEZ-hmeXVd103bddwPVYjxPeABckKXwplsXMizRZ2TB4YfVl1mFY55WecYACgA)

```ts
type BEM<B extends string, E extends string[], M extends string[]> = `${B}${E extends [] ? '' : `__${E[number]}`}${M extends [] ? '' : `--${M[number]}`}`

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type cases = [
  Expect<Equal<BEM<'btn', ['price'], []>, 'btn__price'>>,
  Expect<Equal<BEM<'btn', ['price'], ['warning', 'success']>, 'btn__price--warning' | 'btn__price--success' >>,
  Expect<Equal<BEM<'btn', [], ['small', 'medium', 'large']>, 'btn--small' | 'btn--medium' | 'btn--large' >>,
```
