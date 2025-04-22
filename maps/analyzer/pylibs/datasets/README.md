Библиотека, упрощающая создание загрузку датасетов в ecstatic и на YT
===

Пример использования:

```python
from dateutil import parser

from maps.pylibs.yt.lib import Params

import maps.analyzer.pylibs.datasets as datasets
import maps.analyzer.toolkit.lib as tk

with tk.get_context() as ytc:
    with datasets.DatasetContext(parser.parse('2021-03-21'), parser.parse('2021-03-28')) as dataset_context:
        params = Params()
        params.arg('--output', dataset_context.add_file(tk.sources.MANOEUVRES_POOL_FILE_NAME))
        params.arg('--version', dataset_context.version)
        dataset_context.build(ytc, 'manoeuvres_table', '/builder_bin_path', params)
        dataset_context.save_table(ytc, 'manoeuvres_table', tk.paths.Common.MANOEUVRES.value, tk.sources.MANOEUVRES_TABLE_NAME, 10)
        dataset_context.upload_to_yt(ytc, tk.paths.Common.MANOEUVRES.value, 10)
        dataset_context.upload_to_ecstatic('ecstatic_dataset_name')
```
