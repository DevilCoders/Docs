# Disk getip

## Что это такое

Это небольшой инструментарий для поиска незанятого IP в указанном сетевом макросе, влане и датацентре

## Как этим пользоваться

  ```
  ~/projects » pip install disk-getip
  ~/projects/disk-utils » getip --macro _DISKNETS_ --vlan 564 --dc SAS --v6 --v4
    16:24:06 INFO      Found netinfo => 5.255.243.0/24 datacenter => Сасово-1
    16:24:06 INFO      Found netinfo => 2a02:6b8:0:1a4f::/64 datacenter => Сасово-1
    16:24:06 DEBUG     Probing DNS and switch info for IP => 5.255.243.47
    16:24:06 DEBUG     This ip already have reverse DNS record. Skipping...
    16:24:06 DEBUG     Probing DNS and switch info for IP => 5.255.243.136
    16:24:06 DEBUG     This ip already have reverse DNS record. Skipping...
    16:24:06 DEBUG     Probing DNS and switch info for IP => 5.255.243.27
    16:24:06 DEBUG     This ip already have reverse DNS record. Skipping...
    16:24:06 DEBUG     Probing DNS and switch info for IP => 5.255.243.212
    16:24:07 INFO      Found unassigned IP => 5.255.243.212
    16:24:07 DEBUG     Probing DNS and switch info for IP => 2a02:6b8::1a4f:3e2a:c05f:44cc:5886
    16:24:07 INFO      Found unassigned IP => 2a02:6b8::1a4f:3e2a:c05f:44cc:5886
    5.255.243.212
    2a02:6b8::1a4f:3e2a:c05f:44cc:5886
  ```
