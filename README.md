# Frontend Mentor - Blog preview card solution

This is a solution to the [Blog preview card challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/blog-preview-card-ckPaj01IcS).

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
- [Author](#author)

## Overview

### The challenge

Users should be able to:

- See hover and focus states for all interactive elements on the page

### Screenshot

![](./preview.jpg)

### Links

- Solution URL: [GitHub Repository](https://github.com/jonghwascript/blog-preview-card.git)
- Live Site URL: [Live Demo](https://yourusername.github.io/blog-preview-card)

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties (CSS Variables)
- CSS Grid
- Flexbox
- CSS Container Queries
- CSS Nesting
- BEM naming convention
- Mobile-first workflow

### What I learned

#### 1. Semantic HTML - footer in article

HTML5 표준에 따르면 `<footer>` 태그는 웹페이지 전체의 바닥글뿐만 아니라, `<article>`이나 `<section>` 내부의 마무리 정보(작성자, 발행일 등)를 담는 용도로도 사용됩니다.

```html
<article class="blog-card">
  <!-- 본문 내용 -->
  <footer class="blog-card__author">
    <img src="avatar.webp" alt="프로필">
    <span>Greg Hooper</span>
  </footer>
</article>
```

스크린 리더와 검색엔진에게 "여기부터는 이 카드의 본문이 끝나고, 작성자 정보가 나오는 곳"이라고 명확하게 알려줍니다.

#### 2. Responsive Width Strategy

프론트엔드 멘토에서 제공하는 375px과 1440px은 **디자인 시안의 도화지 크기**입니다. CSS에 직접 넣는 값이 아니라, 브라우저에서 결과물을 검수할 때 사용하는 기준점입니다.

```css
.blog-card-wrapper {
  width: 100%;        /* 화면이 작아지면 유연하게 줄어듦 */
  max-width: 384px;   /* 화면이 커져도 이 크기 이상으로 팽창하지 않음 */
}

body {
  padding: 1.5rem;    /* 모바일에서 카드가 양끝에 붙지 않도록 */
  display: flex;
  justify-content: center;
  min-height: 100vh;  /* 데스크탑에서 정중앙 배치 */
}
```

#### 3. CSS Container Queries

컨테이너 쿼리는 뷰포트가 아닌 부모 컨테이너의 크기를 기준으로 스타일을 적용합니다:

```css
main {
  container-type: inline-size;
  container-name: blog;
}

.blog-card-wrapper {
  --card-theme: mobile;

  @container blog (min-width: 400px) {
    & {
      --card-theme: pc;
    }
  }
}
```

#### 4. CSS Style Queries

CSS 커스텀 속성 값에 따라 조건부 스타일링이 가능합니다:

```css
.blog-card {
  @container style(--card-theme: pc) {
    width: 384px;
  }
}
```

#### 5. CSS Custom Properties for Color Management

CSS 변수를 사용하면 유지보수성이 향상됩니다:

```css
:root {
  --color-yellow: hsl(47, 88%, 63%);
  --color-black: hsl(0, 0%, 7%);
}

body {
  background-color: var(--color-yellow);
}
```

#### 6. Accessibility - Focus States

키보드 탐색 지원을 위한 포커스 스타일:

```css
.blog-card__link:focus-visible {
  outline: 2px solid var(--color-black);
  outline-offset: 2px;
}
```

### Continued development

- Explore `clamp()` function for fluid typography
- Learn more about CSS Container Queries use cases
- Improve accessibility with ARIA attributes

## Author

- Frontend Mentor - [@yourusername](https://www.frontendmentor.io/profile/yourusername)
