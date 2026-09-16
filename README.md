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
  - [Review status](#review-status)
  - [Continued development](#continued-development)
- [Author](#author)

## Overview

### The challenge

Users should be able to:

- See hover and focus states for all interactive elements on the page
- View a responsive card layout on mobile and desktop screens

### Screenshot

![](./preview.jpg)

### Links

- Solution URL: [GitHub Repository](https://github.com/jonghwascript/blog-preview-card.git)
- Live Site URL: [Live Demo](https://jonghwascript.github.io/blog-preview-card)

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

According to the HTML5 standard, the `<footer>` tag can be used not only for the footer of an entire webpage, but also for closing information (author, publication date, etc.) within an `<article>` or `<section>`.

```html
<article class="blog-card">
  <!-- Main content -->
  <footer class="blog-card__author">
    <img src="avatar.webp" alt="Profile">
    <span>Greg Hooper</span>
  </footer>
</article>
```

This clearly tells screen readers and search engines "this is where the card's main content ends and the author information begins."

#### 2. Responsive Width Strategy

The 375px and 1440px values provided by Frontend Mentor are **design canvas sizes**. They are not values to put directly in CSS, but reference points for reviewing the result in the browser.

The wrapper has a maximum width of `24rem`. The card uses `width: 100%`, a mobile maximum width of `20.4375rem`, and a PC maximum width of `24rem`.

A key lesson was that setting a larger `width` does not override a smaller `max-width`. The PC condition now changes `max-width` so the card can actually grow.

#### Grid sizing without overflow

The card uses `grid-template-columns: minmax(0, 1fr)`. The minimum of `0` allows the column to shrink, while `1fr` fills the available content width. A fixed minimum such as `17.4375rem` caused overflow when the card's content area became narrower than that value.

#### Viewport height and outer spacing

The layout uses Flexbox to center the card horizontally and vertically. `min-height: 100dvh` follows the dynamic viewport height while allowing the page to grow when the card needs more vertical space.

The body's default margin is removed, and `main` has `padding-inline: 1rem` to leave room beside the card and its shadow on narrow screens.

```css
main {
  display: flex;
  padding-inline: 1rem;
  justify-content: center;
  align-items: center;
  container-type: inline-size;
  container-name: blog;
  min-height: 100dvh;
}
```

#### 3. CSS Container Queries

Container queries apply styles based on the parent container's size, not the viewport:

```css
main {
  container-type: inline-size;
  container-name: blog;
}

.blog-card-wrapper {
  --card-theme: mobile;

  @container blog (min-width: 25rem) {
    & {
      --card-theme: pc;
    }
  }
}
```

The condition measures the `main` container's content width, not the full browser width. Its inline padding therefore affects when the PC theme becomes active.

#### 4. CSS Style Queries

Style queries enable conditional styling based on CSS custom property values:

```css
.blog-card {
  @container style(--card-theme: pc) {
    max-width: 24rem;
  }
}
```

#### 5. CSS Custom Properties for Color Management

Using CSS variables improves maintainability:

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

Focus styles for keyboard navigation support:

```css
.blog-card__link:focus-visible {
  outline: 2px solid var(--color-black);
  outline-offset: 2px;
}
```

#### 7. Content-sized category badge and readable text

The category badge no longer has an explicit width or height. Its `inline-block` display, text, line height, and padding determine its size. The publication date uses `display: block` so it stays on a separate line.

I tried `3vw` to make the text shrink continuously with the viewport, but it produced text as small as 9.6px at a viewport width of 320px. The final badge uses `0.75rem` on mobile and `0.875rem` in the PC theme: 12px and 14px respectively when the root font size is 16px.

I also learned that `rem` follows the root font size rather than the viewport width. `clamp()` only changes continuously while its preferred value lies between its minimum and maximum. For example, `clamp(0.75rem, 3vw, 1rem)` stops shrinking at 12px with a 16px root font size. A font size set directly on the badge also takes precedence over inheriting the body's font size.

#### 8. Image cropping and rounded corners

The image occupies a `12.5rem`-high Grid row and fills its area with `width: 100%` and `height: 100%`. `min-width: 0` and `min-height: 0` allow the image to shrink within the Grid layout.

I compared `object-fit: contain` and `cover`. `contain` showed the full illustration but left empty space inside the image element, making the rounded corners less apparent. The final choice is `cover`: it preserves the image's proportions and fills the rounded area, accepting some cropping as the available width changes. The corner radius is `0.625rem`.

### Review status

- Manually reviewed the layout at a 320px viewport and on desktop during development; the badge text size and card layout were visually checked.
- Confirmed in the source that the Grid column can shrink and the PC card maximum width can increase.
- Hover and keyboard focus styles are implemented. A final keyboard Tab and hover interaction check remains to be completed.
- The publication date's `datetime` value still needs to be aligned with the visible date, `21 Dec 2023`.
- The screenshot above has not been regenerated as part of this update.

### Continued development

- Practice choosing readable minimum and maximum sizes for fluid typography with `clamp()`
- Learn more about CSS Container Queries use cases
- Check keyboard focus visibility, browser zoom, and short viewport heights
- Review image alternative text and semantic HTML before adding ARIA attributes

## Author

- Frontend Mentor - [@jonghwascript](https://www.frontendmentor.io/profile/jonghwascript)
