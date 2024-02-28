# ParkNcharge APIs

This repository includes all the details related to ParkNcharge APIs. It doesn't include the source code for each services, but repository links are provided.

# Table of Contents

- [Authentication APIs](#authentication-apis)
  - [Base URL](#authentication-base-url)
  - [GET /api/auth/v1/token](#get-apiauthv1token)
  - [POST /api/v1/login](#post-apiv1login)
  - [POST /api/v1/logout](#post-apiv1logout)
  - [GET /api/auth/v1/refresh](#get-apiauthv1refresh)
  - [POST /api/auth/v1/send-otp](#post-apiauthv1send-otp)
  - [POST /api/auth/v1/verify-otp](#post-apiauthv1verify-otp)
  - [POST /api/auth/v1/change-password/:user_id](#post-apiauthv1change-passworduser_id)
- [Timeslots API](#timeslots)
  - [Base URL](#timeslots-base-url)
  - [GET /api/v1/timeslots/:merchant_id/:evc_id/:current_hour](#get-apiv1timeslotsmerchant_idevc_idcurrent_hour)
- [Reservation](#reservation)
  - [Base URL](#reservation-base-url)
  - [POST /api/v1/slots/reserve](#post-apiv1slotsreserve)
  - [PATCH /api/v1/slots/cancel](#patch-apiv1slotscancel)
  - [GET /api/v1/slots/reservations](#get-apiv1slotsreservations)
  - [GET /booking_reservation/api/v1/slots/check-reservation/:evc_id/:timeslot_id](#get-apiv1slotscheck-reservationevc_idtimeslot_id)
  - [PUT /api/v1/slots/cancel-expired-reservations](#put-apiv1slotscancel-expired-reservations)
  - [POST /api/v1/charge_now](#post-apiv1charge_now)
  - [POST /api/v1/slots/reservations/activate/:reservation_id](#post-apiv1slotsreservationsactivatereservation_id)
  - [POST /api/v1/check_current_time_and_date](#post-apiv1check_current_time_and_date)
  - [Reservation and Charge Now Constraints](#reservation-and-chargenow-constraints)
    - [Reservation](#reservation-1)
    - [Charge Now](#chargenow)
- [Nearby Locations in GraphQL](#nearby-locations-in-graphql)
  - [Query cpo_owners](#query-cpo_owners)
  - [Query locations](#query-locations)
  - [Query locations_with_favorites](#query-location_with_favorites)
  - [Mutation Remove from Favorite Location](#mutation-removefromfavoritelocation)
  - [Mutation Add to Favorite Location](#mutation-addtofavoritelocation)
  - [Query Favorite Locations](#query-favorte_locations)
  - [Query Filter Locations](#query-filter_locations)
  - [Query Filter Locations with Favorites](#query-filter_locations_with_favorites)
- [Socket Server](#socket-server)
  - [Socket URL](#socket-url)

## Authentication APIs

This service consists of the APIs for Login, Logout, Send OTP, Verify OTP, and Change Password.

### Authentication Base URL

`https://services-parkncharge.sysnetph.com/login`

### `GET /api/auth/v1/token`

This API will be used to get a Basic Token to be used for all APIs that don't require authorization, and authentication.

**Response Body**

```json
{
	"status": 200,
	"token": "eyJhbGciOiJIUzI1NiJ9.cGFya25jaGFyZ2UtZGV2ZWxvcGVyLWFwaWtleQ.a2HEcaGP6po2yAAV-ieQNHbCoD6nMGDNWs3fGjrGJds"
}
```

[Back to the top](#parkncharge-apis)

### `POST /api/v1/login`

**Authorization: Bearer BASIC_TOKEN**

**Request Body**

```json
{
	"username": "adriannads",
	"password": "adriannads"
}
```

**Response Body**

```json
{
	"status": 200,
	"data": {
		"access_token": "mvZ21YJAXSC2EruZw0fV8ERTfOHxV4gD9i/JsRqe/w4Q3OIXlBhcem/8fNoHApQNNF75yHs0dcbrnqpepG2IWhgaNdRKuExgFZOERgFCR3JkwaB6aHgdUXWhnv58XDeld9uNEIto1a/vPobRKWwB3lh2R8pTKalxKODb48DTtmtuI6iAFSlVGObkQ4hEPQwzXOeVreMpnmEza6gXdwxsPfBj7TR0JSKcjN+9JfaX1LYM0u1D1UhNGMH+33fmGdjmpFbUb0b+D9BY/nKSq4SdUcxBNnhCmq4oKozqu4eRwcHD17T19Ujgghd7tBI3elXZWXGl91Sk8C34uK8cvy9Fp8TmkWA3fBsDACKnv2mv28fgxPzt8xxjjOp+c79e77tZmuEzvDfiGcoBaPxVbNfaaFG8ahLEGALworgyUyn4rqVVv0bT0qZ4dadPePDmpj2opacbNA+ymiqLo7mwARL4CfS2eQq1J0Y9HKU/2Vv7ciU=",
		"access_expires_in": 1705040589,
		"refresh_token": "mvZ21YJAXSC2EruZw0fV8ERTfOHxV4gD9i/JsRqe/w4Q3OIXlBhcem/8fNoHApQNNF75yHs0dcbrnqpepG2IWhgaNdRKuExgFZOERgFCR3JkwaB6aHgdUXWhnv58XDeld9uNEIto1a/vPobRKWwB3nnQW2N+eajOfSUyGcMhUlSiIT81FW0Hr0fiPobWnrG+vCnyiDnou4NH9GghDK65kqE4Ah5j/oW4va3lGFUOlcustJXwBk9+MIp9YuS9p9ErM/Mej5oCnt6/2bOItxn+VeP7lj0PrmhJUPB6nwqDa5cwqZ9mGT7vr1Ot1l41PxSE0FBMltkHdI6PVrigFXefORnTZ6WI5J3Fw/7caCzibjawtDkUg5nLHUCeKPQsrTwjIMA5vvkpXj/LRzbqxWQ1u1P63E1DogKteeKZAtnjDUoz66DR6lzWc7pfsbcoBmXNQCcvtPelwqw/6Ru6zUlm8gJ7xHJNInYMnsV4L4m9cGU="
	},
	"message": "SUCCESS"
}
```

[Back to the top](#parkncharge-apis)

### `POST /api/v1/logout`

**Authorization: Bearer ACCESS_TOKEN**

**Response**

```json
{
	"status": 200,
	"data": [],
	"message": "Logged out successfully"
}
```

[Back to the top](#parkncharge-apis)

### `GET /api/auth/v1/refresh`

**Authorization: Bearer REFRESH_TOKEN**

**Response Body**

```json
{
	"status": 200,
	"data": {
		"access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7ImlkIjo0NywidXNlcm5hbWUiOiJhZHJpYW5uYWRzIiwicm9sZV9pZCI6NDd9LCJqdGkiOiIxNGFkNTRmYi0wZjdhLTRlNGMtOTZmNy1mZjQ0Y2IzMDZhYjciLCJhdWQiOiJwYXJrbmNoYXJnZS1hcHAiLCJpc3MiOiJwYXJrbmNoYXJnZSIsImlhdCI6MTcwNDA5MDgxMCwidHlwIjoiQmVhcmVyIiwiZXhwIjoxNzA0MDk0NDEwLCJ1c3IiOiJzZXJ2In0.hPw1nUHzsSH3qTZ9IsL_-C0Kp-KLthXnMKDpKFpRpyI",
		"access_expires_in": 1704094410,
		"refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7ImlkIjo0NywidXNlcm5hbWUiOiJhZHJpYW5uYWRzIiwicm9sZV9pZCI6NDd9LCJqdGkiOiIyMTM4ZDY2OC02MWQyLTQzNWUtOTQ1OS1jNWQ2YjM5MTViZWIiLCJhdWQiOiJwYXJrbmNoYXJnZS1hcHAiLCJpc3MiOiJwYXJrbmNoYXJnZSIsImlhdCI6MTcwNDA5MDgxMCwidHlwIjoiQmVhcmVyIiwidXNyIjoic2VydiJ9.tg2tCiT5e0mWUwQR6Ie0-G_4rA4m13p-oqq3RWOHMyo"
	},
	"message": "SUCCESS"
}
```

[Back to the top](#parkncharge-apis)

### `POST /api/auth/v1/send-otp`

**Authorization: Basic TOKEN**

**Request Body**

```json
{
	"email": "adriannadslaurianomarcelo@gmail.com"
}
```

**Response Body**

```json
{
	"status": 200,
	"data": [
		{
			"USER_ID": 47,
			"STATUS": "NEW_CREATED_RECORD"
		}
	],
	"message": "Success"
}
```

[Back to the top](#parkncharge-apis)

### `POST /api/auth/v1/verify-otp`

**Authorization: Basic TOKEN**

**Request Body**

```json
{
	"user_id": 47,
	"otp": 364834
}
```

**Response Body**

```json
{
	"status": 200,
	"data": "SUCCESS",
	"message": "Success"
}
```

[Back to the top](#parkncharge-apis)

### `POST /api/auth/v1/change-password/:user_id`

**Authorization: Basic Token**

**Request Body**

```json
{
	"password": "adriannads"
}
```

**Response**

```json
{
	"status": 200,
	"data": [
		{
			"status": "PASSWORD_UPDATED"
		}
	],
	"message": "Success"
}
```

[Back to the top](#parkncharge-apis)

## Timeslots

This API is for retrieving all of the timeslots for a specific station.

### Timeslots Base URL

`https://services-parkncharge.sysnetph.com/booking_timeslot`

### `GET /api/v1/timeslots/:merchant_id/:evc_id/:current_hour`

**Parameters**

- **merchant_id** - Merchant ID.
- **evc_id** - EV Charger/Station ID.
- **current_hour** - Current hour based on current timezone.

**Response Body**

```json
{
	"status": 200,
	"data": [
		{
			"ev_charger_id": 5,
			"settings_timeslot_id": 1,
			"slot_status": "CHARGING",
			"start": "06:00:00",
			"end": "14:00:00",
			"kwh": 7,
			"date": "2024-01-02T00:43:32.734Z"
		},
		{
			"ev_charger_id": 5,
			"settings_timeslot_id": 2,
			"slot_status": "OFFLINE",
			"start": "14:00:00",
			"end": "22:00:00",
			"kwh": 7,
			"date": "2024-01-02T00:43:32.734Z"
		},
		{
			"ev_charger_id": 5,
			"settings_timeslot_id": 3,
			"slot_status": "OFFLINE",
			"start": "22:00:00",
			"end": "06:00:00",
			"kwh": 7,
			"date": "2024-01-02T00:43:32.734Z"
		}
	],
	"message": "Success"
}
```

[Back to the top](#parkncharge-apis)

## Nearby Merchants

### Nearby Merchants Base URL

`https://services-parkncharge.sysnetph.com/booking_merchants`

### `POST /api/v1/nearby_merchants`

**Authorization: Basic TOKEN**

**Request Body**

```json
{
	"lat": 14.5564414,
	"lng": 121.0218253
}
```

**Response Body**

```json
    "status": 200,
	"data" : [] // list of nearby merchants objects
```

[Back to the top](#parkncharge-apis)

### `POST /api/v1/filter-merchants`

**Authorization: Basic TOKEN**

**Request Body**

```json
{
	"location": {
		"lat": 14.5564414,
		"lng": 121.0218253
	},
	"filter": {
		"city": "Makati",
		"region": "NCR",
		"types": ["GB/T"],
		"meter_types": ["AC"]
	}
}
```

**Response Body**

```json
{
	"status": 200,
	"data": [] // list of filtered merchant objects
}
```

[Back to the top](#parkncharge-apis)

### `GET /api/v1/merchants/:merchant_id/:lat/:lng`

**Authorization: Basic TOKEN**

**Request Parameters**

- **merchant_id** - Merchant ID
- **lat** - Location's latitude
- **lng** - Location's longitude

**Response Body**

```json
{
	"status": 200,
	"data": // merchant object
}
```

> NOTE: If the merchant is not found, it will return a MERCHANT_NOT_FOUND status/message.

[Back to the top](#parkncharge-apis)

## Favorite Merchants

### Favorite Merchants URL

`https://services-parkncharge.sysnetph.com/booking_merchants`

### `POST /api/v1/merchants/favorites/:user_merchant_id`

**Authorization: Bearer ACCESS_TOKEN**

**Parameters**

- user_merchant_id: INT

**Response**

```json
{
	"status": 200,
	"data": []
}
```

[Back to the top](#parkncharge-apis)

### `GET /api/v1/merchants/favorites`

**Authorization: Bearer ACCESS_TOKEN**

**Search Query**

- lat - location's latitude
- lng - location's longitude

**Response Body**

```json
{
	"status": 200,
	"data": [] // list of favorite merchants object
}
```

[Back to the top](#parkncharge-apis)

### `DELETE /api/v1/merchants/favorites`

**Authorization: Bearer ACCESS_TOKEN**

**Search Query**

- merchant_id

**Response**

```json
{
	"status": 200,
	"data": []
}
```

[Back to the top](#parkncharge-apis)

### `POST /api/v1/nearby-favorite-merchants`

> NOTE: This API can be used only when the user is logged in.

**Authorization: Bearer ACCESS_TOKEN**

**Request Body**

```json
{
	"lat": 14.5564414,
	"lng": 121.0218253
}
```

**Response Body**

```json
{
	"status": 200,
	"data": [] // list of merchants
}
```

[Back to the top](#parkncharge-apis)

### `POST /api/v1/filtered-favorite-merchants`

> NOTE: This API can be used only when the user is logged in.

**Authorization: Bearer ACCESS_TOKEN**

**Request Body**

```json
{
	"location": {
		"lat": 14.5564414,
		"lng": 121.0218253
	},
	"filter": {
		"city": "Makati",
		"region": "NCR",
		"types": ["GB/T"],
		"meter_types": ["AC"]
	}
}
```

**Response Body**

```json
"status": 200,
"data" : [] // list of merchants
```

[Back to the top](#parkncharge-apis)

## Reservation

### Reservation Base URL

`https://services-parkncharge.sysnetph.com/booking_reservation`

### `POST /api/v1/slots/reserve`

> NOTE: This API can be used only when the user is logged in.

**Authorization: Bearer ACCESS_TOKEN**

**Request Body**

- **evc_id**
  - EV Charger ID
- **settings_timeslot_id**
  - Timeslot ID. This is one of the data from the individual timeslot from TIMESLOT API ([See Timeslot API](#timeslots))
- **timeslot_date**
  - This is one of the data from the individual timeslot from TIMESLOT API. (Valid date format is YYYY-MM-DD). ([See Timeslot API](#timeslots))
- **next_timeslot_id**
  - ID of the next timeslot from the result list of TIMESLOT API. ([See Timeslot API](#timeslots))
- **next_timeslot_date**
  - Date of the next timeslot from the result list of TIMESLOT API. (Valid date format is YYYY-MM-DD). ([See Timeslot API](#timeslots))
- **date**
  - Current date of user. (Valid date format is YYYY-MM-DD).
- **current_time**
  - Current time of user. (Valid time format is HH:MM:SS).
- **want_to_book**
  - This property by default must be 0. This is an identifier if the user still wants to book his/her chosen timeslot even if it is less than one (1) hour, and even the next timeslot is not available.

```json
{
	"evc_id": 2,
	"settings_timeslot_id": 1,
	"timeslot_date": "2024-01-11",
	"next_timeslot_id": 2,
	"next_timeslot_date": "2024-01-11",
	"date": "2024-01-11",
	"current_time": "11:30:00",
	"want_to_book": 1
}
```

**Response Body**

```json
{
	"status": 200,
	"message": "SUCCESS"
}
```

**Other Messages that this API can return:**

- **DRIVER_ID_NOT_FOUND**
  - When the user's driver id is not found.
- **EV_CHARGER_ID_NOT_FOUND**
  - When EV charger's id is not found.
- **TIMESLOT_ID_NOT_FOUND**
  - When timeslot's id is not found.
- **CHARGER_IS_OFFLINE**
  - When charger's status is offline.
- **INSUFFICIENT_BALANCE**
  - When the RFID balance or user/driver is less than the required minimum RFID balance of the system.
- **IN_USE**
  - When the EV charger's status is charging.
- **DRIVER_CHARGING_ALREADY**
  - When driver is already charging.
- **DRIVER_ALREADY_BOOKED**
  - When driver have an existing reservation.
- **TIMESLOT_ALREADY_BOOKED**
  - When driver's chosen timeslot is already reserved.
- **DO_YOU_WANT_TO_BOOK_THE_NEXT_TIMESLOT**
  - When the system want's a confirmation from the user if the time is less than one (1) minute.
- **ARE_YOU_SURE_YOU_WANT_TO_BOOK_THIS_SLOT**
  - When the system want's a confirmation from the user if the user still wants to book the timeslot.

[Back to the top](#parkncharge-apis)

### PATCH /api/v1/slots/cancel

> **NOTE:** This API can be used only when the user is logged in.

> **NOTE:** The timeslot can only be cancelled when the status is ACTIVE.

**Authorization: Bearer ACCESS_TOKEN**

**Request Body**

- **reservation_id**
  - Reservation ID.
- **evc_id**
  - ID of the EV charger which the timeslot associated with.
- **timeslot_id**
  - ID of the timeslot to be cancelled. ([See Timeslot API](#timeslots))

**Response Body**

```json
{
	"status": 200,
	"data": {
		"STATUS": "SUCCESS"
	}
}
```

[Back to the top](#parkncharge-apis)

### GET /api/v1/slots/reservations

> **NOTE:** This API can be used only when the user is logged in.

**Description**

Returns list of reservations of the user.

**Authorization: Bearer ACCESS_TOKEN**

**Response Body**

```json
{
	"status": 200,
	"data": [...] // List of reservations
}
```

[Back to the top](#parkncharge-apis)

### GET /api/v1/slots/check-reservation/:evc_id/:timeslot_id

**Description**

Check if the selected timeslot of the user is his/her own reservation (when status is 'RESERVED').

**Authorization: Bearer ACCESS_TOKEN**

**Request Parameters**

- **evc_id**
  - EV Charger ID.
- **timeslot_id**
  - Selected timeslot ID.

**Response**

```json
{
	"status": 200,
	"message": "OWNED_RESERVATION" // List of reservations
}
```

**Response Status Messages**

- **OWNED_RESERVATION**
  - When the reservation is owned by the user.
- **NOT_OWNED_RESERVATION**

  - When the reservation is not owned by the user.

[Back to the top](#parkncharge-apis)

### PUT /api/v1/slots/cancel-expired-reservations

**Description**

Cancel all of the expired reservations. The reservation will be set as expired when the grace_period is less than the current time.

**Authorization: Basic BASIC_TOKEN**

**Request Body**

- **datetime**
  - Current date and time. Valid format: YYYY-MM-DD HH:MM:SS
  - The time to be passed is in 24-hour format.

**Response**

```json
{
	"status": 200,
	"result": {
		"STATUS": "SUCCESS",
		"expired_reservations": 2
	}
}
```

### POST /api/v1/charge_now

**Description**

Gives the user the ability to initiate charging without having to book or reserve a timeslot.

**Authorization: Bearer ACCESS_TOKEN**

**Request Body**

- **current_time** - current time of the user.
- **current_date** - current date of the user.
- **location_id** - ID of the location associated with an EVSE.
- **evse_uid** - UID of the EVSE
- **type** - This consists of two commands: inquire, and activate. For inquire, this will check the status of the charger, RFID balance, and timeslot status. On the other hand, activate, will activate the charger so that the user can plug the connector.
- **lat** - current location latitude of the user.
- **lng** - current location longitude of the user.

**Example Request with type "inquire"**

```json
{
	"current_time": "20:40:01", // current time of user
	"current_date": "2024-02-14", // current date of user
	"location_id": 2,
	"evse_uid": "3b505713-2902-48de-80db-7b0fad55d979", // Need to check the evse_uid
	"type": "inquire",
	"lat": 14.1555,
	"lng": 121.1555
}
```

**Example Request with type "activate"**

```json
{
	"current_time": "20:40:01", // current time of user
	"current_date": "2024-02-14", // current date of user
	"location_id": 2,
	"evse_uid": "3b505713-2902-48de-80db-7b0fad55d979", // Need to check the evse_uid
	"type": "activate",
	"lat": 14.1555,
	"lng": 121.1555
}
```

> When type is "activate", it will set a reservation, and set the status as VIRTUAL_ACTIVE

**Response Body**

```json
{
	"status": 200,
	"data": {
		"status": "AVAILABLE",
		"remarks": "CHARGER_AVAILABLE",
		"time_remaining": "02:40:01"
	}
}
```

**Other possible values of Remarks for Inquire**

- **OUTSIDE_OF_LOCATION_AREA** - This remark indicates that the user is not in the required vicinity to enable activation of charging.
- **CHARGER_OFFLINE** - Charger is offline.
- **INSUFFICIENT_BALANCE** - Insufficient RFID balance.
- **TIMESLOT_OFFLINE** - Timeslot is offline.
- **TIMESLOT_RESERVED** - Timeslot is reserved.
- **CHARGER_AVAILABLE** - Charger is available and can be activated.

**Other possible values of Remarks for Activate**

- **USER_ALREADY_HAVE_EXISTING_CHARGING_SESSION** - Indicates that the user has existing charging session.
- **CURRENT_TIMESLOT_IS_NOT_AVAILABLE** - Current timeslot for charger activation is not available.
- **USER_ALREADY_HAVE_EXISTING_RESERVATION** - Indicates that the user has existing reservation.

[Back to the top](#parkncharge-apis)

### POST /api/v1/slots/reservations/activate/:reservation_id

**Description**

This API activates user reservation for charging.

**Authorization: BEARER_TOKEN**

**Parameters**

- reservation_id

**Response**

- USER_ALREADY_HAVE_EXISTING_CHARGING_SESSION
- RESERVATION_NOT_FOUND
- SUCCESS

[Back to the top](#parkncharge-apis)

### POST /api/v1/check_current_time_and_date

**Description**

This API checks if the user current time and date is valid to activate the charger specific timeslot.

**Authorization: Bearer BASIC_TOKEN**

**Request Body**

- **timeslot_id** - Selected timeslot ID.
- **current_time** - Current time of user.
- **current_date** - Current date of user.
- **timeslot_date** - Selected timeslot date.

**Response**

- **VALID_TO_ACTIVATE**
- **INVALID_TO_ACTIVATE**

**Example**

Requesty Body

```json
{
	"timeslot_id": 1,
	"current_time": "05:53:00",
	"current_date": "2024-02-29",
	"timeslot_date": "2024-02-29"
}
```

Response

```json
{
	"status": 200,
	"result": "INVALID_TO_ACTIVATE"
}
```

The result is INVALID_TO_ACTIVATE because the current time is outside of the range of 6 am to 2 pm.

[Back to the top](#parkncharge-apis)

### Reservation and ChargeNow Constraints

#### ChargeNow

1. NOT ALLOWED to CHARGE NOW if location of user is not valid.
2. NOT ALLOWED to CHARGE NOW if evse uid does not exists.
3. NOT ALLOWED to CHARGE NOW if charger is offline.
4. NOT ALLOWED to CHARGE NOW if user has insufficient balance.
5. NOT ALLOWED to CHARGE NOW if timeslot is offline.
6. NOT ALLOWED to CHARGE NOW if timeslot is reserved.
7. NOT ALLOWED to CHARGE NOW if timeslot is charging.
8. Kapag ang current timeslot ay less than one (1) hour, and available ang next timeslot. Current timeslot is CHARGING, and next timeslot is RESERVED.
9. Kapag ang current timeslot ay less than one (1) hour, and HINDI AVAILABLE ang next timeslot. Current timeslot is CHARGING.

#### Reservation

1. NOT ALLOWED to RESERVE if DRIVER ID is not found.
2. NOT ALLOWED to RESERVE if evse uid is not found.
3. NOT ALLOWED to RESERVE if timeslot id is not found.
4. NOT ALLOWED to RESERVE if charger is offline
5. NOT ALLOWED to RESERVE if RFID balance of user is insufficient.
6. NOT ALLOWED to RESERVE if timeslot is IN_USE
7. NOT ALLOWED to RESERVE if driver is already charging.
8. NOT ALLOWED to RESERVE if driver has already reservation.
9. NOT ALLOWED to RESERVE if timeslot is already occupied/reserved/charging
10. IF the current time of user is greater than one (1) hour before the selected timeslot, then RESERVED that timeslot.
11. IF the selected timeslot date is ahead of the current date, then RESERVE the timeslot.
12. IF the current time of user is less than one (1) hour before the selected timeslot, AND next timeslot is available, then RESERVE the next timeslot.
13. IF the current time of user is less than one (1) hour before the selected timeslot, AND next timeslot is NOT AVAILABLE, then RESERVATION MUST BE DECLINED.
14. OTHERWISE
    1. RESERVE the selected timeslot
    2. IF the current time of user is less than one (1) hour and next timeslot is available, then RESERVE the next timeslot.

[Back to the top](#parkncharge-apis)

## Nearby Locations in GraphQL

### Reservation Base URL

`https://services-parkncharge.sysnetph.com/booking_reservation/graphql`

### Query `cpo_owners`

**Authorization:** <ACCESS_TOKEN>

**Sample Query**

```graphql
query Cpo_owners {
	cpo_owners {
		id
		user_id
		party_id
		cpo_owner_name
		contact_name
		contact_number
		contact_email
		logo
	}
}
```

[Back to the top](#parkncharge-apis)

### Query `locations`

**Authorization:** <BASIC_TOKEN>

**Arguments**

- lat: Float - Required
- lng: Float - Required

**Sample Query**

```graphql
query Locations {
	locations(lat: 14.1234, lng: 121.1234) {
		id
		publish
		name
		address
		address_lat
		address_lng
		city
		date_created
		date_modified
		distance
	}
}
```

[Back to the top](#parkncharge-apis)

### Query `location_with_favorites`

**Authorization:** <ACCESS_TOKEN>

**Arguements**

- lat: Float - Required
- lng: Float - Required

**Sample Query**

```graphql
query Location_with_favorites {
	location_with_favorites(lat: 14.1234, lng: 121.1234) {
		id
		publish
		name
		address
		address_lat
		address_lng
		city
		date_created
		date_modified
		distance
		favorite
	}
}
```

[Back to the top](#parkncharge-apis)

### Mutation `removeFromFavoriteLocation`

**Authorization:** <ACCESS_TOKEN>

**Arguments**

- cpo_location_id: Int - Required

**Sample Query**

```graphql
mutation RemoveFromFavoriteLocation {
	removeFromFavoriteLocation(cpo_location_id: 2) {
		user_id
		cpo_location_id
	}
}
```

[Back to the top](#parkncharge-apis)

### Mutation `addToFavoriteLocation`

**Authorization:** <ACCESS_TOKEN>

**Arguments**

- cpo_location_id: Int - Required

**Sample Query**

```graphql
mutation AddToFavoriteLocation {
	addToFavoriteLocation(cpo_location_id: 2) {
		user_id
		cpo_location_id
	}
}
```

[Back to the top](#parkncharge-apis)

### Query `favorte_locations`

**Authorization:** <ACCESS_TOKEN>

**Sample Query**

```graphql
query Favorite_locations {
	favorite_locations(lat: 14.1234, lng: 121.1234) {
		id
		publish
		name
		address
		address_lat
		address_lng
		city
		date_created
		date_modified
		distance
		favorite
		evses {
			uid
			evse_id
			serial_number
			meter_type
			status
			cpo_location_id
			current_ws_connection_id
			server_id
			date_created
		}
	}
}
```

[Back to the top](#parkncharge-apis)

### Query `filter_locations`

**Authorization:** <BASIC_TOKEN>

**Arguments**

- lat: Float - Required
- lng: Float - Required
- facilities: [String] - Optional
- capabilities: [String] - Optional
- payment_types: [String] - Optional
- parking_types: [String] - Optional
- parking_restrictions: [String] - Optional
- connector_types: [String] - Optional
- power_types: [String] - Optional

**Sample Query**

```graphql
query Filter_locations {
	filter_locations(lat: 14.1234, lng: 121.1234, facilities: ["BANKS/ATM"]) {
		id
		publish
		name
		address
		address_lat
		address_lng
		city
		date_created
		date_modified
		distance
		facilities {
			id
			code
			description
		}
	}
}
```

[Back to the top](#parkncharge-apis)

### Query `filter_locations_with_favorites`

**Authorization:** <ACCESS_TOKEN>

**Sample Query**

```graphql
query Filter_locations_with_favorites {
	filter_locations_with_favorites(
		lat: 14.1234
		lng: 121.1234
		facilities: ["CAFE"]
	) {
		id
		publish
		name
		address
		address_lat
		address_lng
		city
		date_created
		date_modified
		distance
		favorite
	}
}
```

[Back to the top](#parkncharge-apis)

## Socket Server

### Socket URL

**`ws://192.46.227.227:4006`**

### Events

#### ON `charger-status`

This will return the current status of the charger.

**Payload**

```json
{
	"CHARGER_STATUS": {
		"connection_id": "49db5116-d931-421d-b68a-fdd875d20252",
		"ev_charger_id": 2,
		"status": "ONLINE"
	}
}
```

**Other status for charger**

- PLUGGED-IN
- CHARGING
- ONLINE
- UNPLUGGED-ONLINE

[Back to the top](#parkncharge-apis)

#### ON `charging-status`

This will return the status of charging.

**Payload**

```json
  "CHARGING_STOP_DETAILS": {
    "connection_id": "629705fe-63a5-4589-ac71-1764dbb44ae9",
    "ev_charger_id": 2,
    "transactionId": 982,
    "kwh_used": 0,
    "time_used": "00:00:37",
    "price": 0,
    "remaining_balance": 513186.22
  }
```

[Back to the top](#parkncharge-apis)

#### ON `charging-stop-details`

This will return all infomration when charging stops.

**Payload**

```json
"CHARGING_STOP_DETAILS": {
    "connection_id": "629705fe-63a5-4589-ac71-1764dbb44ae9",
    "ev_charger_id": 2,
    "transactionId": 982,
    "kwh_used": 0,
    "time_used": "00:00:37",
    "price": 0,
    "remaining_balance": 513186.22
  }
```

[Back to the top](#parkncharge-apis)
