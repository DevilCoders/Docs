## `/v1/maps/getPointInfo`

request
```json
{
	"country_code": "ru",
	"lat": 15.624144117265729,
	"lng": 7.9526889116598625,
	"check_zone": 1
}
```

response
```json
{
	"status": "OK",
	"data": {
		"lowerCorner": "15.271199,4.242096",
		"upperCorner": "23.518287,15.9956",
		"address": "Agadez",
		"lat": 19.470976,
		"lng": 10.496643000000001,
		"pointCountryCode": "ne",
		"zone_id": 0
	}
}
```

## `/v1/launch`

request
```json
{
	"country_code": "ne",
	"zone_id": 0
}
```

response
```json
{
	"status": "OK",
	"data": {
		"passenger": {
			"guid": "8b54ec77-22a4-4d49-8cc8-5d8fd2f3d63e",
			"msisdn": "79996194119",
			"fb_token": null,
			"first_name": "Vladimir",
			"last_name": "",
			"gender": null,
			"date_of_birth": null,
			"email_address": null,
			"avatar": null,
			"measurement_units": "metric",
			"hour_format": "12",
			"users_levels_id": null,
			"banned": true,
			"avg_rating": "5.00",
			"internal_comments": "",
			"language_id": 1,
			"number_of_trips": 0,
			"status": "completed",
			"created_at": "2021-04-14 14:21:22",
			"updated_at": "2021-04-14 15:26:03",
			"country_id": null,
			"is_blocked": "0",
			"sign_up_date": "2021-04-14 14:21:44",
			"block_reason_id": null,
			"block_reason_text": null,
			"country_code": "ne",
			"first_offer_created": "0",
			"first_order_created": "0",
			"is_received_push_notification": true,
			"is_deleted": "0",
			"enc_hash": "***",
			"channel_auth_token": "***",
			"locationLastUpdateTime": 1618413963,
			"driver": {
				"guid": "918988ec-4ab3-49b8-80ff-d7df2506bc5a",
				"avg_rating": "5.00",
				"current_balance": "0.00",
				"city_id": null,
				"country_id": null,
				"partner_id": null,
				"has_vehicle": "0",
				"internal_comments": "",
				"reg_step": "",
				"number_of_trips": 0,
				"driver_status": "new",
				"created_at": "2021-04-14 14:21:44",
				"updated_at": "2021-04-14 14:21:44",
				"moderation_data": "",
				"sign_up_date": null,
				"first_bid_created": "0",
				"first_order_created": "0",
				"is_for_testing": "0",
				"daily_income": "0",
				"vehicle": null,
				"country": null
			}
		},
		"country": null,
		"current_language": "en",
		"current_language_id": 1,
		"detected_country_code": "ne",
		"privacyPageLink": "https:\/\/rida.app\/en\/privacy?mobile=true&deviceType=iPhone",
		"last_order_guid": ""
	}
}
```

## `/v1/getFakeOffers`

request - query only

response
```json
{
	"status": "OK",
	"data": [{
		"order_ts": 1585299643,
		"point_a_lat": 9.0707398000000001,
		"point_a_lng": 7.4570654000000003,
		"point_a": "2410 Lusaka St, Abuja, Nigeria",
		"point_b_lat": 9.1022394000000002,
		"point_b_lng": 7.4474293999999999,
		"point_b": "Katampe Rd, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585299643.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "6578ab7b-6988-4988-b095-b178bfa90091",
		"user_rate": 4.9000000000000004,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15852996436883.jpeg",
		"user_first_name": "Ebuka",
		"payment_method_id": 3,
		"initial_price": 600,
		"comment": "",
		"order_guid": "de6efaf5-6ae2-4625-9438-8f64b2532766",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585300947,
		"point_a_lat": 9.0881679999999996,
		"point_a_lng": 7.4247534999999996,
		"point_a": "Airforce Hotel, Abuja, Nigeria",
		"point_b_lat": 9.0764391,
		"point_b_lng": 7.4253855,
		"point_b": "Jabbi Lake Mall, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585300947.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "29e53586-d521-4b9d-9ab1-e787d585a0e1",
		"user_rate": 4.7000000000000002,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853009472161.jpeg",
		"user_first_name": "Uche",
		"payment_method_id": 3,
		"initial_price": 500,
		"comment": "",
		"order_guid": "f6108a55-c4ab-4108-a566-e8bbded2878d",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585301074,
		"point_a_lat": 9.0388415999999996,
		"point_a_lng": 7.4630887000000001,
		"point_a": "National Hospital, Abuja, Nigeria",
		"point_b_lat": 9.0552118000000004,
		"point_b_lng": 7.4895766999999998,
		"point_b": "Ceddi Plaza, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585301075.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "6d3a5413-fc9a-4149-8b47-95a041e55889",
		"user_rate": 4.9000000000000004,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853010748138.jpeg",
		"user_first_name": "Adamu",
		"payment_method_id": 3,
		"initial_price": 500,
		"comment": "",
		"order_guid": "caf9fc8d-c6f7-4958-a3bf-5d95d16c8ba4",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585301346,
		"point_a_lat": 9.0677251999999999,
		"point_a_lng": 7.4515440000000002,
		"point_a": "Berger Junction, Abuja, Nigeria",
		"point_b_lat": 9.0804679999999998,
		"point_b_lng": 7.4144394,
		"point_b": "Emab Plaza, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585301347.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "4ac1522f-61ed-4788-8987-d4b76a22fcc7",
		"user_rate": 4.7000000000000002,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853013467865.jpeg",
		"user_first_name": "Sani",
		"payment_method_id": 3,
		"initial_price": 450,
		"comment": "",
		"order_guid": "05efcd05-81b5-475c-a959-fe7ca24152e4",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585301510,
		"point_a_lat": 9.0686464999999998,
		"point_a_lng": 7.4659740000000001,
		"point_a": "Banex, Wuse Market, Abuja, Nigeria",
		"point_b_lat": 9.0742863000000007,
		"point_b_lng": 7.4949810000000001,
		"point_b": "Transcorp Hiltion, Abuja,Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585301510.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "8bd1ee44-4e8d-47eb-82b2-d5b0b088bda5",
		"user_rate": 4.7000000000000002,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853015105805.jpeg",
		"user_first_name": "Suleyman",
		"payment_method_id": 3,
		"initial_price": 450,
		"comment": "",
		"order_guid": "40106b14-189a-40e6-834b-79b25da6f064",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585301981,
		"point_a_lat": 9.0447968999999997,
		"point_a_lng": 7.4859257000000001,
		"point_a": "Chelsea Hotel, Abuja, Nigeria",
		"point_b_lat": 9.1148588999999998,
		"point_b_lng": 7.3901494000000003,
		"point_b": "612 Rd, Gwarinpa, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585301982.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "402d3875-e4b6-4b76-b2b1-06c763f9f9be",
		"user_rate": 4.7999999999999998,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853019817399.jpeg",
		"user_first_name": "Biola",
		"payment_method_id": 3,
		"initial_price": 550,
		"comment": "",
		"order_guid": "f5e30f7b-ae86-4ccb-a8fa-124b686e94dd",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585302091,
		"point_a_lat": 9.0304573999999995,
		"point_a_lng": 7.4934335000000001,
		"point_a": "Dominos Pizza, Garki, Abuja, Nigeria",
		"point_b_lat": 9.1098896000000007,
		"point_b_lng": 7.4042408999999996,
		"point_b": "613 Rd, Gwarinpa, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585302092.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "b376f423-de88-4533-8ab8-3a76849041d5",
		"user_rate": 4.9000000000000004,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853020919591.jpeg",
		"user_first_name": "Ngozi",
		"payment_method_id": 3,
		"initial_price": 700,
		"comment": "",
		"order_guid": "2685922c-d3e4-4d5d-b5a3-fde8a535a977",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585302916,
		"point_a_lat": 9.0764391,
		"point_a_lng": 7.4253855,
		"point_a": "Jabbi Lake Mall, Abuja, Nigeria",
		"point_b_lat": 9.0799716999999998,
		"point_b_lng": 7.5124899000000003,
		"point_b": "Ventures Park, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585302916.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "f7929def-5d0c-40f0-a09c-5192c9e138fe",
		"user_rate": 4.9000000000000004,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853029160329.jpeg",
		"user_first_name": "Adebola",
		"payment_method_id": 3,
		"initial_price": 1000,
		"comment": "",
		"order_guid": "1af2fad0-d6e3-4d52-8cd7-0cb22d109c83",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585303034,
		"point_a_lat": 9.054964,
		"point_a_lng": 7.4403116000000002,
		"point_a": "Efab Mall, Abuja, Nigeria",
		"point_b_lat": 9.0685828999999991,
		"point_b_lng": 7.4660565999999999,
		"point_b": "Wuse Market, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585303034.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "31711eb3-e845-4ac1-8557-7e8a35db2496",
		"user_rate": 4.9000000000000004,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853030342047.jpeg",
		"user_first_name": "Opeyemi",
		"payment_method_id": 3,
		"initial_price": 800,
		"comment": "",
		"order_guid": "008d42cd-6aec-4bd7-ab47-404e7b5e1782",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585303185,
		"point_a_lat": 9.0242626999999995,
		"point_a_lng": 7.4733001000000003,
		"point_a": "Federal Secretariat, Abuja, Nigeria",
		"point_b_lat": 9.0637348000000006,
		"point_b_lng": 7.4331038999999999,
		"point_b": "Jabi Motorpark, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585303185.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "95367e96-bc67-4414-ab2a-fe3f213a25f1",
		"user_rate": 4.9000000000000004,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853031851633.jpeg",
		"user_first_name": "Fatima",
		"payment_method_id": 3,
		"initial_price": 1000,
		"comment": "",
		"order_guid": "85f668db-4570-49f2-a117-a5540d50c7bb",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585303302,
		"point_a_lat": 9.0470240999999998,
		"point_a_lng": 7.5020518999999997,
		"point_a": "FCDA Abuja, Nigeria",
		"point_b_lat": 9.1004147999999994,
		"point_b_lng": 7.4119165000000002,
		"point_b": "32 Crescent, Gwarinpa, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585303303.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "b575c0a5-744b-49a6-9a41-95196c778ca2",
		"user_rate": 4.9000000000000004,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853033028352.jpeg",
		"user_first_name": "Funso",
		"payment_method_id": 3,
		"initial_price": 1000,
		"comment": "",
		"order_guid": "776487ca-dab6-491f-9041-d1bd9bb8e849",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585303473,
		"point_a_lat": 9.0334742000000006,
		"point_a_lng": 7.4850089999999998,
		"point_a": "Garki Hospital, Abuja, Nigeria",
		"point_b_lat": 9.0859976000000007,
		"point_b_lng": 7.4942472000000002,
		"point_b": "Maitama Farmers Market, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585303473.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "bc1358fd-df19-42a1-a4a3-7b16403c5061",
		"user_rate": 4.9000000000000004,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853034734274.jpeg",
		"user_first_name": "Maryam",
		"payment_method_id": 3,
		"initial_price": 800,
		"comment": "",
		"order_guid": "d69b4e0e-5871-4c12-a103-629876d2f8b5",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585303623,
		"point_a_lat": 9.0461240000000007,
		"point_a_lng": 7.3419037999999999,
		"point_a": "Idu Train Terminal, Abuja, Nigeria",
		"point_b_lat": 9.0529702000000007,
		"point_b_lng": 7.4791458000000004,
		"point_b": "Grand Square Shopping Mall, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585303623.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "cf80c5da-3b87-4e72-a3c0-9805eba4256d",
		"user_rate": 4.7999999999999998,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853036234108.jpeg",
		"user_first_name": "Alli",
		"payment_method_id": 3,
		"initial_price": 1500,
		"comment": "",
		"order_guid": "f8154b16-7229-412e-bf63-52561b1dbc29",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585317325,
		"point_a_lat": 9.0502851999999994,
		"point_a_lng": 7.5064418999999996,
		"point_a": "KFC Garki, Abuja, Nigeria",
		"point_b_lat": 8.9927765999999991,
		"point_b_lng": 7.3553799,
		"point_b": "Lugbe Plaza, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585317325.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "56102246-d586-4f65-9837-a30c90f11f24",
		"user_rate": 4.9000000000000004,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853173251361.jpeg",
		"user_first_name": "Victor",
		"payment_method_id": 3,
		"initial_price": 1500,
		"comment": "",
		"order_guid": "c7549231-d930-4e52-ae46-d3707ec2895f",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585317684,
		"point_a_lat": 9.0362028999999993,
		"point_a_lng": 7.5208427999999996,
		"point_a": "Asokoro Shopping Mall, Abuja, Nigeria",
		"point_b_lat": 9.0469226000000003,
		"point_b_lng": 7.4739398000000001,
		"point_b": "River Plaza and Mall, Constitution Ave, Central Business Dis, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585317685.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "d234f679-b66c-474f-979c-3221ecd5f1b5",
		"user_rate": 4.7000000000000002,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853176849989.jpeg",
		"user_first_name": "Mayowa",
		"payment_method_id": 3,
		"initial_price": 850,
		"comment": "",
		"order_guid": "82fd4762-1741-4f30-bac4-d4670ea25dfc",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585317876,
		"point_a_lat": 9.0358894999999997,
		"point_a_lng": 7.4846295999999999,
		"point_a": "Garki Market, Abuja, Nigeria",
		"point_b_lat": 8.9847906999999996,
		"point_b_lng": 7.4928501000000001,
		"point_b": "Novare Mall, Apo 2, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585317876.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "bd3bc8ad-0e20-4ff1-9ee5-a43412d0518f",
		"user_rate": 4.7000000000000002,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853178766119.jpeg",
		"user_first_name": "Funke",
		"payment_method_id": 3,
		"initial_price": 650,
		"comment": "",
		"order_guid": "2dfdf887-553c-4721-a9a2-5d83dda44832",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585318110,
		"point_a_lat": 9.0431413999999997,
		"point_a_lng": 7.4920783000000002,
		"point_a": "Abuja International Conference Centre, Abuja, Nigeria",
		"point_b_lat": 9.0599944000000008,
		"point_b_lng": 7.4898558,
		"point_b": "National Mosque, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585318110.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "82c46bc5-c360-4580-88e3-d13786d7a70c",
		"user_rate": 4.7000000000000002,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853181102228.jpeg",
		"user_first_name": "Aminu",
		"payment_method_id": 3,
		"initial_price": 400,
		"comment": "",
		"order_guid": "352408ff-086f-4f06-95da-1f4540abfd3a",
		"payment_method": "Cash payment"
	}, {
		"order_ts": 1585337643,
		"point_a_lat": 9.0519786999999994,
		"point_a_lng": 7.4946088,
		"point_a": "National Christian Centre, Abuja, Nigeria",
		"point_b_lat": 9.0663623999999992,
		"point_b_lng": 7.4454517999999998,
		"point_b": "Utako Market, Abuja, Nigeria",
		"order_status": "PENDING",
		"direction_map_url": "https:\/\/api.rida.app\/images\/fake_offer\/route_images\/1585337643.jpg",
		"direction_duration": "",
		"direction_distance": "",
		"user_guid": "5e62aaeb-c9cc-45ab-b8a7-e3fb46ce800e",
		"user_rate": 4.7999999999999998,
		"user_avatar": "https:\/\/api.rida.app\/images\/fake_offer\/1\/15853182417672.jpeg",
		"user_first_name": "Yinka",
		"payment_method_id": 3,
		"initial_price": 850,
		"comment": "",
		"order_guid": "507de51a-47f6-4063-a5a1-374b426bac17",
		"payment_method": "Cash payment"
	}]
}
```

## `/v1/getOffers`

request
```json
{
	"page": 1,
	"type": "all" | "user" | "driver"
}
```

response
```json
{
	"status": "OK",
	"data": {
		"offers": [],
		"offersCount": 0,
		"hasNextPage": false
	}
}
```

## `/v1/getSuggestedPrice`

request
```json
{
	"zone_id": 0,
	"duration": 11109,
	"country_id": 12,
	"distance": 184587
}
```

response
```json
{
	"status": "OK",
	"data": {
		"suggestedPrice": "9100"
	}
}
```

## `/v1/auth/updateData`

request
```json
{
	"field_name": "is_received_push_notification",
	"field_value": "0",
	"token": "token"
}
```

response
```json
{
	"status": "OK",
	"data": {
		"passenger": {
			"guid": "8b54ec77-22a4-4d49-8cc8-5d8fd2f3d63e",
			"msisdn": "79996194119",
			"fb_token": null,
			"first_name": "Vladimir",
			"last_name": "",
			"gender": null,
			"date_of_birth": null,
			"email_address": null,
			"avatar": null,
			"measurement_units": "metric",
			"hour_format": "12",
			"users_levels_id": null,
			"banned": true,
			"avg_rating": "5.00",
			"internal_comments": "",
			"language_id": 1,
			"number_of_trips": 0,
			"status": "completed",
			"created_at": "2021-04-14 14:21:22",
			"updated_at": "2021-04-14 15:57:31",
			"country_id": null,
			"is_blocked": "0",
			"sign_up_date": "2021-04-14 14:21:44",
			"block_reason_id": null,
			"block_reason_text": null,
			"country_code": "ng",
			"first_offer_created": "0",
			"first_order_created": "0",
			"is_received_push_notification": false,
			"is_deleted": "0",
			"locationLastUpdateTime": 1618416841,
			"driver": {
				"guid": "918988ec-4ab3-49b8-80ff-d7df2506bc5a",
				"avg_rating": "5.00",
				"current_balance": "0.00",
				"city_id": null,
				"country_id": null,
				"partner_id": null,
				"has_vehicle": "0",
				"internal_comments": "",
				"reg_step": "",
				"number_of_trips": 0,
				"driver_status": "new",
				"created_at": "2021-04-14 14:21:44",
				"updated_at": "2021-04-14 14:21:44",
				"moderation_data": "",
				"sign_up_date": null,
				"first_bid_created": "0",
				"first_order_created": "0",
				"is_for_testing": "0",
				"daily_income": "0",
				"vehicle": null,
				"country": null
			}
		},
		"token": "***"
	}
}
```

## `/v1/offer/create`

request
```json
{
	"direction_distance": "",
	"device_brand_model": "iPhone12,1",
	"used_bonus": 0,
	"is_push_sent": false,
	"order_ts": 1618416841,
	"zone_id": 0,
	"point_b": "44aguiyi Aguiyi Ironsi St, Wuse ",
	"direction_distance_len": 184587,
	"offer_guid": "E9FA920D-265B-42A8-A682-5E492FE0ACB6",
	"direction_duration": "",
	"point_a_long": 7.3126261308789253,
	"user_phone_number": "79996194119",
	"payment_method": "Cash payment",
	"point_b_lat": 9.0837594999999993,
	"point_a_lat": 8.106333021293187,
	"device_scale": "2",
	"point_a": "Unnamed Road",
	"numberOfTrips": 0,
	"lang_code": "en",
	"order_status": "PENDING",
	"payment_method_id": 3,
	"is_shown": false,
	"creator_push_token": "***",
	"user_guid": "8b54ec77-22a4-4d49-8cc8-5d8fd2f3d63e",
	"application_version": "20101",
	"user_rate": 5,
	"application_id": "83B42E1B-3EF2-4B93-8418-CBBE09CF1F42",
	"device_type": "iPhone",
	"user_first_name": "Vladimir",
	"expire_ts": 1618416841,
	"country_id": "12",
	"direction_duration_ts": 11109,
	"accepted_drivers": [

	],
	"suggestedPrice": "9 100 NGN",
	"initial_price": 9500,
	"available_bonus": 0,
	"point_b_long": 7.4860148000000004,
	"user_avatar": "",
	"direction_map_url": "https:\/\/maps.googleapis.com\/maps\/api\/staticmap?size=600x300&maptype=roadmap&key=AIzaSyDYsoQNrUvh-uk49eYjiI8NfSjHBhRwrNw&path=color%3A0x000000%7Cweight%3A5%7Cenc%3Aarop%40kisk%40iDwAeCwLiNjIqUrKaMfEaPnKuStJqV%60MkKlKuGrMaNvMeD%7CAyJxKyJvRsBfK_F%7EQoJnQkQbk%40sPxj%40yXpp%40gHlHkF%7CHw%40bEIrN%7B%40pOqB%7C%5DsDbM_AxIaApK%5C%7CQEvUa%40xaB%7EFtl%40oAzX%7BKb%60%40aE%7ERiIdNmd%40%7Ef%40_JpFeGhH_c%40pg%40kRn%5Bij%40p%5DgNdYaJ%7EKkBfGe%40%7CJvAjIt%40fGyGxP%7D%40xCmCWkDm%40sKyEc%60%40%7D_%40uHqD%7BTyB%7Be%40mBoOYs%5EfBgUvCeLbHig%40pv%40eh%40rx%40mMfNia%40vW%7BtA%60%7C%40gUzLkQlE_XlAsT%7B%40eU%40qJjGkGpKwEfCcPhCyk%40tIkLdFyMzToUlh%40ia%40v%7D%40sF%7CGkLtFus%40fTe%5ClDw%5Bg%40_o%40uDmcATk%7E%40vNkf%40rIqXfKsc%40fXiMtBeT%7D%40gUkDp%40pBJ%7ECoBhGyL%7ELoFnDst%40p%5CgUfKaHtGoF%7CIaO%7CEyOfIkK%60OmJxOoYtTygA%7Cv%40%7BWrM%7BKjDob%40fCgHdBs%5Eb%5BmFpIsd%40teA%7DBzH%5Df%5EcAjFoDtBcEOgHgCoEPmBhCLpE%60HjItAtFkC%60Ta%5Ej%7BB%7D%5CxiB%7DNdaAyJhq%40cM%7Eq%40_%40bBWfAgFAuBDe%40%40wIl%40oG%7C%40a_%40zGso%40%7CLw%7E%40lQqe%40fJyzAlYmcBz%5BwlEr%7B%40gu%40tMw%7C%40bPsN%5EaS%7BA%7DTkBwr%40uHapAgNwtAeOyqAwNqz%40kOsdAsQc%60AeP_f%40kI%7Dx%40wPapAuf%40q%60D_pAie%40aR_XuMke%40ia%40uv%40au%40whAmfAqlBkiBkW%7BVcWg%5CoLqTii%40%7DeAocAipBsSwRuSiIymBuXagAgOeRwEofCy%7B%40cfBam%40%7DVuNg%5EwWym%40gd%40%7DToPyQiJuVwEq%60%40yD_fAmKeP%7DCuJ%7DD%7DP_M%7BGgJeMa%5CsToo%40wSgj%40gMkPwQwOsYcVed%40a_%40mp%40wh%40sq%40c%5Bg%60Bur%40aIoEaNwGeBcCs%40mIhEaJd%60%40et%40tk%40cfAle%40_bAtMqXfT%7Dc%40d_%40_%7C%40ph%40i%7BAzn%40ohBn%5EeeAf%5EaqAfVk%7B%40zR%7Bw%40nYstAxDqRjFkc%40Qwe%40yE_%5CyNk%60%40wQoZoKaOqMaSeXm%5BaMmNqTkW%7DQoSuIcMuJoSwYcv%40k_AicCcc%40y_Aqh%40m%60Amc%40ah%40ac%40u%60%40md%40%7Da%40ss%40qp%40ik%40al%40g%5Eyk%40sQw%5DcCmJuEa%40qHSmG%7DAeFwDeGoVyBeSdAm%40fBz%40k%40xBkL%60FiLrE%7BKdCcS%60Dcl%40b%40sZdDkTnDeLXqLs%40%7DMaDyLmGiH%7BGu%5Dic%40eRwXsQk%5EcQaP%7DKmFuMaDrAoFvJcJtPaKlCZrDjCtB%7EA%7EBwAtBeB%7CBwCbDoIxEmQtAkC&markers=icon:https:\/\/api.rida.app\/img\/point_from_orange.png%7C8.1063330212932,7.3126261308789&markers=icon:https:\/\/api.rida.app\/img\/point_to_green.png%7C9.0837595,7.4860148",
	"os_version": "14.4.2"
}
```

request
```json
{
	"status": "OK",
	"data": {
		"offer": {
			"offer_guid": "084d4e63-f8ef-49da-8003-bfa6c65746d5",
			"user_guid": "8b54ec77-22a4-4d49-8cc8-5d8fd2f3d63e",
			"user": {
				"guid": "8b54ec77-22a4-4d49-8cc8-5d8fd2f3d63e",
				"msisdn": "79996194119",
				"fb_token": null,
				"first_name": "Vladimir",
				"last_name": "",
				"gender": null,
				"date_of_birth": null,
				"email_address": null,
				"avatar": null,
				"measurement_units": "metric",
				"hour_format": "12",
				"users_levels_id": null,
				"banned": true,
				"avg_rating": "5.00",
				"internal_comments": "",
				"language_id": 1,
				"number_of_trips": 0,
				"status": "completed",
				"created_at": "2021-04-14 14:21:22",
				"updated_at": "2021-04-14 15:57:31",
				"country_id": null,
				"is_blocked": "0",
				"sign_up_date": "2021-04-14 14:21:44",
				"block_reason_id": null,
				"block_reason_text": null,
				"country_code": "ng",
				"first_offer_created": "0",
				"first_order_created": "0",
				"is_received_push_notification": false,
				"is_deleted": "0",
				"locationLastUpdateTime": 1618416842
			},
			"driver_guid": null,
			"driver": null,
			"point_a": "Unnamed Road",
			"point_a_lat": 8.106333021293187,
			"point_a_long": 7.3126261308789253,
			"point_b": "44aguiyi Aguiyi Ironsi St, Wuse ",
			"point_b_lat": 9.0837594999999993,
			"point_b_long": 7.4860148000000004,
			"points_data": null,
			"entrance": null,
			"comment": null,
			"price_sequence": 1,
			"initial_price": 9500,
			"final_price": 0,
			"available_bonus": 0,
			"used_bonus": 0,
			"offer_status": "PENDING", // в запросе был order_status ...?
			"payment_method_id": 3,
			"payment_method": {
				"id": 3,
				"alias": "cash",
				"sort_order": 1,
				"show_status": "1",
				"current": {
					"id": 4,
					"payment_methods_id": 3,
					"language_id": 1,
					"name": "Cash payment",
					"show_status": "1"
				}
			},
			"city_id": 0,
			"zone_id": 0,
			"country_id": 12,
			"offer_cancel_reason_id": 0,
			"offer_cancel_reason_text": null,
			"trip_estimated_duration": null,
			"direction_map_url": "https:\/\/maps.googleapis.com\/maps\/api\/staticmap?size=600x300&maptype=roadmap&key=AIzaSyDYsoQNrUvh-uk49eYjiI8NfSjHBhRwrNw&path=color%3A0x000000%7Cweight%3A5%7Cenc%3Aarop%40kisk%40iDwAeCwLiNjIqUrKaMfEaPnKuStJqV%60MkKlKuGrMaNvMeD%7CAyJxKyJvRsBfK_F%7EQoJnQkQbk%40sPxj%40yXpp%40gHlHkF%7CHw%40bEIrN%7B%40pOqB%7C%5DsDbM_AxIaApK%5C%7CQEvUa%40xaB%7EFtl%40oAzX%7BKb%60%40aE%7ERiIdNmd%40%7Ef%40_JpFeGhH_c%40pg%40kRn%5Bij%40p%5DgNdYaJ%7EKkBfGe%40%7CJvAjIt%40fGyGxP%7D%40xCmCWkDm%40sKyEc%60%40%7D_%40uHqD%7BTyB%7Be%40mBoOYs%5EfBgUvCeLbHig%40pv%40eh%40rx%40mMfNia%40vW%7BtA%60%7C%40gUzLkQlE_XlAsT%7B%40eU%40qJjGkGpKwEfCcPhCyk%40tIkLdFyMzToUlh%40ia%40v%7D%40sF%7CGkLtFus%40fTe%5ClDw%5Bg%40_o%40uDmcATk%7E%40vNkf%40rIqXfKsc%40fXiMtBeT%7D%40gUkDp%40pBJ%7ECoBhGyL%7ELoFnDst%40p%5CgUfKaHtGoF%7CIaO%7CEyOfIkK%60OmJxOoYtTygA%7Cv%40%7BWrM%7BKjDob%40fCgHdBs%5Eb%5BmFpIsd%40teA%7DBzH%5Df%5EcAjFoDtBcEOgHgCoEPmBhCLpE%60HjItAtFkC%60Ta%5Ej%7BB%7D%5CxiB%7DNdaAyJhq%40cM%7Eq%40_%40bBWfAgFAuBDe%40%40wIl%40oG%7C%40a_%40zGso%40%7CLw%7E%40lQqe%40fJyzAlYmcBz%5BwlEr%7B%40gu%40tMw%7C%40bPsN%5EaS%7BA%7DTkBwr%40uHapAgNwtAeOyqAwNqz%40kOsdAsQc%60AeP_f%40kI%7Dx%40wPapAuf%40q%60D_pAie%40aR_XuMke%40ia%40uv%40au%40whAmfAqlBkiBkW%7BVcWg%5CoLqTii%40%7DeAocAipBsSwRuSiIymBuXagAgOeRwEofCy%7B%40cfBam%40%7DVuNg%5EwWym%40gd%40%7DToPyQiJuVwEq%60%40yD_fAmKeP%7DCuJ%7DD%7DP_M%7BGgJeMa%5CsToo%40wSgj%40gMkPwQwOsYcVed%40a_%40mp%40wh%40sq%40c%5Bg%60Bur%40aIoEaNwGeBcCs%40mIhEaJd%60%40et%40tk%40cfAle%40_bAtMqXfT%7Dc%40d_%40_%7C%40ph%40i%7BAzn%40ohBn%5EeeAf%5EaqAfVk%7B%40zR%7Bw%40nYstAxDqRjFkc%40Qwe%40yE_%5CyNk%60%40wQoZoKaOqMaSeXm%5BaMmNqTkW%7DQoSuIcMuJoSwYcv%40k_AicCcc%40y_Aqh%40m%60Amc%40ah%40ac%40u%60%40md%40%7Da%40ss%40qp%40ik%40al%40g%5Eyk%40sQw%5DcCmJuEa%40qHSmG%7DAeFwDeGoVyBeSdAm%40fBz%40k%40xBkL%60FiLrE%7BKdCcS%60Dcl%40b%40sZdDkTnDeLXqLs%40%7DMaDyLmGiH%7BGu%5Dic%40eRwXsQk%5EcQaP%7DKmFuMaDrAoFvJcJtPaKlCZrDjCtB%7EA%7EBwAtBeB%7CBwCbDoIxEmQtAkC&markers=icon:https:\/\/api.rida.app\/img\/point_from_orange.png%7C8.1063330212932,7.3126261308789&markers=icon:https:\/\/api.rida.app\/img\/point_to_green.png%7C9.0837595,7.4860148",
			"direction_duration_ts": 11109,
			"direction_distance_len": 184587,
			"bids": null,
			"review": {},
			"near_drivers_count": 0,
			"created_at": "2021-04-14T16:14:02.117000Z",
			"started_at": "2021-04-14T16:14:02.000000Z",
			"expired_at": "2021-04-14T16:17:02.000000Z",
			"expired_after": 179
		},
		"connect_channel_url": "https:\/\/events.rida.app\/sub\/user"
	}
}
```

## `/v1/offer/passengerCancel`

request
```json
{
	"offer_guid": "084d4e63-f8ef-49da-8003-bfa6c65746d5",
	"offer_cancel_reason_id": 10,
	"offer_cancel_reason_text": ""
}
```

response
```json
{
	"status": "OK",
	"data": []
}
```
