В чем разница между selectors и getters.

selectors принимают на вход state. Скажем getVinReport это примерно `(state) => state.vinReport.data`.
А getters принимают на вход результат работы селекторов: isVinReportFetched `(vinReport) => (vinReport !== null)`.

