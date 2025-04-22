## prediction-api:0.2.28 (01.04.2022 11:09)

  * upd dollar const + upd validdation to supergen coefs 

## prediction-api:0.2.27 (01.04.2022 11:09)

  * fix logging

## prediction-api:0.2.26 (24.03.2022 22:00)

  * upd coefs + add validdation to supergen coefs 

## prediction-api:0.2.25 (22.03.2022 14:09)

  * add sentry

## prediction-api:0.2.24 (18.03.2022 14:09)

  * add coef for supergeneration + add orig_price to response

## prediction-api:0.2.21 (05.03.2022 18:17)

  * add "dollar const" for all predictions

## prediction-api:0.2.18 (28.12.2021 12:07)

  * remove norming

## prediction-api:0.2.16 (Thu, 23 Dec 2021 12:00:20 +0300)

  * swagger-ui from external sources

## prediction-api:0.2.15 (Thu, 21 Dec 2021 11:00:20 +0300)

  * daily ​update ​(from ​config, ​10am ​default)

## prediction-api:0.2.14 (Thu, 21 Dec 2021 11:00:20 +0300)

  * daily ​update ​(from ​config, ​6am ​default)

## prediction-api:0.2.9 (Thu, 15 Dec 2021 17:00:20 +0300)

  * refactoring

## prediction-api:0.2.7 (Thu, 10 Dec 2021 18:00:20 +0300)

  * gunicorn ​+ ​eventlet

## prediction-api:0.2.4 (Thu, 08 Dec 2021 14:00:20 +0300)

  * run via hypercorn + Quart

## prediction-api:0.2.3 (Thu, 08 Dec 2021 17:00:20 +0300)

  * split gunicorn for monitoring and app

## prediction-api:0.2.2 (Thu, 08 Dec 2021 15:00:20 +0300)

  * fix response 422 with empty configuration

## prediction-api:0.2.1 (Thu, 08 Dec 2021 12:00:20 +0300)

  * run via hypercorn + WsgiToAsgi

## prediction-api:0.2.0 (Thu, 07 Dec 2021 17:00:20 +0300)

  * run via uvicorn.workers.UvicornWorker

# prediction-api:0.1.27 (Thu, 07 Oct 2021 17:00:20 +0300)

  * increase update rate

## prediction-api:0.1.26 (Thu, 23 Sep 2021 15:39:20 +0300)

  * fix logging for quantile model

## prediction-api:0.1.25 (Tue, 21 Sep 2021 12:41:08 +0300)

  * add nirvana instance to logging

## prediction-api:0.1.24 (Thu, 22 Apr 2021 15:34:52 +0300)

  * add retries for data updating process

## prediction-api:0.1.23 (Wed, 09 Dec 2020 17:11:24 +0300)

  * remove memcache dependency
  * support dealer matrix for  tradein price

## prediction-api:0.1.22 (Fri, 04 Dec 2020 16:48:48 +0300)

  * better include features logic

## prediction-api:0.1.21 (Mon, 30 Nov 2020 15:39:44 +0300)

  * change normalization source

## prediction-api:0.1.20 (Tue, 24 Nov 2020 16:38:58 +0300)

  * tech bump version

## prediction-api:0.1.19 (Tue, 24 Nov 2020 15:37:32 +0300)

  * Add normalization support. Set it as default for general/dealers

## prediction-api:0.1.18 (Tue, 14 Apr 2020 09:23:30 +0300)

  * multiple models support
  * dealers model
  * quantile rergerssion
  * catboost features-vector in JSON-response

## prediction-api:0.1.17 (Wed, 01 Apr 2020 13:27:09 +0300)

  * correct sigma for intervals

## prediction-api:0.1.16 (Fri, 27 Mar 2020 15:01:23 +0300)

  * new tradein for low-price 

## prediction-api:0.1.15 (Tue, 17 Mar 2020 12:28:03 +0300)

  * python 3.6->3.7
  * better logging

## prediction-api:0.1.14 (Wed, 12 Feb 2020 14:24:02 +0300)

  * use different error rates for old and non-old cars
  * build python from source

## prediction-api:0.1.13 (Thu, 5 Dec 2019 17:59:58 +0300)
 
  * fix bug with pts datatype

## prediction-api:0.1.12 (Tue, 26 Nov 2019 19:00:09 +0300)
 
  * new registry
  * monotonic model supported
  * fix bug with relative mileage feature

## prediction-api:0.1.11 (Tue, 22 Oct 2019 14:32:15 +0300)

  * support default geo_id

## prediction-api:0.1.10 (Mon, 07 Oct 2019 16:49:04 +0300)

  * fix feature generation and tradein coef

## prediction-api:0.1.9 (Mon, 07 Oct 2019 14:45:56 +0300)

  * use all regions from geobase

## prediction-api:0.1.8 (Thu, 03 Oct 2019 16:26:00 +0300)

  * more validation
  * fix issues with error logging

## prediction-api:0.1.7 (Tue, 17 Sep 2019 09:46:47 +0300)

  * json stdout logging
  * memcached support for metrics in monitoring app

## prediction-api:0.1.6 (Fri, 13 Sep 2019 15:05:02 +0300)

  * huge refactoring
  * split feature prepare and prediction processes in different classes
  * removed "last" model
  * hierarchical stat support
  * model update without service restart

## prediction-api:0.1.5 (Fri, 02 Aug 2019 16:13:59 +0300)

  * bump version

## prediction-api:0.1.4 (Fri, 02 Aug 2019 10:17:17 +0300)

  * Use global minimum for price ranges

## prediction-api:0.1.3 (Wed, 22 May 2019 13:44:15 +0300)

 
 * fix error code in swagger
 * VSANALYTICS-4661: support defaults for feature values
 * VSANALYTICS-4650: support tradein coefficients instead of single constant
 * fix negative values caused by year feature

## prediction-api:0.1.2 (Mon, 22 Apr 2019 09:58:18 +0300)

  * support same json and protobuf scheme
  * new swagger

## prediction-api:0.1.1  (Mon, 08 Apr 2019 12:01:01 +0300)

  * initial
