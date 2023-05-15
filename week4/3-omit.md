# 20230515

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBDMELQQPIFsCWAXS8491gRgJ4QCCAdugBYD2ZxAYgK4QAUAAgIYUBmjAlBADEyAKYATVI2RDGZVLSH5GqADbo4qMmCyDdEAIqMRAZ3TytWAJLIADipGiKEKiIhLV6zRAAGKDAB4AFQAaCABpAD5vCABzETIRACdUAGMIAHcMGkZ0CEZjTRiIDAA6bSgAYVpTRMYU9GMIDmdCG1ciCBtUgGtCppUVTsTqNsSzEwhuYelvQOiuMWdKeIhEh2oANz7vMO9yiHpqRIgRAA8OW3t97xuGrE10JO4OFNdA6jFqCABvLCgzdD2ABcEBqhT+EDEJhSyRsZloILBZBiEJS1EuIkeYhB+Go1HsXCwAF99uhWm8PtQAAprLYidIQAC8EAAsoQ-OggpTQgByKHGGGoOHmHkQAA+EB5APsPIi+zRZFMzkpIPenxpIjpDOZvygUDRGKxIOeKmMImCxKwNz2WAiEAAaqh6RAFABxDAACUY+BBlHQ6BsxiBwGADRSlBKACtjCUjjFgNAwCBgNpQBAAPqZrPZrMQACa1EYxyqUIgHqSrhzVczEGT2jJbVZ7LQnJC4TtzK4hFTIAz1ZzEECJlyFQ4Zsa-YHddQtiOuQbrm+EAAogBHRgcFShZenNr1CBEybTSVsBdwcOb+zIkzAHKqYw8+vkiApMcTZkAbSwO73nLXG5UfwfxEepxAARlCNkOS5T5eX5QVhVoWUIgiC0oGA+ogPXTcgN3ECsQAJkg5sAjVag4OhWF4TIUUJR5A07ExcRkNQsAAF1U2ACBT2MOAzl-PjEmGRIwAXE4hKOJkm2gsiKIFKiRXFSVNA2TdUDEWVtAeJ4XgpT4fiwaURERdBkmRLB4IUhFQVM8F9XRRijTcPECS0EkwG0xJnleFc8NAsQwIM-4MGBGyzJRezDXEHEXJEQl3M87zXAwwigucELjLC8F3LTSdswOIsXGOABlR5Az7PL01rFNQFtCBisoDg1ggQhC2OYx8TvapfX9QNg1DAUI2jWNEnjaBgC4Yx0iSOrHWdDqVC6xUeoDIMQzDIaYzjBNgAWpbjDqlkjlcCpGoGeI4iDCA-VW-qNqjLbRqTFMgA)

```ts
type MyOmit<T, K extends keyof T> = {
  [P in keyof T as P extends K ? never : P]: T[P];
};

/* _____________ Test Cases _____________ */
import type { Equal, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Equal<Expected1, MyOmit<Todo, "description">>>,
  Expect<Equal<Expected2, MyOmit<Todo, "description" | "completed">>>
];

// @ts-expect-error
type error = MyOmit<Todo, "description" | "invalid">;

interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

interface Expected1 {
  title: string;
  completed: boolean;
}

interface Expected2 {
  title: string;
}
```

type에서 as의 역할 = [**Type assertion**의 역할](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions)
평소에도 타입 지정하는 용도로 사용하고 있었는데 조건문과 함께 사용 가능하다는 건 처음 알았다.

key가 `never`타입인 경우 `존재하지 않는 경우` 라고 취급
그래서 `[P in keyof T as P extends K ? never : P]` 를 풀어서 설명하면,
T의 키 중 하나인 P는 K에 포함되면 P, 포함되지 않으면 never인 키를 나타낸다.

여기서 `P extends K ? never : P`는 T를 가리키는 게 아님
(type MyOmit<T, K extends keyof T> = {[P in keyof (T as P extends K ? never : P)] : T[P]} // error)
