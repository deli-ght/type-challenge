# 20230807

## [문제](https://www.typescriptlang.org/play?ssl=27&ssc=1&pln=21&pc=1#code/PQKgUABBAs0JxwgWggYQBYFcB2BrSySRxBARgJ4SC1DIFcMgrQyCHDBAI4CWAhtgB6sQAUAATaceABmgBGUQEoIAYgC2AUwAmrTAvkAXTAAcANkrAE5piAEVMSgM5bWAe2zGoAEXsRy9zBFzZ7AdwgAA317FXZrdCCAfmCMHFwgiFZrCHYIADclACdKTGslADNMfQhi7ABjO0dk7GStABoIP0DDLQByVNYFAyVlbC16gDoCIPi8AB4AFSaAOQA+JPYKiqVdLVStf3dspWZMVl2VCC1yXSUIXXZs9mUtHOsmrXQLoKmkhXzB0gv0oJ1ekEmpxjs9XrMPl8ID80nUgqwBkoAOY5CDzAC8EiCzmCQX+1gIp3OECUXF0Egg6LQWEmAG0JE0AExNADMAF0mfMIMBgCSyUoqqoTu4YbT6UyORBaey2YSzhdSbpGZTqQkJuKIMyIOymtAuTy+edBaCRRcxQzNay2bKoESFWSWSrxrh1RatTqIBJ9bzFQL7iboWb6ZLaYyQzLRnicVyAGqsJSBGoAcVYWgAEphSAAuCDoLRaXTWLM8jYVdBDABW1iG9mySOAsAQYBAwGMoAgAH0u92e92IABNLzZNBhC5pnIXXtTrsQFtgO2qyZTPn3bAqVKcci0yWzFdKNepbAaH7ZJoAZX87F0e4PsK3bJV2656LAF6vtPahmwSOe7QfpNXdcIFmAhYlpN9dCaIZoOdaY5nmG0IBzZcAP3IDaQRQpUQAaSg6DMNRAAZRCoFiWDCLmJpaWgoYIKabC2XmAgoBzCCb3Qh9YjYnNwMvXRZTbEBO2nXsICmGxBlQCIbGEkS+znbpdFrQYFwAbwgABRfZ2H0JoNP5KoIAAXzKbJ7E0doBDtJAyx0r8UWsYBMDsfRrHaYwFwqaTUipWkCH0o0tAmLTMB0iZYO3JovSoxj5gafyDKCkKwoit0rSiuKpWDKiwyomV5jihLAuC7T9HCmkXQ1d1JUZTLzQlPLrQK+KoACv0StCsrUqZVldRquqqvDPrYpazTEo6lKKtdHrtT6poAFYBrS2aYCawrWvG5KuqmjUtGyKwZsKHSCn6qjdv2pQQy1I7XMukawAE9s5J7CAADFMGyMFhzPe5C1k57Z1bUACC5M90GuC5PA+iBrHsfRnIcbAi1zfNC2LYBS3LKsazrBt4DgYBOGsfwchBiA4wTGG4YRxxkbzAsixLawy0rata3rRsCdh+HqiRsmAFlawuDA7P3Byc3ptGmZZ7H2ebVsgA)

```ts
type Chunk<
  T extends any[],
  N extends number,
  Swap extends any[] = []
> = Swap["length"] extends N
  ? [Swap, ...Chunk<T, N>]
  : T extends [infer K, ...infer L]
  ? Chunk<L, N, [...Swap, K]>
  : Swap extends []
  ? Swap
  : [Swap];
```

넘 어렵다..