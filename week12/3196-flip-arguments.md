# 20230714

## [문제](https://www.typescriptlang.org/play?ssl=26&ssc=141&pln=24&pc=1#code/PQKgUABBDMCMCcA2CBaCAxANgSwA4QEEAnAcwFcBbAUwDsAXAZ0lRVbeYCMBPCAK2wCGNEgwAWQiAAoAAvyEjxNanQEBKCAGJqAE2yVNA0pVqMwzDRYgBFMlQZ1sAexpmoASQq5MVavQh1RKn8uXCCANyoiBicaCEcAMwhMR20BMQByBggAA1yAfQA6eJxcXOyC1wgAFRCgsqw8YnJfRgAeKoA+MogiKgBHMmxerPiyGgBjB2dg0Jzcqu6hbR6qOjIiGiyBCBoqAHcIUYmp2LpaiD3RbHHRCHEsgKCGAWoVtY2ZoITqiA4yOhWESiVGWuEML1WkQYFWY6EcRAgVAAHi8vFQAFyVMpnUIMcZEPB0Zg4oINXChZYAXgwJSaxnoDFakkMJAADOiIPYCcIADQQFmwDk0SgcSJ8lkAJg5HEcjm8QnUlI6EDCjmw2g6zGAwCkLPZv1l8po4tIgp2IrF-NIUs5dG5JEVytV6uYZUqyoAath9nFYgBxbB0AASZA4HNEdDouAY6O1jBuBV40PhJGAcCQYBAwDMoAgeXzBcLBYgAE1HOsIABhFJBIORIJFxv5iBZswkiAAJSoQIYVDpLVaAAVEUi6LRtFsaFwANoAXWV1OHyLHNAnEGn2Bo8UihD5BX3m+3CIAQrOIAB+TvdqF9owD6f7grHvkEecQDmDtvnMn9kyMqojiua6SI+LIxvyU6OhBXALj8y7jlkIH7mBHKHjug5QWhCIdheUigaQWQcl2Pa3s0JhDsqUE4UK15EDmIB5k2RbVHYAKVmkdiMUxxattgnjwgC7YAN4QAAogMAiYHyolIqEkwQAAvocRCOBQEDpNIJIoDckneMIdjAP82CYAw6RmOMzj2Py740o0d5-ky8SyhyXKbg6EBKuaFCikQsFzl+szjBxWTUtOzAyXJdCtOJZCSa0P72QyTJQTKcpUEIHR8pIKWGulNAdJl4WyVQkzRRJmDxbSiVtJITmOC5dpuVBwreZEmVSHVDX2s1Fq+YVUARSVUUxXFCVkUlzKkPqrm8laJBmi1PkmiQNqpUaUHOhqWV6tKuVCMtC29ctNoze5nmbQVPJgLOAVBJEKlRB565ajqmkMCgyKRR9RAPbCVXjW0mSNcI6T9RA2oQG9H3FZM32-VAY30m0IkANZUFwHLpGEkm2OkilgxDUOfUNcPwn9dkA4y07pAI5LeOkfLpBwQgswzECwKyrJ8iJAgcrAinzldUCE4w0NffdZMI-9SOMsKmCYBAAA+EBjNoVDxJuIKFTdYC5txhYYOsjwIgAymO0ZcfrLbZqAzDKib4i9BAXDlgiDBykZlnhpG0axsA8aiImyakGmCCIMAQgMHskR2xAXo+u7mCe5s3tRjGcZ4oHSYFCmodIMAifJ0wUDKgAsvCQSVuI8u0CQdip77GcJtnKaZtmQA)

```ts
type FlipArguments<T extends (...args: any) => any> = T extends (
  ...args: infer P
) => infer R
  ? (...args: P) => R
  : never;
```

```ts
type ReverseArgument<P extends any[]> = P extends [infer A, ...infer B]
  ? ReverseArgument<[...B, A]>
  : P;

type FlipArguments<T extends (...args: any) => any> = T extends (
  ...args: infer P
) => infer R
  ? (...args: ReverseArgument<P>) => R
  : never;
```

never[]로 인식됨..

`ReverseArgument<[...B, A]>` 를 `[...ReverseArgument<B>, A]` 로 수정

```ts
type ReverseArgument<P extends any[]> = P extends [infer A, ...infer B]
  ? [...ReverseArgument<B>, A]
  : P;

type FlipArguments<T extends (...args: any) => any> = T extends (
  ...args: infer P
) => infer R
  ? (...args: ReverseArgument<P>) => R
  : never;
```

# 20230725

## [문제](https://www.typescriptlang.org/play?ssl=35&ssc=1&pln=24&pc=1#code/PQKgUABBDMBMAs0IFoIDEA2BDALjgpgHYAi+ADjgBaQrJ300BGAnhAFYCWWhA5gM6VuEABQABTt36DCAW3w4sASggBiOQBMOAVxmqsAJ31ZmYGivMQAilvx8cHAPaFTUAEr4Axlv18OAN3wMVgAzbDwiCAMjVi0yCBwHCHVyKniOOT4AOhd0B30IfAAPLBkyDHwALhyAA1qcZjJbD30OChp6xsiIAF50MIISFMoAHgBtAEYAGghYadHoafgAXTnR0YBWJa2VmYA+CGBgCAnp2ZhFuc2lzIhQ3AJ9Qhm0jPaG-AhGHr77olIKEYnGZzBYQZarDbbJb7Q7HKbA85g1ZXa4Qf6pZLBLBaDA4PjxRKMD7jGi1ao5ACSwXilA+yQBEA4+LI+gcfg4yXU0w4OAA5PieFoDNwCPh1ATPh8yA5fPYAozCAQePh9NkaPsAGocfAAdwgTggAHEeQAJLSMCoQSh4Mh8CqHPEeSiZNhZPI8YBwRBgEDAUygCAAfWDIdDIYgAE0HN4IABhBzJCAmlUfMNp4MQX2mDofTC-QYA4Y0AAqBUKA3U+O4zFGKxoAGUyxX8YQdET8r0pjQAKpNoiVyKEGtLb61sD7Xrd0a88q8Ki8kdFZsQes0AD8EGLNEtpaX-fxow4hGCKvQ00yF6PJ-yriW6-QfcIA+rY6gUA3owvmTz4QLVGGaDTPWcxft20y8tWEB+FgGA2BAHhCESkTqJyC67OeF4-gM6IjK4QHTN2ux3m+ECWqMgEQF+WF-EMwx4SuBFEdum6mGAAbpmmm62DgcZYHwthBhxoaZn66TSvoPE5hAADeEAAKIAI5Chg0xyYUjQeDxAC+tysrovKiDmyBOjBs7KnwwBaPYGB8Ly2bvPBfECb0ow0GpGk4MMinKQB-Q0YWtbocc0LoW56meJ53kwb5+Y4WM8JnKCyxBUCiWLCFkxhR5XlKdF1F-oC8KjLAWwpQlGVZRFOU+flcWpSC6UQiiOywGVpzTEllylaFUDuVVUUYDFv51QlDVgjsayQtsbUIp1xxTRVvXhZp1V5X5BXxXMZzzHM8BdVCHUzWlSLHFcuw9fJy2Rblg21bRQLFWNox7adUI7OMACcsAAGwAAwABzjAA7EdHUXBAmznZld5sSAglCRmaDeFQp71gQtrwwjImw+qK6CPoHzMNG+R8A4sH2E4dpWjadoOnwToum6+gel60DANwfA6iquNarqECk+TjiEFT1o4La9rAI6zqupk7qeggbMC1ZQt8LjACyeQfLGggYGZtiWqL4t0wzMvuj6fpAA)

```ts
type FlattenDepth<
  T extends any[],
  S extends number = 1,
  U extends any[] = []
> = U["length"] extends S
  ? T
  : T extends [infer F, ...infer R]
  ? F extends any[]
    ? [
        ...FlattenDepth<F, S, [...U, "any value can be added"]>,
        ...FlattenDepth<R, S, U>
      ]
    : [F, ...FlattenDepth<R, S, U>]
  : T;
```

길이를 어떻게 줄이고 늘리지 고민했는데, length를 이용해 다루는 방법이 있었다.

```ts
S extends number = 1
U extends any[]

// 같은 경우 늘리고 다른 경우 줄이기
U['length'] extends S ?
  // 늘리기
  [...U, 'add length']
  // 줄이기
  : U extends [infer A, ...infer R] ? [...R] : [] // 배열 내용이 아무것도 없으면 length = 0

```
