# 20230619

## [문제](https://www.typescriptlang.org/play?#code/PQKgUABBBsAsCsEC0EAiBLAZpyyn4NwCMBPCALQE0BlALxIGcIAKAASrsYEoIBiAWwCmAE3QBXfnwD2RAFaCAxgBcwuXuogBFMYIZL0UgHaqoAcUFKIAQ0MQABgHk5ipXYhKAFlcvomnwRCi2IIAToKGCgFEFgDuguH2Dm4AZIkAjHYmEAB8EABq6IIxEEYQpuhKABJiRABcEB5KSgAODLXAwEoMCh4AdLIMvVIhAObAcPBgIMCqoBAA+otLy0sQlFJiIRAAwlLCAZWhASsnixDTs8AQqUI2TADkghUeoQ1WDPcANBAAPhC3hgeRCknjeADdBPcwEoSM0AhhsAAeBzfBxpXIAXggAG9cABtADSEHQtgA1oISFJMCwHNcIGieO8IETBAAPJThYRMcmU6nMWl-BkQAD8EEMgghW3qBIAuvV+XSGYSZQBuMAAXzVYA67lh8KwmGRqPRECxDn4FWRirS3x5VJpv3paS42UuurhaANRqdmJx2quUEJxNsAFFWQoADZifaIu182mpBm2ilUhWC53ZOUOxPO5X+iDq2YgBanFYQAAquks23euhLpdWF3Q-Gaw0sMI92IgIYAjmIrBHvmG4coCxBMCEpJJ7qwO4IkD0BxHwiNdMAxPoIx9VHOIAAxKRSU1+qCGKxCep6EIkka4Kyry9Ka+GW+F3cAISsWyxuNP58Ej7PreUD3gBEBXjeuCroY+whPUhgSNEIQatCeo7Iex6-mK-6AZBUDQbB8GIaEKFgAoRh6NYED1AihoHlI3yfiEvpYQRrz1AAzLAuCFqhHoKLWTBYniuDDi4iK9v2EaIrRiL0YxX7ZN8XZsXBYrEVs6rZEpomsiOSgSX2A4yV6THfPRSk4hAqlEfwSEFtpny6fphlSSZSLyehUiWV2oG4S+KrWZyoS2fZWk6VAYnKK5xmybsDH7oePnWA+4FPjegU2epdmvOFTkykW9YNvM+6bP4WzUByrRFQ25wzKAuC5NQXhhBAlKbOBUhRvoFH1I0LRtB0XQ9P0gzDGMEzAHccTIVAuQFEUnXdQYgJ9U0rTtJ03R9AMQyjOMCDAAwXUbitDCNRAACywwBNsXgRsuL66GtA2bcNO1jaMUwzEAA)

## 1. `&`와 `|` 활용하기

```ts
// & means 'either has', | means 'both have'
type Diff<O, O1> = {
  [K in keyof (O & O1) as K extends keyof (O | O1) ? never : K]: (O & O1)[K];
};
```

## 2. Omit 활용하기

```ts
type Diff<O, O1> = Omit<O & O1, keyof (O | O1)>
```

## 3. Exclude 활용하기

```ts
type Diff<O, O1> = {
  [K in Exclude<keyof (O & O1), keyof(O | O1)>]: (O & O1)[K]
}
```