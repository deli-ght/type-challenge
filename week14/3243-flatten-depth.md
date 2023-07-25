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
