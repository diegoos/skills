# BEM + Sass — examples

Shapes only. The rules are in [`SKILL.md`](../SKILL.md) and [`conventions.md`](conventions.md).

## Card and button

The card owns its title. The button is its own block. The loading state is a second class.

```html
<article class="card card--highlight">
  <h2 class="card__title card__title--large">Title</h2>
  <p class="card__body">Supporting text.</p>
  <button class="button button--primary is-loading" type="button">Submit</button>
</article>
```

```scss
.card {
  background-color: $color-surface;
  border-radius: $radius-2;
  padding: $space-4;

  &__title {
    font-size: $font-size-md;

    &--large {
      font-size: $font-size-lg;
    }
  }

  &__body {
    color: $color-text;
  }

  &--highlight {
    border-color: $color-accent;
  }
}

.button {
  display: inline-block;
  padding: $space-2 $space-4;

  &--primary {
    background-color: $color-accent;
    color: $color-on-accent;
  }

  &.is-loading {
    opacity: $opacity-muted;
    pointer-events: none;
  }
}

.nav {
  &__link {
    &:hover {
      color: $color-text;
    }

    &:focus-visible {
      outline: $outline-focus;
    }
  }
}
```

Compiled: `.card__title--large`, `.button--primary`, `.button.is-loading`, `.nav__link:hover`, `.nav__link:focus-visible`.

## Blocks inside a block

The header, the logo, and the nav each stand alone, so each is a block.

```html
<header class="header">
  <a class="logo" href="/">...</a>
  <nav class="nav">...</nav>
</header>
```

## Tight field

The input and the label exist only inside this field, so they are elements. The `id` pairs the label. A control that is reused alone is its own block (`.input`, `.label`) inside a shell block.

```html
<div class="form-field">
  <input class="form-field__input form-field__input--checkbox" type="checkbox" id="agree" />
  <label class="form-field__label" for="agree">I agree</label>
</div>
```
