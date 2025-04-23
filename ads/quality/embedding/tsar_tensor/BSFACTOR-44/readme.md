# Development:

### Начальные знания о BidCorrection РСЯ: 
* BidCorrection РСЯ обучается на логах `//home/factor_check/logs/bid-correction-pool/`
* Таск обучения - `ads/factor_check/matrixnet/tasks/bc/task.yml`, можно запустить с `ads/ml_engine/tool`
* В логе, указанном выше, нет дампа профилей, их нужно приджойнить. Тут есть особенность - нужно джойнить профили на момент, предыдущий моменту ивента (симулируем реальные условия). @alexpush сказал, что есть возможность использования только дневных профилей (то есть они обновляются раз в день, доступны за год) - они лежат тут `//home/factor_check/logs/beh-profile-regular-log` (я нашел еще часовые `//logs/beh-profile-regular-log/1h/`, но они только за месяц). Значит по сути timestampы обучающей выборки огрубляются до дней, к каждому ивенту джойним вчерашний профиль. 

---

### Что планируется сделать:
1) Приджойнить профили к логам за какое-то время (логи доступны максимум за год). 
    
    ~~Для этого используем `ads/factor_check/features/calc_features`. Эту программу нужно дописать, добавить туда логику обработки beh-profile-regular-log, написать такой редьюсер, который имеет имеет два входных потока: первый - ивенты бид-коррекшн пула, второй - профили. Профили определяют состояние (запоминает для текущего UserID последнее состояние профиля), а к ивентам джойним профиль из текущего состояния. Таким образом состояние профиля всегда будет на момент времени раньше чем ивент. Затем обработать таким бинарником логи за какое-то время.~~

    Запустить `~/ads/quality/embedding/tsar_tensor/py_join_profiles`
2) Посчитаем вектора профилей ``ym && YT_POOL="neuralnetworks-broadmatch" ./dssm_apply -s //home/ads/users/jruziev/tensar/BSFACTOR-44/rsya_bidcor_20180618_20190606_userid -d //home/ads/users/jruziev/tensar/BSFACTOR-44/rsya_bidcor_20180618_20190606_userid.dssm -m ~/tmp/spynet.dssm -o EmbeddingUser -v query_embedding --col2field Queries=queries,Region=region,TopDomains=topdomains,KryptaAdhoc=adhoc,Bmcats=bmcats,VisitGoals=visitgoals,PurchaseOffers=purchase_offers,CartOffers=cart_offers,DetailOffers=detail_offers,PurchaseCounterIds=purchase_counterids,CartCounterIds=cart_counterids,DetailCounterIds=detail_counterids,Ages=ages,Revenues=revenues,Genders=genders,DetailedDeviceTypes=detailed_device_types,Browsers=browsers``
3) Приджойнить баннеры (в логе данные по баннерам неполные). Для этого используем `ads/quality/embedding/join_banners`
4) Прогнать дссмы над профилями и баннерами, получить эмбеддинги
5) Думать над тем, как делать тензорные свертки поверх этих векторов
