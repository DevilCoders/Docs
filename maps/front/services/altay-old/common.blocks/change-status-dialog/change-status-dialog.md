# change-status-dialog

## Usage

### BEMJSON
```javascript
{
	block: 'modal',
	mods: { theme: 'islands' },
	mix: {
		block: 'change-status-dialog',
		mods: { type: 'act-attributes' },
		js: {
            status: 'act_attributes',
            taskId: 42474,
            requestId: 211219
		}
	},
	content: {
		block: 'form',
		mix: {
			block: 'change-status-dialog',
			elem: 'form'
		},
		content: {
			block: 'change-status-dialog',
			mods: { type: 'act-attributes' },
			elem: 'content',
			content: [
                // ...
			]
		}
	}
}
```

### JS
```javascript
modules.define('my-block', ['i-bem-dom', 'modal'],
    function(provide, bemDom, Modal) {

        const MyBlock = bemDom.declBlock(this.name, {
            _someEvent() {
                this.findChildBlock(Modal).setMod('visible');
            }
        });

        provide(MyBlock);

    });
```
