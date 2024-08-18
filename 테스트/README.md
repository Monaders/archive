# 테스트

## 목차

- [테스트 코드?](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md)

  - [테스트 종류](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md#%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%A2%85%EB%A5%98)

    - [단위 테스트](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md#%EB%8B%A8%EC%9C%84-%ED%85%8C%EC%8A%A4%ED%8A%B8)
    - [통합 테스트](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md#%ED%86%B5%ED%95%A9-%ED%85%8C%EC%8A%A4%ED%8A%B8)
    - [E2E 테스트](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md#e2e%ED%85%8C%EC%8A%A4%ED%8A%B8)

  - [테스트코드의 필요성](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md#%ED%85%8C%EC%8A%A4%ED%8A%B8%EC%BD%94%EB%93%9C%EC%9D%98-%ED%95%84%EC%9A%94%EC%84%B1)

    - [디버깅 비용 절감](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md#%EB%94%94%EB%B2%84%EA%B9%85-%EB%B9%84%EC%9A%A9-%EC%A0%88%EA%B0%90)
    - [문서화](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md#%EB%AC%B8%EC%84%9C%ED%99%94)
    - [리팩토링의 편리함](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md#%EB%A6%AC%ED%8C%A9%ED%86%A0%EB%A7%81%EC%9D%98-%ED%8E%B8%EB%A6%AC%ED%95%A8)
    - [클린코드](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md#%ED%81%B4%EB%A6%B0%EC%BD%94%EB%93%9C)
    - [배포 테스트](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md#%EB%B0%B0%ED%8F%AC-%ED%85%8C%EC%8A%A4%ED%8A%B8)

  - [결론](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8%20%EC%BD%94%EB%93%9C%3F.md#%EA%B2%B0%EB%A1%A0)

- [단위 테스트](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%EB%8B%A8%EC%9C%84%ED%85%8C%EC%8A%A4%ED%8A%B8.md#%EB%8B%A8%EC%9C%84-%ED%85%8C%EC%8A%A4%ED%8A%B8)

  - [단위 테스트 전략](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%EB%8B%A8%EC%9C%84%ED%85%8C%EC%8A%A4%ED%8A%B8.md#%EB%8B%A8%EC%9C%84-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%A0%84%EB%9E%B5)

  - [효과적인 단위 테스트를 위한 원칙](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%EB%8B%A8%EC%9C%84%ED%85%8C%EC%8A%A4%ED%8A%B8.md#%ED%9A%A8%EA%B3%BC%EC%A0%81%EC%9D%B8-%EB%8B%A8%EC%9C%84-%ED%85%8C%EC%8A%A4%ED%8A%B8%EB%A5%BC-%EC%9C%84%ED%95%9C-%EC%9B%90%EC%B9%99)

  - [단위 테스트의 구조(AAA)](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%EB%8B%A8%EC%9C%84%ED%85%8C%EC%8A%A4%ED%8A%B8.md#%EB%8B%A8%EC%9C%84-%ED%85%8C%EC%8A%A4%ED%8A%B8%EC%9D%98-%EA%B5%AC%EC%A1%B0-aaa)

  - [좋은 단위 테스트](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%EB%8B%A8%EC%9C%84%ED%85%8C%EC%8A%A4%ED%8A%B8.md#%EC%A2%8B%EC%9D%80-%EB%8B%A8%EC%9C%84%ED%85%8C%EC%8A%A4%ED%8A%B8)

    - [테스트 4대 요소](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%EB%8B%A8%EC%9C%84%ED%85%8C%EC%8A%A4%ED%8A%B8.md#%ED%85%8C%EC%8A%A4%ED%8A%B8-4%EB%8C%80-%EC%9A%94%EC%86%8C)

    - [블랙박스 테스트](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%EB%8B%A8%EC%9C%84%ED%85%8C%EC%8A%A4%ED%8A%B8.md#%EB%B8%94%EB%9E%99%EB%B0%95%EC%8A%A4-%ED%85%8C%EC%8A%A4%ED%8A%B8)

    - [DRY보다 DAMP하게 작성해야 합니다.](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%EB%8B%A8%EC%9C%84%ED%85%8C%EC%8A%A4%ED%8A%B8.md#dry%EB%B3%B4%EB%8B%A4-damp%ED%95%98%EA%B2%8C-%EC%9E%91%EC%84%B1%ED%95%B4%EC%95%BC-%ED%95%A9%EB%8B%88%EB%8B%A4)

    - [구현이 아닌 결과를 검증해야 합니다.](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%EB%8B%A8%EC%9C%84%ED%85%8C%EC%8A%A4%ED%8A%B8.md#%EA%B5%AC%ED%98%84%EC%9D%B4-%EC%95%84%EB%8B%8C-%EA%B2%B0%EA%B3%BC%EB%A5%BC-%EA%B2%80%EC%A6%9D%ED%95%B4%EC%95%BC-%ED%95%A9%EB%8B%88%EB%8B%A4)

    - [문서화 가능한, 읽기 좋은 테스트를 작성하세요.](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/%EB%8B%A8%EC%9C%84%ED%85%8C%EC%8A%A4%ED%8A%B8.md#%EB%AC%B8%EC%84%9C%ED%99%94-%EA%B0%80%EB%8A%A5%ED%95%9C-%EC%9D%BD%EA%B8%B0-%EC%A2%8B%EC%9D%80-%ED%85%8C%EC%8A%A4%ED%8A%B8%EB%A5%BC-%EC%9E%91%EC%84%B1%ED%95%98%EC%84%B8%EC%9A%94)

- [TDD & BDD](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/TDD%26BDD.md#tdd--bdd)

  - [TDD](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/TDD%26BDD.md#tdd)
  - [BDD](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/TDD%26BDD.md#bdd)
    - [Given-When-Then](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/TDD%26BDD.md#given---when---then)

- [Jest](https://github.com/Monaders/archive/blob/feature/%233-%ED%85%8C%EC%8A%A4%ED%8A%B8/%ED%85%8C%EC%8A%A4%ED%8A%B8/Jest.md#jest)
