# 20230705

## [문제]()

```ts
type RequiredByKeys<T, K extends keyof T = keyof T> = Omit<
  Required<Pick<T, K>> & Omit<T, K>,
  never
>;
```

어제의 정답에서 `Parial`을 `Required` 로 변경해주면 되는 문제.
Omit, Pick을 해도 기존에 Optional이었으면, Optional로 분리된다.
