# 20230516

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBAcELQQEoFMCGATA9gOwDYE8IAmSeOci0gI0IEFsAXACx0IDEBXCACgAFVGAMw4BKCAGIAtsnQBLDpIkAnNFjyFxmKgCtkAYwZwA1snwBnMKXHWIARQ7IzDWTktQAkpIAOuZNMYQqBAA5sjYyEqyehAABgCy+CgYOAREADwAKgA0EADSAHwxEADuTFFMEAyoJmaVxZiV+F7IgUrBCmEMsRlFAuixuTEAdG4DRWbNerKChMwtZshdmIIQXkqYzUrOjhDL3UXMqF1mLBy4-QtdDA1JagRDEADqTGFjELK12Jhda5gAbrJ0DIcrJjqdzhBJNUWqhcLhVutNttaipkuoINoOE4ILhZCZKi8IF8lFD4TFbil8JlCiNSGxMEoIMgAB6oby+UYxLkMCxQWSMCKCVB6FoZTBYCAAb1IUGcDF8AC4IE5IthgjKIECzHpIl5nDglSr+eqoFA9Jh2YsZEqqJhML4BKQAL6jc3YbHXLBKhIU9TpMVYHIAcjlviDEAAPhAg1qdbI9S5sEH8hAALxSjWh5BKgBEAAlTDmshrY7r9dhc4I7VRUEoixrzZaGNaIELcAti1AXaRPZghlm0xB88g4ZgcxBgMAIABRJTrJRKvQCL5dVFmMyyYLYQIQVF3Qi-JH4Hvivul+Plwc5mtKeljidT2fzxfL767tDrzfboJ7ykIjYRAwx6yqeQyNj4Vr9OmDBKA4D4QAA8rkpBcjEowpgAarIyDFLs24AOKgnmHBUEqTAMAwXhmAqk48noTBDNoZhDAywTANAYAgMAligBAAD6AmCUJgkQAAmpgHCMgAwuKLQFio-HCUpfEQFxlhAc0EA+qolL+jkuRMsyzbYOgtQmPgewZIO5mWSm6YIZIoKZPpKYAGSkL6BBpAAClERjOXk+T5AA3DxICKcpQkQBkjhdFJqALLUkXCap3GyN4DJXE0LSShAtC4iYOTTsykxdE6rbrIoQa8BpyBwPRsK+GqjjABwzjtkG6nZRAS6JYOADapDFaVaT5XiyBpNpaKpJkp4AIz5DknlUgGmALUFnYziV+gMKNBUTVN+7+vNwZZuGUYxo4cYJjgyZFdtBgyBtQ0PbtY0mJNiQ6X6s1YEQp2gmGkbRueN1JotW2lU9i0vSN70HV9034Mdf3BqD5bhhDw07dDxYALo8VONVmHALKlaTc4MmAtVMpTjLpodum-WtAPysg53RvyfywoCyaWPyzZKEKIrRfNGayoD2bKjBxqkOjiYAPyGjLaqkOBvjNugNp2g62BgN2AuCsKoqnkQ4vvkjlSS8rqompqV1lorNuy2aFoQZr2v2mgesGwKQvG5DOP9NKUC-uiWbO6roffQQ9vao7OBK9Lttq27GstraXuOt2vHJVFnBbC8jIAMrNlREV56lYCgKQKbF0wtYtBZknKvabWJtREDkZR1G0dqDFMSxbTscAAhmMUES1xAWE4a3uDtzgnfd1RNHAHRA-MaxI9mG35a8hAKZxAyLRSQ3cJhKES8USvff0Yxm9tJx3FAA)

```ts
/* _____________ Your Code Here _____________ */

type MyReadonly2<T, K extends keyof T = keyof T> = Omit<T, K> &
  Readonly<Pick<T, K>>;

/* _____________ Test Cases _____________ */
import type { Alike, Expect } from "@type-challenges/utils";

type cases = [
  Expect<Alike<MyReadonly2<Todo1>, Readonly<Todo1>>>,
  Expect<Alike<MyReadonly2<Todo1, "title" | "description">, Expected>>,
  Expect<Alike<MyReadonly2<Todo2, "title" | "description">, Expected>>,
  Expect<Alike<MyReadonly2<Todo2, "description">, Expected>>
];

// @ts-expect-error
type error = MyReadonly2<Todo1, "title" | "invalid">;

interface Todo1 {
  title: string;
  description?: string;
  completed: boolean;
}

interface Todo2 {
  readonly title: string;
  description?: string;
  completed: boolean;
}

interface Expected {
  readonly title: string;
  readonly description?: string;
  completed: boolean;
}
```

```ts
type MyReadonly2<T, K extends keyof T = keyof T> = Omit<T, K> &
  Readonly<Pick<T, K>>;
```

### type default value

정답에서 `K extends keyof T = keyof T` 부분이 신기했는데, `= keyof T` 이 부분을 없애면 K에 아무것도 안넘어 올 때, 모두 readonly 처리가 되지 않아서 에러가 발생한다.

`= keyof T`는 prop의 default parameter 처럼 K의 기본값을 설정해주는 역할을 한다.
https://learntypescript.dev/06/l6-generic-parameter-defaults

### type 연결

Omit은 특정 속성을 제외한 값 반납, Pick은 특정 속성을 포함한 값만 반납
이 둘을 합치기 위해 `&`를 사용한다. [intersection type](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types)
