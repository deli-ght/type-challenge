# 20230727

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBDM0OwDYIFoIEkB2B7ATgEwFMcAVHAQwDciBnMgG0hWWZcYCMBPCAKwEsyMAc2oALARAAUAAT4DhYjAFsCAFzIBKCAGJleXgFdF2rG24EAxirCMttiAEV9Bait5YM1qGkUAHOgWUMFQgVEQIQjh9wqhxqNwwILAAzCDZeDDIcLhUcAnD03EIcEPIY2joAOk8IADFcCAIADzJffwAuaoADbpVI53McXh8rKHN3FxK8gEYIAF4IAG9GKAp6NogpgBpliH8klXWMfTo6bagoQcERA8WdlbWIACYz86g9m6XX19W6degXr67Aj7Q7HU53c6Xa6gk4A84AXzhF14VxuR1hO0RjHhEDI1AgYwwLmqvSiEAAgnN0Nh8ERSJQaPQADykgjJSYEKYAPggwGAEAA2lsYJsngBdRjdTrVHkANV4BAA7okEgBxXgqAAS+jY62uKh81DafJU1HMIgq3GoFVwgmAsEQYBAwGsoAgAH1PV7vV6IABNLD6YoAYSwhAgmqI4R9Mc9EGd1nSKiISTI5nCpDyADkw+FPhAfqDFGwiIx3utMwQc+GAD4QdEMZGoiu5Ku5iB1htgeFgVnUwp00qMuhM4gNRrJjB4fGV6vhTtgnnzAQcV0gD2xn0QYjOYLBvHODeb30J3i+XDBPsLCAAUQAjvp6KKb40opYIDikjgsEYAORSVlkHNeh-CEZxgH0Vw6GoX9rEJCYcmmKl80LDYXnLeswReKEPh2VDnh2DD82+B5-ghDCGyRCAcJhcFXixV4aMwjEoCxHE8QJcYrDAeDL1bR5kMYVCtjLYE0SwxgmMo7tcXxXi4K4jloEE+5fjQ0SQVuEi1II14KIkxiUWhZi6I-bCjPEjF2LkriFKJPi8gAFhUgsHhEt4xNo8zmy0858LhfSWMhCyvOxbZrM4+zrD7cwD3xeYBUYF83xUJl70fEdMAHEgh1iZkGy5UUBTFLlCqS18LFS9LmSy2kcoZPKR1ZdlEM5QrBWFf5xVKl5ksqtKHxqmkinpMpmWalJWsedqhRKsqoD6ywBoyplapG3LyhZPoWtbaAZueDY5t6iqluqzLhsHBrNomjlHJm4VHiOsAJTAN1j29Wog1CIgIAAZWTQ0j3e+MXVARgeV+sRcggDhA2KagsDoSD4iNCB9UNY1gFNc1LWtW17XgBBgAEahFVLKA5QVZUEaR1xxj1FQDSNE0zQtK0bRwO0HSJmnkfGcGIAAWVwcJgzEE4CDA1H0eZrHWdxjnBCdF0gA)

```ts
type InorderTraversal<T extends TreeNode | null> = T extends TreeNode
  ? [T["val"], ...InorderTraversal<T["left"]>, ...InorderTraversal<T["right"]>]
  : [];
```

처음에 이렇게 작성했더니 recursive error가 뜸

```ts
type InorderTraversal<T extends TreeNode | null> = [T] extends [TreeNode]
  ? [...InorderTraversal<T["left"]>, T["val"], ...InorderTraversal<T["right"]>]
  : [];
```

T extends TreeNode와 [T] extends [TreeNode]의 차이점?

https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#distributive-conditional-types

```
T는 분산 조건형이기 때문에, 분산 조건형은 합집합형의 모든 타입을 가져와서 확장 판단을 하기 때문에, T가 TreeNode를 확장할 때, 1. TreeNode가 TreeNode를 확장하고, 2. null이 TreeNode를 확장한 다음, null이 []가 되는 두 개의 확장 판단을 하게 되어 너무 깊은 재귀를 하게 됩니다. null extedns TreeNode가 []가 되어 너무 깊은 재귀를 초래합니다.
```
