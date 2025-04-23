Блок с корректировками ставок. Пример использования:

`
{
    block: 'b-adjustment-rates-popup',
    tabsHash: {
        default: defaultTab,
        tabs: adjustmentTabs
    },
    modelId: modelId,
    content: [
        { elem: 'hidden-input' },
        { elem: 'switcher' },
        { elem: 'rates', modelData: campaign.hierarchicalMultipliers }
    ]
}
`
adjustmentTabs - ['mobile', 'video', 'retargeting', 'demography', 'performance-tgo'] - список доступных табов
defaultTab - имя таба, выбранного по умолчанию
