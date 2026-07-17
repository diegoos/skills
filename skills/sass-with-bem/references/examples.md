# BEM + Sass — examples

Shapes only. Rules: [`SKILL.md`](../SKILL.md), [`conventions.md`](conventions.md).

## Card + button (composition, flat `&`)

```html
<article class="card card--highlight">
  <h2 class="card__title card__title--large">Title</h2>
  <p class="card__body">Supporting text.</p>
  <button class="button button--primary is-loading" type="button">
    Submit
  </button>
</article>
```

```scss
.card {
  background-color: #fff;
  border-radius: 8px;
  padding: 16px;

  &__title {
    font-size: 1.2rem;

    &--large {
      font-size: 1.5rem;
    }
  }

  &__body {
    color: #333;
  }

  &--highlight {
    border: 2px solid #ffaa00;
  }
}

.button {
  display: inline-block;
  padding: 8px 16px;

  &--primary {
    background: #06c;
    color: #fff;
  }

  &.is-loading {
    opacity: 0.6;
    pointer-events: none;
  }
}

.nav {
  &__link {
    &:hover {
      color: #111;
    }

    &:focus-visible {
      outline: 2px solid #06c;
    }
  }
}
```

→ `.card__title--large`, `.button.is-loading`, `.nav__link:hover` — still **flat** class chains.

## Form field (axiom: tight vs composed)

Tight — input/label only make sense together:

```html
<div class="form-field">
  <input
    class="form-field__input form-field__input--checkbox"
    type="checkbox"
    id="agree" />
  <label class="form-field__label" for="agree">I agree</label>
</div>
```

Reusable alone → separate blocks (`.input`, `.label`) composed in a shell.
