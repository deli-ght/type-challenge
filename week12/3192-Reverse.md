# 20230713

## [문제](https://www.typescriptlang.org/play?ssl=22&ssc=96&pln=22&pc=1#code/PQKgUABBDMCMCcAmCBaCAlApgN0wJwGdNJUUzySAjATwgCsBLAQwDsBzAgC1YgAoABRqw7cWAW0wAXJgEoIAYgkATBgFcxCyaoAOAG2Il5RiAEVVmApIYB7FmBIBJMXswSWkiJM6ZP1bT9xCGxYIawAzCAADaIBBPDwmagA6PBx8ImjI+ygAMWs8CEwADyZnfQAubKjoyT8LAGM8Bm1JElr-CCYIAF4MNMJMAB4AbQByJlGAGghRylGAXQA+CGBgCDG56fGFtrqISh6+wKIR7a3NmfqF5dX10avzqZmJ+ZJMquWANQZMAHdQkIAcQYkgAEqpKOUIJxJJJtARyqtJAR6pwknQCEl8mxgHAkGAQMB7KAIAB9ckUykUiAATWsqgKAGFrEofKD8D4qVzyRBCfZ2j4sMchgAVZa9EWFIqSTAsJQEdbzCAAfkVEChkuKMrlCuGDBYYXwEBi0ySZv1hoKACElarhmakkL0kMrYtpjElVDhq8wCTuVyICKLB5GUwiAr-VTeUSGM58h4BRAAN4QACiAEdVExdNNU0V-PUPABfCBhPDWDSjfgClCo7P6dgWYCqKy6Aijfl7ephiyHYYkPMFySDDNZ3SDJ0DEZLabexZugf5zCFkeZ7MT-onMYTR4zu4XbZLBdQQfL4ej9eTrdnGYHq57sYPW9PQ-zyZgH2J-Dlwh9ki3asCBQYoh2A+J8hIK8hlGSwmnYUZjxWNZAOApdCzAn9IM3IYUwAa0wagoVGbBs3MUYICLBcfT9SNqRyBkvCNABlGV4TJWieT5UASGWJjuFSCBqHpAoCGsXQW2CBFoVheFEWAZFUXRTFsVxBBEGAVgCF+fAeIgb4-ggUTxKsWwpJhOEESRFE0QxLE8BxPF1KMiTTN0gBZfIfEZbhdAbNgLChczZKsxTbOxAkiSAA)

```ts
type Reverse<T> = T extends []
  ? []
  : T extends [infer A, ...infer B]
  ? [...Reverse<B>, A]
  : [];
```

```ts
T extends []
  ? []
```

이 부분을 단축시킬 방법이 없으려나..

```ts
type Reverse<T> = T extends []
  ? T
  : T extends [infer A, ...infer B]
  ? [...Reverse<B>, A]
  : T;
```

```ts
type Reverse<T> = T extends [infer A, ...infer B] ? [...Reverse<B>, A] : T;
```

엥 그냥 이렇게 해도 안터짐

```Ts
type Reverse<T extends any[]> = T extends [infer F, ...infer Rest] ? [...Reverse<Rest>, F] : T;
```
