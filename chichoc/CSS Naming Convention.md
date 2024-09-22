# CSS Naming Conventions

## 목차

1. [OOCSS](#oocss)
   - [원칙](#원칙)
     1. [Structure와 Skin 분리](#structure와-skin-분리)
     2. [Container와 Content 분리](#container와-content-분리)
2. [SMACSS](#smacss)
   - [규칙](#규칙)
     1. [Base](#base)
     2. [Layout](#layout)
     3. [Module](#module)
     4. [State](#state)
     5. [Theme](#theme)
3. [BEM](#bem)
   - [Block](#block)
   - [Element](#element)
   - [Modifier](#modifier)
     1. [Boolean](#boolean)
     2. [Key-Value](#key-value)
   - [Mix](#mix)
4. [문제점](#문제점)
5. [Utility-First CSS / Functional CSS](#utility-first-css--functional-css)
   - [vs inline style](#vs-inline-style)
6. [마무리](#마무리)
7. [참고](#참고)

<br>

바닐라 자바스크립트로 프로젝트를 진행하면서 css 네이밍 컨벤션의 중요성을 절실히 느끼고 있다.

- 지금까지 Reactjs와 Nextjs에서 CSS-in-JS. css-modules 혹은 tailwind CSS를 사용해왔다.

  CSS-in-JS와 css-modules는 컴포넌트 단위로 추상화하고, 클래스명을 고유한 해시값으로 변환해준다.
  덕분에 css 명에 대해 깊게 고민해본 적이 없었다.

- 오히려 자식 선택자(>)를 2 depth까지 활용하며 클래스 사용을 지양해왔으며, 클래스가 필요한 경우 구글링 했을 때 가장 많이 보았던 kebab-case를 아래와 같이 주로 활용했다.

  ex) `.root-nav`, `.modal-content`

하지만 바닐라 자바스크립트로 개발하는 경우 CSS가 전역적으로 영향을 주고, DOM 조작시 활용된다.

그래서 클래스를 적극적으로 활용하되, CSS 네이밍은 보다 신중해야 한다는 생각이 들었다.

그러던 중 CSS의 여러 방법론을 알게되어 정리해보았다.

# OOCSS

> Object Oriented CSS

- CSS를 모듈 방식으로 코딩하여 중복을 최소화하는 기법이다.

  1. 모듈의 집합을 만든다.
  2. 그 모듈을 조합해 페이지 만든다.

     신규 페이지를 만드는 경우에도 CSS를 추가적으로 만들 필요 없다.

- 다른 CSS 방법론들의 근본이다.

  기본적으로 많던 적던 OOCSS를 참조하면서 개선한 것

## 원칙

크게 두 가지 원칙을 기준으로 모듈을 구현한다.

### Structure와 Skin 분리

- structure(구조): 공통적인 스타일
- skin(화면): 다른 스타일

```css
/* structure  */
#main .btn {
}

/* skin */
#main .accept {
}

#main .cancel {
}
```

### Container와 Content 분리

- container: 영역
- content: 모듈

  가능한 모듈을 특정한 영역에 의존하지 않도록 함

```css
#main {
}

/* ❌ #main .btn { */
.btn {
}
```

# SMACSS

> Scalable and Modular Architecture for CSS

- CSS 코드를 역할에 따라 5가지로 분류한 것이 특징이다.
- 다른 설계 기법과 조합하는 경우가 많다.

  각 규칙이 경우에 따라 너무 유연하여 실제 코드 지침으로 삼기 어렵기 때문이다.

## 규칙

### Base

프로젝트 전반에 적용되는 스타일링이다.

ex) 바탕화면 색상, reset css, normalize css 등

### Layout

- 웹 사이트의 레이아웃을 구성하는 큰 모듈에 관한 규칙이다.
  ex) 헤더, 메인, 사이드바 등
- id 셀렉터: 특정 페이지에서 한 번 사용되는 경우
- class 셀렉터: 반복되는 경우
  suffix `l-`를 붙임

### Module

- 모든 모듈은 레이아웃 규칙 안에 배치되는 것을 가정한다.
- 특정 컨텍스트에 지나치게 의존하지 않도록 작성한다.

  다른 페이지로 이동하거나 레이아웃에 삽입되어도 그대로 사용 가능해야 한다.

- 모듈의 루트 요소에는 반드시 class 셀렉터를 활용한다.
  - 모듈의 하위 요소는 요소 셀렉터 지양한다.
    HTML과 스타일링을 느슨하게 결합하기 위함이다.
  - 그럼에도 요소 셀렉터 사용시 손자 셀렉터가 아닌 자녀 셀렉터(>) 사용한다.

### State

- 기존 스타일 덮어쓰거나 확장하기 위해 사용한다.

  ex) hidden, expend, active, hover 등

  - 필요한 경우에는 !important 권장한다.
  - 레이아웃이나 모듈에 할당한다.

    자바스크립트에 의존하기에 레이아웃 또는 모듈과 구분하기 쉽다.

- 클래스 이름은 모두 `is-` 접두사로 시작한다.

### Theme

- 일정한 규칙에 따라 덮어쓰는 것이다.

  ex) 다크모드

- 적용 범위가 넣은 테마는 `theme` 접두사로 시작한다.

# BEM

> Block, Element, Modifier

- 컴포넌트 기반 웹 개발 접근법으로서 UI를 독립된 블록으로 분리하는 것이다.
- id는 사용할 수 없고, class만 사용 가능하다.

## Block

기능적으로 독립적이고 재사용 가능한 페이지 구성 요소를 뜻한다.

ex) `header`, `container`, `menu`, `checkbox`, `input`

- class 셀렉터를 사용한다.
  id 또는 요소 셀렉터 ❌
- 이름은 상태가 아닌 용도를 나타내야 한다.
  ```html
  <div class="error">용도</div>
  <div class="red-text">상태</div>
  ```
- 환경에 영향을 미치지 않아야 한다.
  margin 또는 position을 설정하면 외부 환경에 의존적이게 됨
- block들은 서로 중첩될 수 있다.

## Element

Block의 복합 부품으로 Block과 별도로 사용할 수 없다.

ex) `menu item`, `list item`, `checkbox caption`, `header title`

- 명명법: `block-name__element-name`

  Block과 동일하게 상태가 아닌 용도를 나타내야 함

- 모든 Block이 element를 가지는 것은 아님
- element는 서로 중첩될 수 있다.

  하지만 Block의 부분이지 Element의 부분이 아니므로 `block-name__element_element2` 와 같이 사용될 수 없다.

> [!TIP]
> 언제 Block과 혹은 Element를 만들어야 할까?
>
> - 구현된 다른 페이지 컴포넌트에 의존하지 않고 코드가 재사용된다. → Block
> - 부모 없이 구분해서 사용할 수 없다. → Element
> - Element가 더 작은 부분으로 나뉘어져야 한다. → Block/ Mix

## Modifier

- Block 또는 Element의 모양, 상태 또는 동작을 정의한다.
  - 모양: 사이즈, 테마
    ex) `size big`, `color yellow`
  - 상태: 어떻게 다른지
    ex) `disabled`, `highlighted`, `checked`, `fixed`
  - 동작: 어떻게 행동하는지
    ex) `directions_left-top`
- 홀로 사용되지 않는다.
- 크게 두 유형으로 나뉜다.

### Boolean

- Modifier 유무만 중요하고 그 값이 무관할 때 사용한다.
  ex) `disabled`, `focused`
- 명명볍
  - `block-name_modifier-name`
  - `block-name__element-name_modifier-name`
    MindBEMding: modifier 전후의 구분 문자를 `_` 대신 `-—`로 변경한 스타일
  - `block-name--modifier-name`
  - `block-name__element-name--modifier-name`

### Key-Value

- Modifier 값이 중요할 때 사용한다.
  ex) `size_s`, `theme_islands`
- 명명볍
  - `block-name--modifier-name_modifier-value`
  - `block-name__element-name_modifier-name_modifier-value`
    MindBEMding
  - `block-name--modifier-name--modifier-value`
  - `block-name__element-name--modifier-name--modifier-value`
- 동일한 유형의 Modifier를 동시에 사용할 수 없다.
  ```html
  <form class="search-form search-form_theme_islands search-form_theme_lite"></form>
  ```

## Mix

- Block과 Element가 하나의 HTML 요소에 존재하는 것을 의미한다.
- 가급적 상세도를 높이지 않고 Block의 독립성을 유지할 수 있다.

# 문제점

- HTML에 의존하는 CSS
  ex) OOCSS, SMACSS
- CSS에 의존하는 HTML
  ex) BEM

# Utility-First CSS/ Functional CSS

- 의존한다는 문제점를 해결하기 위해 대두된 방법론이다.
- 미리 정의된 클래스를 HTML에서 조합해서 사용한다.
- ex) Tailwind CSS, Tachyons, Atomic CSS

## vs inline style

- 사전에 정의한 클래스를 활용하므로 일관성을 높일 수 있다.

  아무 값이나 지정할 수 있는게 아니다.

# 마무리

- CSS 방법론에도 역사가 있다는 점이 흥미로웠으며, 그 속에서 공통적인 지향점이 있다고 느꼈다.

  - 코드 재사용성
  - 유지보수
  - 확장 가능성
  - 예측 가능성

  무엇보다 중요한 것은 프로젝트에 따라 적절한 방법론을 선택하는 것이라 생각한다.

- 정리하면서 느낀 아쉬운 점은 OOCSS와 SMACSS는 자료마다 내용이 조금씩 달랐다는 점이다.

  그래서 우선 CSS 방법론을 처음 접한 우아한테크 자료를 중심으로 정리한 후 다른 자료를 덧붙였다.

  공식 자료를 일일이 비교하며 정확성을 검토하기에는 내용이 방대했을뿐더러 CSS 방법론의 발전 흐름을 이해하는 것이 우선이기 때문이다.

# 참고

[우아한테크\_[10분 테코톡] 🎉 동동의 CSS 방법론](https://www.youtube.com/watch?v=B70h37mpD74)

[GeeksforGeeks_CSS Naming Conventions](https://www.geeksforgeeks.org/css-naming-conventions/)

[NTS\_[CSS방법론] SMACSS, BEM, OOCSS](https://wit.nts-corp.com/2015/04/16/3538)

[OOCSS 공식 사이트](http://oocss.org/)

[Slideshare_Object Oriented CSS](https://www.slideshare.net/slideshow/object-oriented-css/990405)

[SMACSS 공식 사이트](https://smacss.com/book/)

[BEM 공식 사이트](https://getbem.com/)

[카카오엔터테인먼트\_카카오웹툰은 CSS를 어떻게 작성하고 있을까?](https://fe-developers.kakaoent.com/2022/220210-css-in-kakaowebtoon/)
