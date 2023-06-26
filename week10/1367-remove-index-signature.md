# 20230626

## [문제](https://www.typescriptlang.org/play?ssl=31&ssc=1&pln=28&pc=1#code/PQKgUABBCMDMBsB2CBaCAlApgWwPYDdMIBJAOwBNMAPCAZQEsBzUgQwBcBXAJ00lRQGC+AIwCeEABb0uuUSwj16ALw4BreQAoAAlJlzFK9QEoIAYmyZy9DtjO5hAK0wBjNilWZRAZzB9T-iABFDkwvNnpcUl8oYmwABwAbHExSNggAAyw8QjJKKgZmdm5MAB4AFQA+dIgAGghqZwSOSgg2CSJ6CmoILyZWTh4IADMZW3snV1bRONCAOmiIADFcLnqqFnikgC4F9L22Hz42aaJl3AgAXggAbz4oAG0PUS2eti5OxgBdF5ZSUQBuO7DXC4DRGF74XD0ciAqAAXwWxxmEAAgpcMDgCJhctQCv1iiUzhUoMBgGsZq5LDdgaDwRBIdCIAi+Ht0gtiQA1eiYADuEEiEAA4vQ2AAJDjCF4SNhsOJeLakg7OCSzBxeWYrRjAOBIMAgYC+UAQAD6prN5rNEAAmrhuBAAMK4FqizCDC3u00QfW+JFELJYnH5PpFHjlYlXW4PADSClIECeuCGEDKEBYXle71IjDWbBS5HTMYA-BBSJhCKsXqQbMJXTm8wWIMXS+WIC8o99k-d22BmUaPe7k6E0va06ETf3zV6DfR4is0r7qQBRACOHBYCTqi6oFLScOGowgAHItL6UMr10ks6FgBxwgkvIefScliD0ZGII9PC8wpmvj8-nwQwgmCEJQuQPZPsiABCLCrBGfCfs8JbVq6Ha-KIIiwSB9JgXwAAM35vB8EFgM4kRhDSwiweitCiNgwi4AkGiHkB9iwYeRhgAuZwwXBNwIU8350QxCRoQBDysVRXCfNhDLgcyC4wUob6YVwsm4VAVFKIRv4kWRpAUfILz+jkXRBoUAylESb6sep0JwoCXHPs4o7plc9x8FuO4lCua4JCUJnYmZeIhlZIIVHU1w0nZ5BMhUEWeduLhsD5q7rgFmKmXkIWWSUvERdSUkxf8EAERmHxxQlUBeclqV+Rl2RBdlwa5TxsEFVF9ySbBMl0nJlU1Il3m+elgWBjlBJKR1EBFX1YElVpOkVXC8WDZ8hogOOE6eos3BtLWtC5nKW3bVOYCgHwxK0BIsFEKItqrF4jG3hEBlSjKcoKsASoqmqGpcFqOqIMAvxeDyrqXRAXK8j0z3hOR72yvKipeMqqrqpq2oIMDT1NPDBmQwAsisRD2jdCSXowoSI59KNo39mp6gaQA)

```ts
type RemoveIndexSignature<T, P = PropertyKey> = {
  [K in keyof T as P extends K ? never : K extends P ? K : never]: T[K];
};
```

```ts
type RemoveIndexSignature<T> = {
  [K in keyof T as string extends K
    ? never
    : number extends K
    ? never
    : symbol extends K
    ? never
    : K]: T[K];
};
```

```ts
/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type Foo = {
  [key: string]: any
  foo(): void
}

type Bar = {
  [key: number]: any
  bar(): void
  0: string
}

const foobar = Symbol('foobar')
type FooBar = {
  [key: symbol]: any
  [foobar](): void
}

type Baz = {
  bar(): void
  baz: string
}

const a : RemoveIndexSignature<Foo> = {foo(): void};

type cases = [
  Expect<Equal<RemoveIndexSignature<Foo>, { foo(): void }>>,
  Expect<Equal<RemoveIndexSignature<Bar>, { bar(): void; 0: string }>>,
  Expect<Equal<RemoveIndexSignature<FooBar>, { [foobar](): void }>>,
  Expect<Equal<RemoveIndexSignature<Baz>, { bar(): void; baz: string }>>,
]
```

너무 어려운 문제..ㅠㅠ
