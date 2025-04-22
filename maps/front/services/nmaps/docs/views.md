# Views

## Methods

### Order
Lifecycle methods should be defined before any other methods in the following order:
```
onInit
onChildContextRequest
onRender
onMount
onChange
shouldRerender
onUpdate
onUnmount
```

Good:
```tsx
class MyComponent extends vidom.Component {
    protected onInit(): void { ... }

    protected onRender(): vidom.Node {
        return (
            <div>
                { this.renderFoo() }
                { this.renderBar() }
            </div>
        );
    }

    protected onMount(): void { ... }

    protected onUnmount(): void { ... }

    private renderFoo(): vidom.Node { ... }

    private renderBar(): vidom.Node { ... }
}
```

Bad:
```tsx
class MyComponent extends vidom.Component {
    protected onRender(): vidom.Node {
        return (
            <div>
                { this.renderFoo() }
                { this.renderBar() }
            </div>
        );
    }

    private renderFoo(): vidom.Node { ... }

    private renderBar(): vidom.Node { ... }

    protected onInit(): void { ... }

    protected onMount(): void { ... }

    protected onUnmount(): void { ... }
}
```

### Handlers

In general, handlers should be extracted to separate methods.

Good:
```tsx
class MyComponent extends vidom.Component {
    protected onRender(): vidom.Node {
        return (
            <div>
                <Button onClick={ this.onButtonClick }/>
                <MyComponent onAction={ this.onAction }/>
            </div>
        );
    }

    private onButtonClick = (): void => {
        this.doFoo();
        this.doBar();
    }

    private onAction = (): void => {
        this.doSomething();
    }
}
```

Bad:
```tsx
class MyComponent extends vidom.Component {
    protected onRender(): vidom.Node {
        return (
            <div>
                <Button
                    onClick={
                        () => {
                            this.doFoo();
                            this.doBar();
                        }
                    }
                />
                <MyComponent onAction={ () => this.doSomething() }/>
            </div>
        );
    }
}
```

Extraction can be omitted in case of there exists a function that does the same thing, for example, if handler just calls the corresponding attribute:
```tsx
interface MyComponentAttrs {
    title: string;
    onClick(): void;
}

class MyComponent extends vidom.Component<MyComponentAttrs> {
    protected onRender(): vidom.Node {
        return (
            <Button onClick={ this.attrs.onClick }/>;
        );
    }
}
```

Inline handlers are acceptable if they depend on something that can't be obtained inside them, for example, variables inside closures.
Nevertheless, they should pass that dependency to the corresponding separate handler:
```tsx
interface MyComponentAttrs {
    items: string[];
}

class MyComponent extends vidom.Component<MyComponentAttrs> {
    protected onRender(): vidom.Node {
        return (
            <div>
                { this.attrs.items.map(item => <Button onClick={ () => this.onItemClick(item) }/> ) }
            </div>
        );
    }

    private onItemClick(item: string): void {
        this.doFoo();
        this.doBar(item);
    }
}
```
