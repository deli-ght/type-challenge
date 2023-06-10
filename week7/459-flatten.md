# 20230609

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBAsCsCcEC0EBiAbAhgF2wUwDtJklSziAjATwgC8ALAewFcqBLAWzYIHMIAKAAIBjehQBOjAJQQAxBzwATNsw5zM48Ziphis-RACKzPAGdsbRkWIBJAhGz02piKMzp0hHngA0EKiwQAO4s6IoQBHhKDozB4mz4EJgOVAAOeA70OA6YANZmSfYaWjSYBOF4XLjRjhkAZljVRZraKekAdLpQqIziEHgAHpgcqZ4AXF0QAAYz2KbE2Gn1jfj2ALxoK4QAPADaAIx+AEx+uwDMftAAuqe7u7BXj1cAfBDAwBAHx34XMH4PxBmU0mrwAamw8EEIFYIABxBIACWYFDGEHouFSpjG7zmonaACtTO1ejxgHB4GAQMBdKAIAB9BmMpmMiAATRYfQAwoxFBkEXhxBlmcKGRAqbpFulNjhVtsAIL9AarRQuXZXCCvDYKwbK1XcOoCiAAIT8+sNnPVxAA-MbFbrPpaoFAbRBOXbCCqHRBiE6IDbdhgZTsjc8-IGmttOc9Hb6IKiA1sCNsQ34Ld7fai3TqPaqY87PibpRGo3moPHC2maSB6SLmRAACpmbCuzCmAq1uvizipXrNyUZADeEAAogBHZjuPzDgbpYTNgC+EDqkjUAHJBP2kG4PF4zMBmBZ0KZV7pw7Kvp8jo9nhKlq5WwUNrtiNPZ9htmOJ+htmedmrQw6zyhi+M54HOH7ju4P6JnshwQCcEC-NcAEXghSEvMBUCvmB76flBv5JheuxXi8pxwVeQE+CBb4QV+0FBoR5GnOhtz3E8pGfExiGXP8GFUVhoHgXh34EXsQ51IwjCoquFAaKuADc8GovsAAMEDzn4q4SYwsniKuHG7OJknSbpClKRAqnqZp2mmXxYBXDSHwbqYSCDG+rmaL0YD9v0nl9Bsomrvsq43mAtIdkyaDMOItR9AAyvgmI1hFdJitSoDEK8cVZIK-gchApiMOgB6WAQWJohiWI4qYeKEsS4ikuSwBlKYQQCplEDgpCBVFSVVjlei2CYtiwC4vQBJEiSZIIMAhXFRY-UdQAsr0GSclkO68GYqKDcN1W1ZNDWUtSQA)

```ts
type Flatten<A> = A extends [infer B, infer C] 
  ? B extends [] 
    ?  C extends [] 
      ? [Flatten<B>, Flatten<C>] 
      : [Flatten<B>, C] 
    : C extends [] 
    ? [B, Flatten<C>] 
     : [B, C]
  : A

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from '@type-challenges/utils'

type cases = [
  Expect<Equal<Flatten<[]>, []>>,
  Expect<Equal<Flatten<[1, 2, 3, 4]>, [1, 2, 3, 4]>>,
  Expect<Equal<Flatten<[1, [2]]>, [1, 2]>>, ❌
  Expect<Equal<Flatten<[1, 2, [3, 4], [[[5]]]]>, [1, 2, 3, 4, 5]>>, ❌
  Expect<Equal<Flatten<[{ foo: 'bar'; 2: 10 }, 'foobar']>, [{ foo: 'bar'; 2: 10 }, 'foobar']>>, 
]
```

```ts
type Flatten<A> = A extends [infer B, ...infer C] 
  ? B extends [] 
    ? [...Flatten<B>, ...Flatten<C>] 
    :  [B, ...Flatten<C>] 
  : A

/* _____________ Test Cases _____________ */
import { Equal, Expect } from "@type-challenges/utils"

const a: Flatten<[1, [2]]> = [1, 2]

type cases = [
  Expect<Equal<Flatten<[]>, []>>,
  Expect<Equal<Flatten<[1, 2, 3, 4]>, [1, 2, 3, 4]>>,
  Expect<Equal<Flatten<[1, [2]]>, [1, 2]>>,
  Expect<Equal<Flatten<[1, 2, [3, 4], [[[5]]]]>, [1, 2, 3, 4, 5]>>,
  Expect<Equal<Flatten<[{ foo: 'bar'; 2: 10 }, 'foobar']>, [{ foo: 'bar'; 2: 10 }, 'foobar']>>,
]
```

```ts
type Flatten<T> = T extends []
  ? [] 
  : T extends [infer First, ...infer Rest]
    ? [...Flatten<First>, ...Flatten<Rest>]
    : [T]

    
/* _____________ Test Cases _____________ */
import { Equal, Expect } from "@type-challenges/utils"

const a: Flatten<[1, [2]]> = [1, 2]

type cases = [
  Expect<Equal<Flatten<[]>, []>>,
  Expect<Equal<Flatten<[1, 2, 3, 4]>, [1, 2, 3, 4]>>,
  Expect<Equal<Flatten<[1, [2]]>, [1, 2]>>,
  Expect<Equal<Flatten<[1, 2, [3, 4], [[[5]]]]>, [1, 2, 3, 4, 5]>>,
  Expect<Equal<Flatten<[{ foo: 'bar'; 2: 10 }, 'foobar']>, [{ foo: 'bar'; 2: 10 }, 'foobar']>>,
]
```

`T extends [] ? [] : ...`가 있고 없고가 무슨 차이지...

해당 조건이 없는 경우, `const a: Flatten<[1, [2]]> = [1, 2]`의 타입이 [1, 2, [], [] 와 같이 잡힘]
Flatten<[[2]]> 를 하는 경우, [...Flatten<[2]> , ...Flatten<[]>] 이 되고,
Flatten<null> 은 [] 이 되어 []를 리턴하기 때문

**spread parametersms 항상 배열로 넘겨진다.** (값이 없으면 빈배열)
