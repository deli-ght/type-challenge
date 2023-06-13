# 20230612

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBCsBMDsEC0ECCAHdBTAdgEwgBcB7CYgIwCssBjQyZJJ5h8gTzXwCcsOBpLgEMAzsQBuwgNYcAFAAFyPAMwAGSUIBsAThrCAlBADEAWyx4AlgFdjRitTpJJvYWAaH3EAIqWswwueIcVygASWN0ABssUxxCCEEiNmwiAAtBOME8PGF4iBwsAHcIADNzLAiCElSsCHNYrC5iwRosADoIABUUmsIknsEnHMJu1J4awS4Ac2tcQmF2rpriS0J0FYhhFOWKiHJxnDIqWjiC82HqvMKSsorW4IgAMWIuCCwAD0FwqPuAAz+5hi9ZIdXxxAC8EAA3rU8AAuCAAcgAjAiIABfQF9CAAJV8lgi4LQmFweA6xAA8kc6AAeEF+AA0iLEggiPgRjIALAA+CDAYCvN7YOhmIikPZQmHw5HsiDM1lYeEc9EMP4-e48gBqZSKgQgAHEzgAJSzkeEpQirYSwvlzGgpVqUebPSbAODwMAgYCuUAQAD6-oDgYDEAAmssXgBhYh4GqGho1IOJ-0QT2uIE1DDYfBkyn2Qi0xkAVUZGp5EMEODY3pAfqTQc6oIgEZEvlrdeDqfM4WecXTEoAogBHSwsxn9wXHdElLjEGwIuTppB2llRHCTXzAFbmCLCBFprGEUFIiAQyEMJxsKU0dJ7qBynxSyZjHB7jFgPuHvzjoWEY+n8+8FeN4MPeCqIk+WC4LeEBbKY8LkMQxBRBWYBvh+oKwCeUIAZeiJ4MQkyogAPhAlj4FgpT5HgIEsg+iIFCkZxYNBwhkfChBcD4qH7skn6EN+xyYf+UAXlK+GERAJFkTGlFmDR8pSgxTEsWxRCcVgDCwWBSLce+B6gkoWFniJgGIjQxAFNBoFSmw5QRBZKk4PCTQ7hpaH6V+E50IZwkQKJZkOfJdEIrZET2ZZDCsU5JQssIGlQOYwgALLEMMDTYpYwjCOYgjObFNRSeRsnUe5yTXnFOQQgA2gwAk0kOI4RNSmYkjmVL5nxSKMgiWkyghSFYBWXKMnxdW-lyw21V5+YNSyzXEtmFLtdSfGwN1vWMkiw1EKCY2wBN9JTT+1KzU1LWLbmxwrQZ3WJSlaVcBlWU5TKLlxZJpFFXUZjbaN01KAdYAALrVm27a+o8lhcA9EAAMqHugOTgx2XqgAwPKw2kPAQGw4YbEhW6BFaMEWoj1rALa9qOq0zquggwAVsIBQNOjEBalcoisv4RNmqTVo2sIdoOk6Ux0-AwCc4TOAuFAPIpdjEZpGFuDrsT5qWuTlPCzTUwel6QA)

```ts
type AppendToObject<T, U extends string, V> = { [K in keyof T ] : T[K] } & { [K2 in U] : V }
```

이렇게 했을 때, 테스트는 에러나는데 별도로 데이터를 할당하면 에러 안남

```Ts
const a : AppendToObject<test1, 'home', boolean> = { key: "cat", value: "green", home : true}

type cases = [
  Expect<Equal<AppendToObject<test1, 'home', boolean>, testExpect1>>,
  Expect<Equal<AppendToObject<test2, 'home', 1>, testExpect2>>,
  Expect<Equal<AppendToObject<test3, 'isMotherRussia', false | undefined>, testExpect3>>,
]
```

```ts

type AppendToObject<T, U extends string, V> =  { [K in keyof T | U] : K extends keyof T ?  T[K]  : V}
```

결과 받는 부분에서 구분해주기
