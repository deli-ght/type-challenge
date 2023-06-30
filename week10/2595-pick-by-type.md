# 20230629

## [문제](https://www.typescriptlang.org/play?ssl=26&ssc=41&pln=26&pc=58#code/PQKgUABBBMCsCcsIFoIAUCWBjA1gIQE8AVAgBwFNIVkbaqAjAiAKwwEMA7AcwGcALThAAUAAVadeAjgFtyAFzYBKCAGJZAEwwBXaaoD29ZuSxywVFRYgBFLeR5yMejmagAxAE57dAAyLeANBCk2DgQbBA88hB6AGZBnhTuDnYQAO58epEQcmTkYe55bDw8GFwcbPQANnlyehDeAKreAHQuEK567hAAogAebNKk1W3eozkUPFjuGKSmUON5APIclQR4enrVggC86CGEJBQAPADeVFDlsgBcEXLT3OcQWHpaHHI3HDr05O6PGDwAJXIbHUTlWN3oGy2zigUH+3XKVXIEKhwJhEAAvoFIZs0QA+CDAYAQE4Qf5AkFgggo3GcADcZJ4CIq1Rp0IZGKoo28bQJADUMORUtEOBAAOIYOQACS09BufDkclIPCuRLkkz4zWYPGanS4wDgiDAIGAZlAEAA+lbrTbrRAAJovLoAYT06jyUp+eVtPqtEBNZgWe1wB1yRyIgQaBN2pIA2gBpMminDkAixCBEMI8DMJgC6EHIvTk5A46mzDQgAH4IImPuQAG4-fM3CucsDm30+jN2OQQZ1FFKd23+00YQadXtB0ndACOWjYlUCfQoJkxEBinl0AHIRAtkFgBJVqtw7MAtA5Kjwt2YMG8fjE2Fg8gBZN3kSokqiXZG3e5cKjPK87wQJ80jfL8cKAsCoIrNSEA4tCVDwoirLwainBgG2QZYAO2a7LGVDLsYchHLO86VEcmAhsQYavu6i5obSHB4oEpLktBVJsmiDLISyP4IWimJ4ixhG9CuJFkQulH7DRxx0e+gT2H+LEkiBAw-kpt5cEJIlQERJikXOUlUfgsnkEc8kMaB4EqaSgFvB8Xw-Dp-hgLmZogJaQ52q4WhJHwzkAMrFsqXneRaI7tuAUAEoFAgFBAaZ+REmzno4HAqhACpKiqaoalqOp6gaCCwMAnA8KkPxUPygrCjwqUOE4mXZcqqrAOqB4Fbq7j6oapX1ZUaVNdVECvglzqHseXB2PKiqtXlnXat1-4BkAA)

```ts
type PickByType<T, U> = { [K in keyof T]: T[K] extends U ? T[K] : never };
```

-> { isReadonly: any; isEnable: any } 로 리턴되는 문제

```ts
type PickByType<T, U> = { [K in keyof T as T[K] extends U ? K : never]: U };
```

type assertion을 어떻게 사용해야하는가.
`as T[K] extends U`
