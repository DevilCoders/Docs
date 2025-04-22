# Error Boundary

Error boundary is a component that allows to catch JS errors 
anywhere in their component tree and display a fallback UI instead
of the component tree that crashed. Error boundary catches errors
during rendering, in lifecycle methods, and in constructors of the
whole tree below them.

## Props

| Name | Type | Default | Description |
|------|------|---------|-------------|
| children | React.ReactNode | | child nodes which will be rendered if there are no runtime errors present
| fallback | React.ReactElement | | element that will be rendered if an error was caught
| className | string | | class name of the root element
| styles | React.CSSProperties | | styles applied to the root element

---

For more information please refer to [React docs](https://reactjs.org/docs/error-boundaries.html)
