#Блок-обертка для содержимого блока мультиредактирования
Принимает следующие параметры:
type {String} - тип мультиредактирования, бывает dynamic, dynamic-media, mobile-content, text

formData {Object} - дополнительные параметры для формы, например:
- formData: {
    cmd: 'saveMobileAdGroups'
}
Поле cmd для формы обязательно!

editData {Object} - дополнительные данные для блока редактирования баннеров
Обязательно поле type. Примеры:
- editData: { type: 'dynamic-full' }
- editData: {
  type: 'mobile-content',
  headerType: 'mobile-content'
}

buttonsData {Object} - дополнительные данные для кнопок. Пример:
- buttonsData: {
    mods: { type: 'dynamic-media' },
    showBackButton: this.data.FORM.from_newCamp,
    statusModerateIsNotNew: this.data.campaign.statusModerate && this.data.campaign.statusModerate != 'New',
    showSaveDraft: hasLoginRights('AllowImportXlsBanners', 'agency_control')
}
- buttonsData: {
    buttons: [
        this.isMultipleSteps && 'back',
        {
            name: 'submit',
            // DIRECT-52588 только при создании, не при копировании
            mix: this.isNewGroup && {
                block: 'b-metrika',
                js: { goal: 'MEDIATYPEDYNAMIC2' }
            }
        },
        hasLoginRights('AllowImportXlsBanners', 'agency_control') &&
            (this.data.campaign.statusModerate && this.data.campaign.statusModerate != 'New') &&
            'to-draft'
    ],
    isCampaignModerated: this.data.campaign.statusModerate && this.data.campaign.statusModerate != 'New'
}
