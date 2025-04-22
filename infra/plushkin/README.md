./plushkin --yp-util ~/arcadia/infra/yp_util/bin/yp-util --quota-mover ~/arcadia/infra/capacity_planning/utils/quota_mover/bin/quota_mover --from-service FROM_ID --to-service TO_ID --cluster man --recursive --resource cpu --resource memory --resource hdd --resource hdd_bw --resource ssd --resource ssd_bw

Чтобы запустился реальный перенос нужно еще передать --execute, в противном случае программа просто выведет то, что хочет сделать
