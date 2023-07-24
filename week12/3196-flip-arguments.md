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
