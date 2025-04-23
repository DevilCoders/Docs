```mermaid
title Sequence of getting crossbrand products

participant "eats-products" as eats-products

participant eats-retail-seo
participant eats-nomenclature
participant eats-catalog



eats-products->eats-retail-seo:/v1/product/generalized-info\n params:\n   - publicId
eats-products<--eats-retail-seo:Generalized_info

space
eats-products->eats-nomenclature:/v1/manage/brand-ids-by-sku-id\nparams:\n  - sku_id\n

eats-products<--eats-nomenclature:array(brand_id, public_id)

space
eats-products->eats-catalog:/internal/v1/places\nparams:\n  - location\n  - array(brand_id)\n

eats-products<--eats-catalog:array(place_id, brand_name, logo, color_theme)


space
eats-products->eats-nomenclature:/v1/place/products/info\nparams:\n  - array(place_id, public_id)

eats-products<--eats-nomenclature:array(dynamic_info)
```