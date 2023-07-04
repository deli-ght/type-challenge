# 20230704

## [문제]()

```ts
type PartialByKeys<T, U extends keyof T = keyof T> = Omit<
  Partial<Pick<T, U>> & Omit<T, U>,
  never
>;

// Partial<{ [key in keyof T as key extends K ? K : never] +?: T[key] }> & Omit<T, K>

// Partial<{ [key in keyof T] : T[key]}> & Omit<T, K>

// {[Key in keyof T as Key extends K ? (Key | never) : Key] : T[Key] }
```
