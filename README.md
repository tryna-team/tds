# tryna Design System

tryna Design System은 Figma Variable을 기준으로 만든 Tailwind CSS 토큰 패키지입니다. 원본 토큰은 `resource/`에 보관하고, 실제 개발에서 사용하는 Tailwind 토큰과 유틸리티는 `src/tailwind.css`에서 제공합니다.

## Overview

이 패키지는 디자인 파일의 토큰을 개발 코드에서 같은 의미로 사용할 수 있게 만드는 것을 목표로 합니다.

- Figma Variable을 기준으로 색상, 간격, radius, typography를 정의합니다.
- 숫자 단위는 CSS 사용성을 위해 `rem` 기준으로 변환합니다.
- Tailwind v4의 `@theme`를 사용해 `bg-*`, `text-*`, `px-*`, `rounded-*` 같은 클래스로 사용할 수 있게 합니다.
- typography는 여러 Tailwind 유틸리티를 조합하지 않고 `.default-body-medium` 같은 묶음 클래스로 제공합니다.
- 토큰명은 Figma 의미를 유지하되, 개발자가 쓰기 어렵지 않도록 3단계 이하의 짧은 이름을 사용합니다.

## Usage

Tailwind 진입 CSS에서 디자인 시스템 CSS를 import합니다.

```css
@import "./src/tailwind.css";
```

npm 배포 후에는 아래처럼 패키지 경로로 import하는 형태를 목표로 합니다.

```css
@import "@tryna/tds/tailwind.css";
```

## Token Rules

### Naming

토큰명은 짧고 예측 가능해야 합니다.

```txt
좋음: text-default
나쁨: semantic-text-default

좋음: padding-small
나쁨: page-padding-small

좋음: rounded-small
나쁨: radius-radius-small

좋음: gap-small
나쁨: gap-gap-small
```

Tailwind namespace가 이미 역할을 표현하므로 같은 의미를 반복하지 않습니다.

```txt
--color-text-default      -> text-text-default
--spacing-padding-small   -> px-padding-small, p-padding-small
--radius-small            -> rounded-small
@utility gap-small        -> gap-small
```

### Unit

Figma의 `px` 값은 CSS에서 `rem`으로 변환합니다.

```txt
8px  -> 0.5rem
12px -> 0.75rem
16px -> 1rem
20px -> 1.25rem
24px -> 1.5rem
```

`Radius.Full`처럼 무한 radius 의미가 있는 값은 `9999px`를 사용합니다.

## Color Tokens

색상은 base palette, system color, semantic color로 나뉩니다.

### Base Colors

기본 팔레트는 Tailwind color utility로 바로 사용합니다.

```txt
green-50 ~ green-900
blue-50 ~ blue-900
apricot-50 ~ apricot-900
pink-50 ~ pink-900
yellow-50 ~ yellow-900
purple-50 ~ purple-900
grey-50 ~ grey-900
grey-opacity-50 ~ grey-opacity-900
white
black
```

사용 예:

```tsx
<div className="bg-green-500 text-white" />
<div className="bg-grey-opacity-100 text-grey-900" />
```

### System Colors

상태 표현에 사용합니다.

```txt
danger-50, danger-100, danger-200
warning-50, warning-100, warning-200
success-50, success-100, success-200
information-50, information-100, information-200
```

사용 예:

```tsx
<p className="bg-danger-50 text-danger-200">
  삭제할 수 없는 이벤트입니다.
</p>
```

### Semantic Colors

컴포넌트와 화면에서는 가능한 semantic color를 우선 사용합니다.

```txt
text-default
text-additional
text-disable
text-white
icon-default
icon-additional
icon-disable
icon-white
divider-default
background-white
```

사용 예:

```tsx
<section className="bg-background-white text-text-default">
  <p className="text-text-additional">보조 설명</p>
</section>
```

## Spacing Tokens

spacing은 margin, icon margin, padding으로 구분합니다.

```txt
margin-xsmall
margin-small
margin-medium
margin-icon-xsmall
margin-icon-small
margin-icon-medium
padding-xsmall
padding-small
padding-medium
```

사용 예:

```tsx
<section className="px-margin-small py-padding-medium" />
<button className="px-padding-small py-padding-xsmall" />
```

## Gap Tokens

`gap`은 Tailwind theme namespace가 아니라 별도 utility로 제공합니다.

```txt
gap-small
gap-medium
```

사용 예:

```tsx
<div className="flex gap-small" />
```

## Radius Tokens

radius는 Tailwind의 `rounded-*` utility로 사용합니다.

```txt
rounded-xsmall
rounded-small
rounded-medium
rounded-large
rounded-full
```

사용 예:

```tsx
<div className="rounded-small" />
```

## Typography Tokens

Typography는 Figma의 최상위 그룹인 `Default`와 `Brand`를 class prefix로 사용합니다.

### Default

```txt
default-caption-large
default-label-medium
default-label-large
default-body-small
default-body-medium
default-body-large
default-body-strong-small
default-body-strong-medium
default-body-strong-large
default-title-medium
default-title-large
default-title-strong-medium
default-title-strong-large
default-heading-small
default-heading-medium
default-heading-large
default-display
```

### Brand

```txt
brand-caption
brand-label-medium
brand-label-large
brand-body-small
brand-body-medium
brand-body-large
brand-body-strong-small
brand-body-strong-medium
brand-body-strong-large
brand-title-medium
brand-title-large
brand-title-strong-large
brand-heading-medium
brand-heading-large
brand-heading-strong-medium
brand-display
```

사용 예:

```tsx
<h1 className="brand-display text-text-default">tryna</h1>
<p className="default-body-medium text-text-additional">
  일정을 더 쉽게 관리하세요.
</p>
```

## Examples

### Primary Button

```tsx
<button className="default-label-large bg-green-500 text-text-white px-padding-small py-padding-xsmall rounded-small">
  시작하기
</button>
```

사용 토큰:

```txt
Default.Label.Large
Base.Green.Green 500
Semantic.Text.White
Spacing.Semantic.Page.Padding.Small
Spacing.Semantic.Page.Padding.XSmall
Radius.Semantic.Small
```

### Event Card

```tsx
<article className="bg-background-white px-margin-small py-padding-medium rounded-medium">
  <div className="flex items-center justify-between gap-medium">
    <h2 className="default-title-strong-large text-text-default">
      이번 주 일정
    </h2>
    <span className="default-label-medium bg-green-50 text-green-700 px-padding-xsmall py-padding-xsmall rounded-full">
      진행 중
    </span>
  </div>

  <p className="default-body-medium text-text-additional">
    예정된 이벤트와 마감 일정을 확인하세요.
  </p>
</article>
```

### System Message

```tsx
<div className="bg-warning-50 px-padding-small py-padding-xsmall rounded-small">
  <p className="default-body-strong-small text-warning-200">
    네트워크 상태를 확인해 주세요.
  </p>
</div>
```

### Brand Header

```tsx
<header className="bg-background-white px-margin-medium py-padding-medium">
  <div className="flex items-center gap-small">
    <h1 className="brand-heading-large text-text-default">tryna</h1>
    <span className="brand-label-medium text-text-additional">
      Design System
    </span>
  </div>
</header>
```

## Source Tokens

Figma에서 추출한 원본 토큰은 아래 파일에 있습니다.

```txt
resource/Default.tokens.json
resource/Mode 1.tokens.json
resource/Mode 1.tokens 2.json
```

원본 토큰은 직접 수정하지 않고, 변환 스크립트 또는 빌드 산출물에서 CSS 토큰으로 변환하는 방식을 권장합니다.
