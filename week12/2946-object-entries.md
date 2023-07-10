# 20230710

## [문제](https://www.typescriptlang.org/play?ssl=26&ssc=91&pln=26&pc=1#code/PQKgUABBBMCcAsA2CBaCB5ARgKwKYGMAXAUQDtCAnAS1wGdJUUnmHMBPCbKgQ1IHNaAC14QAFAAEuvAcNIBbXIW4BKCAGIFAEyoBXOeoD2OAoTAM1FiAEUddQlQOkzUAJJyADgBtcC8hEKCuP5s7kEAbrgUtA6kEAYAZhAABilYeEQAdLjk1HQpSc4QAGIGFBC4AB7cHt6F+YQhdPjU7qZQVOSR8dz4QQCyBpq4nhAA3gxQpNW4AFwQtJQdfADcExDcfLMQpHqYkatQUJ4G+Nz2jrRzC9T8ANoAuhAAPts6np4HEAC+DA2hEHJBsMyIs6BAALwYYxEEG5WgAHgGQ08AD4IMBgBBbgByKYKbEAGnmi34jxeOI2uEJrzkewoZKx2OOp3OpFo1OuSwez1e73un3yhTRADUaAB3OKxADiVEIAAkdJg5oJCIR3JcMYRaPhBBlsLQMqU+MA4EgwCBgGZQBAAPp2+0O+0QACaBh0ZQAwkCIHLIkFHQG7RALWY-kE0iZYTQEQAVNGQgDWuDYCQgMfKFUI2U0tAgHXikQgAEEIAB+KAlypZ0g5iBJlOJdPl25Fokxlv3R5zbnd+5WkC2wOOtN2CAe7i0MFD4chqgeUqEYL-UYQYgARx03E8ROIFVCRG+EHiFAM+mx4jDKB1W+8-DowB09k87LMHSzFG6vQgSOGYwYeK2Tl+AYSk5h2WlIgYZkzhiS5iRuPhuReHZ3jAH4wDDb8gU8KMwUhHEAI5Ek+AZClNmpcC6VIpkThgi4iIQpDeU8PswHwC5F24CA5gjGEcmjeEV3rUs5h0GtcHiDpcE0b540ZetqTEoZJNIaTWMw05J1zfCGF3fdCHhddN08eFeJIfi6ERbCUSJH8cIs2gURs3S9xMQyNy3UzoXM0EEQABW4Ch7E8uynNs7DcMc5yoD0tyjM8szIsEutkxEiAlIkqSZK+Gz5OTRTxJUtSwpc-T3OMrz0h8uFkvrUTCqy2SiRxBSiQyorNHuEqYtcohyoS7ykqE5MrmInl2sanLmuxVr4KWcaGtUzqStY61pwdYp3QCQsAGUs3VQd1ptYNLVABg0R24QKCCFN3XmAxPEfWDlVVdUZk1bVdX1Q0KGNU1EGAXhaDFSCoBFcV7se1k4JVNUNWALUdT1A0jRNBAAdoB6nouc6sOusdhHebJNhh174cRr6Ud+81LSAA)

```ts
type ObjectEntries<T> = keyof T extends infer A
  ? A extends keyof T
    ? [A, T[A]]
    : []
  : [];
```

optional인 경우, T[A]에 undefined가 추가되어, 원하는 타입이 나오지 않음.

```ts
type ObjectEntries<T> = keyof T extends infer A
  ? A extends keyof T
    ? [A, Required<T>[A]]
    : []
  : [];
```

이렇게 되면 기본값이 undefined인 경우도 undefined가 제거됨.

```ts
type ObjectEntries<T, U = Required<T>> = {
  [K in keyof U]: [K, U[K] extends never ? undefined : U[K]];
}[keyof U];
```

U 타입을 별도로 받아서 하는게 간략하게 할 수 있는 방법인듯 ..ㅠㅠ 안쓰고 싶었는데..
