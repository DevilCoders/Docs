## Библиотека для работы с hiring-forms

См. примеры по коду: `grep -rn hiring_forms_lib .`

Загрузка спецификации и инициализация формы:

    await context.hiring_forms_storage.load_form(
        form_name, accept_language, log_extra=log_extra)
    # raises:
    # - hiring_forms_lib.exceptions.FormNotFound
    # - hiring_forms_lib.exceptions.InvalidFormSpecification
    # - hiring_forms_lib.exceptions.FormLoadError

Валидация полей:

    fields: typing.List[hiring_forms_lib.Field]
    try:
        fields = await context.from_request(
            form_name, accept_language, requests.data.fields,
            log_extra=log_extra)
    except hiring_forms_lib.exceptions.InvalidForm as exc:
        exc.response_object  # models.HiringFormsValidationError
