Утилита для переноса реалов fslb на haproxy
-------------------------------------------

Посмотреть тип реалов в каждом конфиге::
    
    pashayelkin@pashayelkin:~/repos/arcadia/market/sre/tools/fslb2haproxy$ ./fslb2haproxy list
    config: 26134-default-vendors.market_slb-front-stable.yaml env=default type=haproxy
    config: 25412-ipa-blue-pre.market_slb-front-stable.yaml env=default type=haproxy
    config: 103-fox-beru.yaml env=default type=FQDN
    
    # С путями к файлам
    pashayelkin@pashayelkin:~/repos/arcadia/market/sre/tools/fslb2haproxy$ ./fslb2haproxy list --long
    config: /home/pashayelkin/repos/arcadia/market/sre/conf/fslb/prod/values-available/103-fox-beru.yaml env=default type=FQDN
    config: /home/pashayelkin/repos/arcadia/market/sre/conf/fslb/prod/values-available/59-abo-old.yaml env=default type=conductor
    config: /home/pashayelkin/repos/arcadia/market/sre/conf/fslb/prod/values-available/59-abo-old.yaml env=testing type=conductor

Сгенерировать конфиг haproxy (WIP)::

    pashayelkin@pashayelkin:~/repos/arcadia/market/sre/tools/fslb2haproxy$ ./fslb2haproxy convert /home/pashayelkin/repos/arcadia/market/sre/conf/fslb/common/src/balancer/values-available/300-sovetnik.yaml  
    <<< FSLB config
    ...
    >>> Haproxy config
    ...
