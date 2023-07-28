# 20230711

## [문제](https://www.typescriptlang.org/play?ssl=21&ssc=62&pln=21&pc=1#code/PQKgUABBDMAMBsAmCBaCBlAFgSwGYBdJUUTSiAjATwgCtsBDAOwHMBnTJiACgAE6m2HRgFsApvnoBKCAGIxAE2wBXYbPoAndfUpgiM-RACKS0a3zYA9o11QAksIAOAG1FjG+CPkyjPlBz4A3UXVWS0YIC1wIAANYgEFNbQA6djx8WOibCAAxC3UIUQAPekcXLIz8P1MAY3VsB0IoSv8IACVTJScPAF4MHAIAHgBtaAAaCERxgEYAXQA+CGBgCCHJiFmiDKyFgDVsUQB3CPCAcWx8AAklcgAuCEx8fAdWG6X8VmrMJJpWJLzmYBwJBgEDAXSgCAAfWhMNhMIgAE0LEp8gBhCzyHwXYI+OF46EQUG6Zo+LBpAYAFQWvQpBUK+FEjHkrBW2EYuGCEDi4ySvLZHPyACEZhAAPwrXlJYUQO5DGa6apWMwQegyvrkkbjNazakrbXyiH4vEQCmmDyo+isUxQo2wwlg7COPIeEkQADeEAAogBHJT0JzjT2FfzVDwAXwguHUFlUAHIeCSUJ9-S4WKZgEpzE5WLHiVUINVLdbekMiEsIAnWCgiiH8NXNHkiGTBkpGABrRgWA6MOajIhB2sDH1+pwDZv4YbzcZyua9-vB0Shoe+-1j-oToY66fzOdQAeLifD1fj4ZjCbTKd6i+zvt7hdLo+jk9DWP0WPjWPkd8QWPVb+x+RY0vF8vw-P8P0Anc+3lMBDVteFshRLxOXQBlnhteDIXtWDwCgBYsA0HxKGRfJWAsJxMzCF57keZ5XmAd5Pm+X5-kBBBEGAJhWAOYIiF2fYjjIijzCVO4HieF43g+L4fj+dQASBDihMopU+IgABZPIfFRDgnFTZhTDE2jJIY6TmLk5gQTBIA)

```ts
type Shift<T> = T extends [infer A, ...infer B] ? [...B] : [];
```

spread 잊지 말기!