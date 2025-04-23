Скачивание конфига из deploy

ya tool dctl get stage lms-backend-stress > lms-backend-stress.yaml
ya tool dctl get stage lms-backend-tank > lms-backend-tank.yaml
ya tool dctl get stage stress-balancer > stress-balancer.yaml

Восстановить стенды можно соответственно командами

ya tool dctl put stage lms-backend-stress.yaml --rewrite-delegation-tokens
ya tool dctl put stage lms-backend-tank.yaml --rewrite-delegation-tokens
ya tool dctl put stage stress-balancer.yaml --rewrite-delegation-tokens
