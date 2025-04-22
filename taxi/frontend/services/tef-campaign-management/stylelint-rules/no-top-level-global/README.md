# Stylelint rule custom-rules/no-top-level-global

Forbid the usage of the CSS Modules `:global` pseudo-class on top level of stylesheet

## Usage

Add this to stylelint config:
```json
{
    "rules": {
        "selector-pseudo-class-no-unknown": [true, {
            "ignorePseudoClasses": ["global"]
        }],
        "custom-rules/no-top-level-global": true
    }
}
```

## Options

### `true`

The following patterns are considered problems:
```less
:global {
  .test {
    color: red;
  }
}

:global(.test) {
    color: red;
}

@media (min-width: 1000px) {
    :global(.test) {
        color: red;
    }
}
```

The following patterns are not considered problems:
```less
.test {
    :global(.test) {
        color: green;
    }
}

@media (min-width: 1000px) {
    .test {
        :global {
            color: green;
        }
    }
}
```
