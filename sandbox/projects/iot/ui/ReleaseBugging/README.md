В этой таске потребуется и нтеграция с формой и нормальная раббота с вложениями



Работа с вложениями, варианты:
1) Уйти с бинарных задач и использовать startrek_client
2) Доработать перекопирование методов startrek_client. Далее мои попытки

    def on_execute(self)
        attachments = [self.st_attachment_upload(requests.get(att['content'], headers=self.st_headers).content)['id'] for att in self.get_ticket_attachments(ticket)]

    def st_attachment_upload(self, file):
        params = {'filename': 'file'}
        logging.info(requests.Request(method="POST", params=params, files={'file': ('file', file)}, headers=self.st_headers, url='https://st-api.yandex-team.ru/v2/attachments/').prepare())
        response = requests.post('https://st-api.yandex-team.ru/v2/attachments/',
            params=params,
            files={'file': ('file', file)},
            headers=self.st_headers,
        )
        logging.info(response.content)
        return response.json()

    def get_ticket_info(self, ticket):
        response = requests.get(self.st_api_url + ticket, headers=self.st_headers)
        return response.json()

    def get_ticket_attachments(self, ticket):
        response = requests.get(self.st_api_url + ticket + '/attachments', headers=self.st_headers)
        return response.json()