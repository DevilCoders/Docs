# Portrait

## Portrait with an image

Portrait with an image inside can be created by passing
`src` prop to the component.

```tsx
<Portrait alt="Allison Franci" src="/public/photo.png" />
```

If there was an error while loading the image,
fallback will be rendered with the following priority:

- `text` prop
- generic portrait icon

## Portrait with a letter

Portrait with letters inside can be created by passing `text` prop
to the component.

```tsx
<Portrait text="A" />
```

## Portrait size

Dimensions of an portrait can be controlled by the `size` prop of the component.
Four portrait sizes are available:

| Size | Pixel dimensions |
| ---- | ---------------- |
| xs   | 20x20            |
| s    | 24x24            |
| m    | 40x40            |
| l    | 64x64            |

Default portrait size is `m`
