# Промокоды

Промокоды создаются методом Баланса с кучей параметров. Из основного, что бывает: промокод может быть на процент суммы от отплаты или фиксированную сумму, однократный или многократный (по применению), однократный по вводу в форму, иметь минимальную требуемую сумму оплаты, иметь ограничение "на уникальный домен" или "нового клиента". Последние два обычно (или всегда) либо оба выполнены, либо нет, мы на это неявно завязаны в разных местах.

{% cut "Создание промокода с ограничением на клиента и минимальную сумму, на уникальный домен" %}
```
import xmlrpclib
import datetime
import uuid
import optparse

parser = optparse.OptionParser()
parser.add_option('--client', action="store", dest="client_id")
parser.add_option('--minsum', action="store", dest="min_required")
opts,rest = parser.parse_args()

code = uuid.uuid4().hex[0:16].upper()
min_amounts = {}
multicur_bonuses = {'RUB': {'bonus1': 15000, 'bonus2': 15000, 'middle_dt': '2021-01-06T00:00:00', 'discount_pct': '0'}}
if opts.min_required is not None:
    min_amounts['RUB'] = opts.min_required
    multicur_bonuses['RUB']['minimal_qty'] = opts.min_required
promocode_args = {'CalcClassName': 'LegacyPromoCodeGroup',
                  'CalcParams': {u'bonus1': u'15000',
                                 u'bonus2': u'15000',
                                 u'discount_pct': u'0',
                                 u'middle_dt': '2021-01-06T00:00:00',
                                 u'multicurrency_bonuses': multicur_bonuses,
                                 u'service_ids': [7]},
                  'EndDt': datetime.datetime(2021, 12, 1, 0, 0),
                  'EventName': 'Created by service',
                  'FirmId': 1,
                  'IsGlobalUnique': True,
                  'MinimalAmounts': min_amounts,
                  'NeedUniqueUrls': True,
                  'NewClientsOnly': True,
                  'Promocodes': [{'client_id': opts.client_id, 'code': code}],
                  'ReservationDays': 30,
                  'ServiceIds': [7],
                  'StartDt': datetime.datetime(2019, 1, 1, 0, 0),
                  'TicketId': 'FAKE-1',
                  'ValidUntilPaid': False}

balance_url = 'http://greed-ts.paysys.yandex.ru:8002/xmlrpc'
b = xmlrpclib.ServerProxy(balance_url, allow_none=1, use_datetime=1)


res = b.ImportPromoCodes([promocode_args])
print("promocode: %s, balance result %s" % (code, str(res)))
```
Пример запуска `python promocodescr.py --client 123 --minsum 6000`

{% endcut %}

{% cut "Создание промокода на процент, неуникальный домен" %}
```
import xmlrpclib
import datetime
import uuid

balance_url = 'http://greed-ts.paysys.yandex.ru:8002/xmlrpc'
b = xmlrpclib.ServerProxy(balance_url, allow_none=1, use_datetime=1)

code = uuid.uuid4().hex[0:16].upper()

res = b.ImportPromoCodes([{
        'StartDt': (datetime.datetime.now()-datetime.timedelta(days=10)).strftime('%Y-%m-%mT%H:%M:%S'),
        'EndDt': datetime.datetime(2100, 1, 1),
        'CalcClassName': 'FixedDiscountPromoCodeGroup',
        'CalcParams': {
            'discount_pct': 30,
            'adjust_quantity': False,
            'apply_on_create': True,
        },
        'Promocodes': [
            {'code': code}
        ],
        'FirmId': 1,
        'TicketId': 'BALANCE-34131',
        'ServiceIds': [7],
        'NewClientsOnly': 1,
        'ValidUntilPaid': 0,
        'IsGlobalUnique': 0,
        'NeedUniqueUrls': 0,
        'SkipReservationCheck': 1,
    }])
print("promocode: %s, balance result %s" % (code, str(res)))
```
Пример запуска `python promocodescrpct.py`

{% endcut %}

{% cut "Заодно генерация случайного номера карты для тестинга, срок действия произвольный, cvv тоже или 123" %}
```
#!/usr/bin/python
# -*- coding: utf-8 -*-

import random

# Keep this script self-contained
#from baluhn import generate, verify


decimal_decoder = lambda s: int(s, 10)
decimal_encoder = lambda i: str(i)

class Utils(object):
    @staticmethod
    def luhn_sum_mod_base(s):
        # Adapted from http://en.wikipedia.org/wiki/Luhn_algorithm
        digits = [int(c) for c in s]
        b = 10
        return (sum(digits[::-2]) +
                sum(sum(divmod(2 * d, b)) for d in digits[-2::-2])) % b

    @staticmethod
    def verify(s):
        return Utils.luhn_sum_mod_base(s) == 0

    @staticmethod
    def generate(s):
        d = Utils.luhn_sum_mod_base(s + '0')
        if d != 0:
            d = 10 - d
        return str(d)

    @staticmethod
    def generate_pan(pan_len=16):
        prefix = '510000'  # not to mess with real world cards
        base = prefix + str(random.randint(
            10 ** (pan_len - len(prefix) - 2),
            10 ** (pan_len - len(prefix) - 1) - 1))
        pan = base + Utils.generate(base)
        assert Utils.verify(pan)
        return pan


def main():
    print(Utils.generate_pan())

if __name__ == '__main__':
    main()

# vim:ts=4:sts=4:sw=4:tw=85:et:
```
{% endcut %}

Проверки вида "новый клиент" и т д происходят следующим образом: если мы видим, что по домену есть статистика, или число уникальных доменов на баннерах клиента не равно единице, то мы отсылаем при оплате с промокодом флаг `DenyPromocode` в методы Баланса (например, `CreateRequest2`). Если флаг отправлен, и на промокод есть подобное ограничение, Баланс отвечает ошибкой, которую в директовой форме оплаты должны ловить. Для защиты от фрода вида "создал одну кампанию-потом другие с иным доменом или поменял домен" работает ess-джоба PromocodesCheckCampaignChangesProcessor.

Также есть ограничения, когда комдеп выписывает промокоды конкретным клиентам и шлёт эту инфу напрямую в Директ. Такие ограничения мы тоже обрабатываем, механизм включает в себя джобу SafeSearchTearOffPromocodesJob и интапи-ручку `promocodedomains/add` . Подробнее знает [Кирилл Богданов](https://staff.yandex-team.ru/sco76)
