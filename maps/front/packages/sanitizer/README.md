# yandex-sanitizer

Multi-purpose string sanitizer

## How to install
You'll need Node.js >= 10 to run this tool.

```
npm i @yandex-int/sanitizer --registry=http://npm.yandex-team.ru
```

## Interface

```javascript
const sanitizer = require('@yandex-int/sanitizer');

const dirtyString = req.body;

const cleanHtml = sanitizer.sanitizeHtml(dirtyString);

const cleanCdata = sanitizer.sanitizeCdata(dirtyString);

const cleanJs = sanitizer.removeUtfSpecialChars(dirtyString);
```

### Sanitize HTML

For sanitizing HTML, the library provides a method called `sanitizeHtml`. It is a shell for the [sanitize-html](https://github.com/punkave/sanitize-html). `@yandex-int/sanitizer` restricts some of the options of the external library:
 * `allowedTags: false` and `allowedAttributes: false` are forbidden. If used they will be ignored.
 * Attribute name wildcards are also forbidden. Such attribute patters will be ignored.
 * Extending the `allowedSchemes` list is also forbidden. The shell allows only `http`, `https`, `ftp`, `mailto` and `tel` schemes in `src` and `href`.
 * `allowedSchemesByTag` is forbidden. The value of this option will be ignored.

If you need to alter only a small part of the default allowed tag list you can do this by fetching a copy of the allowed tags using the method `getDefaultAllowedTags` and passing it to the `allowedTags` options.

`getDefaultAllowedTags` returns a `Set` which contains a copy of the default tags array. You are free to add or remove tags using the [Set's interface](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set). You can pass your customized tag set to santize-html's `allowedTags` property which was extended to accept [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#iterable) instances.

```javascript
const sanitizer = require('@yandex-int/sanitizer');
const customTags = santizer.getDefaultAllowedTags();
customTags.add('tt');

const cleanHtml = sanitizer.sanitizeHtml(dirtyString, {allowedTags: customTags});

```

## How to develop

Test can be run using:
```
npm test
```

## Former repository

This package formerly lived in the [according repository](https://github.yandex-team.ru/maps/yandex-sanitizer). Now it seems to be abandoned
