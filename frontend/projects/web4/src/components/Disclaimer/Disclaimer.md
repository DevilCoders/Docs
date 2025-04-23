# Disclaimer

Карточка с предупреждением

{{%story::disclaimer-sandbox-desktop--playground%}}

## Использование

```js
import { compose } from "@bem-react/core";
import { Disclaimer as BaseDisclaimer } from '../Disclaimer@desktop';
import { withLimitWidthM } from '../_limitWidth/m/Disclaimer_limitWidth_m';
import { withLimitWidthS } from '../_limitWidth/s/Disclaimer_limitWidth_s';
import { withTypeDietarysuppl } from '../_type/dietarysuppl/Disclaimer_type_dietarysuppl';
import { withTypeMedicine } from '../_type/medicine/Disclaimer_type_medicine';
import { withTypeMedicineBno } from '../_type/medicineBno/Disclaimer_type_medicine-bno';
import { withTypeMedBnoWithDesc } from '../_type/medBnoWithDesc/Disclaimer_type_med-bno-with-desc';

const Disclaimer = compose(
    withLimitWidthM,
    withLimitWidthS,
    withTypeDietarysuppl,
    withTypeMedicine,
    withTypeMedicineBno,
    withTypeMedBnoWithDesc,
)(BaseDisclaimer);

<Disclaimer type="dietarysuppl" limitWidth="s">
    Текст дисклеймера
</Disclaimer>
```
