```jsx
const classNames = require('classnames');
const COLORS_JSON = require('./Colors.json');

const selectText = elem => {
    if (document.body.createTextRange) {
        const range = document.body.createTextRange()
        range.moveToElementText(elem)
        range.select()
    } else if (window.getSelection) {
        const selection = window.getSelection()
        const range = document.createRange()
        range.selectNodeContents(elem)
        selection.removeAllRanges()
        selection.addRange(range)
    }
}

const circlePressedClass = 'colors__item-circle_pressed';

const handleOnMouseDown = e => {
    const elem = e.target;
    elem.classList.add(circlePressedClass);
};

const handleOnMouseUp = e => {
    const elem = e.target;
    const parent = elem.parentNode;
    elem.classList.remove(circlePressedClass);
    if (parent) {
        const colorElem = parent.querySelector('.colors__item-var');
        selectText(colorElem);
        document.execCommand('copy');
    }
};

<div>
    <div className="colors">
        {Object.keys(COLORS_JSON).map((group, index) => {
            const colorsList = COLORS_JSON[group];
            return (
                <div key={`item${index}`} className="colors__group">
                    <div className="colors__group-name">{group}</div>
                    <div className="colors__group-list">
                        {Object.keys(colorsList).map((color, index) => {
                            const colorItem = colorsList[color];
                            const classes = classNames('colors__item', {
                                'colors__item_small': colorItem.small,
                                'colors__item_shadow': colorItem.shadow
                            });
                            return (
                                <div key={`color${index}`} className={classes}>
                                    <div onMouseDown={handleOnMouseDown} onMouseUp={handleOnMouseUp} className="colors__item-circle" style={{backgroundColor: colorItem.hex}}/>
                                    <div className="colors__item-name">{colorItem.name}</div>
                                    <div className="colors__item-hex">{colorItem.hex}</div>
                                    <div className="colors__item-var">{`$${group}${color}`}</div>
                                </div>
                            );
                        })}
                    </div>
                </div>
            );
        })}  
    </div>
</div>
```
