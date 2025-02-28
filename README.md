
# My-TRAC Data Model

## Data Types

| Type name | Description | MY-SQL type (Minimum version 5.7) |
| --------- | ----------- | ----------- |
| boolean | A boolean | TINYINT |
| int | 32-bit integer | INT |
| long | 64-bit integer | BIGINT |
| float | 32-bit floating point number | FLOAT |
| double | 64-bit floating point number | DOUBLE |
| string | variable length string | VARCHAR(256) |
| timestamp | string with format YYYY-MM-DD hh:mm:ss | TIMESTAMP(3) |
| time | string with format "hh:mm:ss" | TIME(3) | 
| date | int with the form YYYYMMDD. Example 20180130 | INT | 
| enum | int representing an enumeration. Example 0 for bus, 1 for railway, etc. | INT |
| json | string representing a JSON | JSON |

__For those conditionally required fields, please look at the official GTFS specification: https://gtfs.org/reference/static/__

## Data Items

These represent the different items in the My-Trac data model. There is a one-to-one mapping between items and tables, and these can be synchronized by individual components' My-SQLs.

### activity

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | MyTrac Activity Crawler |
| mytrac_is_valid | boolean | yes | MyTrac Activity Crawler |
| mytrac_last_modified | timestamp | yes | MyTrac Activity Crawler |
| activity_creation_date | timestamp | yes | MyTrac Activity Crawler | 
| activity_id | string | yes | crawled |
| activity_name | string | yes | crawled |
| activity_lat | double | yes | crawled |
| activity_lon | double | yes | crawled |
| activity_type | enum | yes | crawled |
| activity_start | timestamp | yes | crawled |
| activity_end | timestamp | yes | crawled |
| activity_timezone | string | yes | crawled |


activity_type enum can have the following values:
* 0: work/out-of-office
* 1: education
* 2: health
* 3: service
* 4: religion
* 5: history/culture
* 6: hobby
* 7: eating & drinking
* 8: shopping

### agency (Operator)

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| agency_id | string | yes | operators platform/gtfs |
| agency_name | string | yes | operators platform/gtfs |
| agency_url | string | yes | operators platform/gtfs |
| agency_timezone | string | yes | operators platform/gtfs |
| agency_lang | string | no | operators platform/gtfs |
| agency_phone | string | no | operators platform/gtfs |
| agency_fare_url| string | no | operators platform/gtfs |

### calendar_date

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| service_id | string | yes | operators platform/gtfs |
| date | date | yes | operators platform/gtfs |
| exception_type| enum | yes | operators platform/gtfs |

### calendar

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| service_id | string | yes | operators platform/gtfs |
| monday | int | yes | operators platform/gtfs |
| tuesday | int | yes | operators platform/gtfs |
| wednesday | int | yes | operators platform/gtfs |
| thursday | int | yes | operators platform/gtfs |
| friday | int | yes | operators platform/gtfs |
| saturday | int | yes | operators platform/gtfs |
| sunday | int | yes | operators platform/gtfs |
| start_date | date | yes | operators platform/gtfs |
| end_date | date | yes | operators platform/gtfs |


### facility

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| facility_id | string | yes | My-TRAC |
| facility_name | string | yes | crawled |
| facility_lat | double | yes | crawled |
| facility_lon | double | yes | crawled |
| facility_type | enum | yes | crawled |

### feed_info

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| feed_published_name | string | yes | operators platform/gtfs |
| feed_published_url | string | yes | operators platform/gtfs |
| feed_lang | string | yes | operators platform/gtfs |
| feed_start_date | date | no | operators platform/gtfs |
| feed_end_date | date | no | operators platform/gtfs |
| feed_version | string | no | operators platform/gtfs |
| feed_contact_email | string | no | operators platform/gtfs |
| feed_contact_url | string | no | operators platform/gtfs |

### frequency

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| trip_id | string | yes | operators platform/gtfs |
| start_time| time | yes | operators platform/gtfs |
| end_time | time | yes | operators platform/gtfs |
| headway_secs | int | yes | operators platform/gtfs |
| exact_times | enum | no | operators platform/gtfs |

### mobility_trace

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | My-Trac Companion |
| mytrac_is_valid | boolean | yes | My-Trac Companion |
| mytrac_last_modified | timestamp | yes | My-Trac Companion |
| user_id | string | yes | My-Trac Companion |
| trace_lat| double | yes | My-Trac Companion |
| trace_lon | double | yes | My-Trac Companion |
| trace_prov | string | yes | My-Trac Companion |
| trace_time | timestamp | yes | My-Trac Companion |
| trace_acc | float | no | My-Trac Companion |
| trace_alt | float | no | My-Trac Companion |
| trace_bear | float | no | My-Trac Companion |
| trace_bear_acc | float | no | My-Trac Companion |
| trace_speed | float | no | My-Trac Companion |
| trace_speed_acc | float | no | My-Trac Companion |
| trace_vert_acc | float | no | My-Trac Companion |


### poi

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | My-TRAC |
| mytrac_is_valid | boolean | yes | My-TRAC |
| mytrac_last_modified | timestamp | yes | My-TRAC |
| poi_id | string | yes | My-TRAC |
| poi_type | enum | yes | crawled |
| poi_name | string | yes | crawled |
| poi_lat | double | yes | crawled |
| poi_lon | double | yes | crawled |
| poi_amenity | string | yes | crawled |

poi_type enum can have the following values:
* 0: work/out-of-office
* 1: education
* 2: health
* 3: service
* 4: religion
* 5: history/culture
* 6: hobby
* 7: eating & drinking
* 8: shopping

### route

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| route_id | string | yes | operators platform/gtfs |
| agency_id | string | yes | operators platform/gtfs |
| route_short_name | string | conditional | operators platform/gtfs |
| route_long_name | string | conditional | operators platform/gtfs |
| route_desc | string | no | operators platform/gtfs |
| route_type | enum | no | operators platform/gtfs |
| route_type | enum | yes | operators platform/gtfs |
| route_url | string | no | operators platform/gtfs |
| route_color | string | no | operators platform/gtfs |
| route_text_color | string | no | operators platform/gtfs |
| route_sort_order | string | no | operators platform/gtfs |

### shape

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| shape_id | string | yes | operators platform/gtfs |
| shape_pt_lat | double | yes | operators platform/gtfs |
| shape_pt_lon | double | yes | operators platform/gtfs |
| shape_pt_sequence | int | yes | operators platform/gtfs |
| shape_pt_sequence | int | yes | operators platform/gtfs |
| shape_dist_traveled | float | no | operators platform/gtfs |

### stop_time

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| trip_id | string | yes | operators platform/gtfs |
| arrival_time | time | conditional | operators platform/gtfs |
| departure_time | time | conditional | operators platform/gtfs |
| stop_id | string | yes | operators platform/gtfs |
| stop_sequence | int | yes | operators platform/gtfs |
| stop_headsign | string | no | operators platform/gtfs |
| pickup_type | enum | no | operators platform/gtfs |
| drop_off_type | enum | no | operators platform/gtfs |
| shape_dist_traveled | float | no | operators platform/gtfs |
| time_point | enum | no | operators platform/gtfs |

### stop

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| stop_id | string | yes | operators platform/gtfs |
| stop_code | string | no | operators platform/gtfs |
| stop_name | string | conditional | operators platform/gtfs |
| stop_desc | string | no | operators platform/gtfs |
| stop_lat | double | conditional | operators platform/gtfs |
| stop_lon | double | conditional | operators platform/gtfs |
| zone_id | string | conditional | operators platform/gtfs |
| stop_url | string | no | operators platform/gtfs |
| location_type | enum | no | operators platform/gtfs |
| parent_station | string | conditional | operators platform/gtfs |
| stop_timezone | string | no | operators platform/gtfs |
| wheelchair_boarding | string | no | operators platform/gtfs |
| level_id | string | no | operators platform/gtfs |

### transfer

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| from_stop_id | string | yes | operators platform/gtfs |
| to_stop_id | string | yes | operators platform/gtfs |
| transfer_type | enum | yes | operators platform/gtfs |
| min_transfer_time | int | no | operators platform/gtfs |

### trip

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | operators platform |
| mytrac_is_valid | boolean | yes | operators platform |
| mytrac_last_modified | timestamp | yes | operators platform |
| route_id | string | yes | operators platform/gtfs |
| service_id | string | yes | operators platform/gtfs |
| trip_id | string | yes | operators platform/gtfs |
| trip_headsign | string | no | operators platform/gtfs |
| trip_short_name | string | no | operators platform/gtfs |
| direction_id | int | no | operators platform/gtfs |
| block_id | int | no | operators platform/gtfs |
| shape_id | string | no | operators platform/gtfs |
| wheelchair_accessible | int | no | operators platform/gtfs |
| bikes_allowed | int | no | operators platform/gtfs |

### user

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | MyTrac-Companion  |
| mytrac_is_valid | boolean | yes | MyTrac-Companion  |
| mytrac_last_modified | timestamp | yes | MyTrac-Companion  |
| user_id | string | yes | MyTrac-Companion |
| user_registration_date | timestamp | yes | MyTrac-Companion |
| user_birthday | date | yes | MyTrac-Companion |
| user_gender | enum | yes | MyTrac-Companion |
| user_country | string | yes | MyTrac-Companion |
| user_nationality | string | yes | MyTrac-Companion |
| user_occupation | enum | yes | MyTrac-Companion |
| user_reliability | enum | yes | MyTrac-Companion |
| user_imp_arr | enum | yes | MyTrac-Companion |
| user_tolerance | enum | yes | MyTrac-Companion |
| user_income | enum | yes | MyTrac-Companion |
| user_marital_status | enum | yes | MyTrac-Companion |
| user_tweets | int | yes | MyTrac-Companion |
| user_traveller_type | enum | yes | MyTrac-Companion |
| user_working_hours | int | yes | MyTrac-Companion |
| user_household | int | yes | MyTrac-Companion |
| user_car_avail | boolean | yes | MyTrac-Companion |
| user_moto_avail | boolean | yes | MyTrac-Companion |
| user_bike_avail | boolean | yes | MyTrac-Companion |
| user_interest_work | float | yes | MyTrac-Companion |
| user_interest_education | float | yes | MyTrac-Companion |
| user_interest_health | float | yes | MyTrac-Companion |
| user_interest_service | float | yes | MyTrac-Companion |
| user_interest_religion | float | yes | MyTrac-Companion |
| user_interest_history | float | yes | MyTrac-Companion |
| user_interest_hobby | float | yes | MyTrac-Companion |
| user_interest_eating | float | yes | MyTrac-Companion |
| user_interest_shopping | float | yes | MyTrac-Companion |


user_gender enum can have the following values:
* 0: male
* 1: female
* 2: other

user_occupation enum can have the following values:
* 1:Private employee
* 2:Public servant
* 3:Self-employed
* 4:Student
* 5:Retired
* 6:Unemployed

user_tolerance enum can have the following values:
* 1:Not tolerant at all
* 2:Intolerant
* 3:Neutral
* 4:Tolerant
* 5:Very tolerant

user_reliability enum can have the following values:
* 1:Not reliable at all
* 2:Unreliable
* 3:Neutral
* 4:Reliable
* 5:Extremely reliable

user_imp_arr enum can have the following values:
* 1:Not important at all
* 2:Somewhat important
* 3:Very important

user_income enum can have the following values:
* 1:Low
* 2:Medium
* 3:High

user_marital_status enum can have the following values:
* 0: single
* 1: married

** User working hours need to be clarified **
** User traveller type enum need to be defined **

### user_chooses_route

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | MyTrac-Companion  |
| mytrac_is_valid | boolean | yes | MyTrac-Companion  |
| mytrac_last_modified | timestamp | yes | MyTrac-Companion  |
| user_id | string | yes | MyTrac-Companion |
| group_id| string | no | MyTrac-Companion |
| from_name | string | yes | MyTrac-Companion |
| from_address | string | yes | MyTrac-Companion |
| from_lon | double | yes | MyTrac-Companion |
| from_lat | double | yes | MyTrac-Companion |
| to_name | string | yes | MyTrac-Companion |
| to_lon | double | yes | MyTrac-Companion |
| to_lat | double | yes | MyTrac-Companion |
| to_address | string | yes | MyTrac-Companion |
| time | timestamp | yes | MyTrac-Companion | 
| mode | enum | no |  MyTrac-Companion |
| max_walk_distance | int | no |  MyTrac-Companion |
| num_itineraries | int | no | MyTrac-Companion |
| max_transfers | int | no | MyTrac-Companion |
| user_choice | int | yes | MyTrac-Companion |
| request_reply | json | yes | MyTrac-Companion |

mode can have the following values:
* 0: airplane
* 1: bus
* 2: rail
* 3: bicycle
* 4: subway
* 5: tram
* 6: car
* 7: transit
* 8: walk


### user_evaluates_activity

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | MyTrac-Companion  |
| mytrac_is_valid | boolean | yes | MyTrac-Companion  |
| mytrac_last_modified | timestamp | yes | MyTrac-Companion  |
| user_id | string | yes | MyTrac-Companion |
| activity_id | string | yes | MyTrac-Companion |
| rating | int | yes | MyTrac-Companion |
| time | timestamp | yes | MyTrac-Companion |

### user_joins_group

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | MyTrac-Companion  |
| mytrac_is_valid | boolean | yes | MyTrac-Companion  |
| mytrac_last_modified | timestamp | yes | MyTrac-Companion  |
| user_id | string | yes | MyTrac-Companion |
| group_id | string | yes | MyTrac-Companion |
| time | timestamp | yes | MyTrac-Companion |

### user_purchases_ticket

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | MyTrac-Companion  |
| mytrac_is_valid | boolean | yes | MyTrac-Companion  |
| mytrac_last_modified | timestamp | yes | MyTrac-Companion  |
| user_id | string | yes | MyTrac-Companion |
| tickets_purchased | int | yes | MyTrac-Companion |
| time | timestamp | yes | MyTrac-Companion |

### user_uses_app

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | MyTrac-Companion  |
| mytrac_is_valid | boolean | yes | MyTrac-Companion  |
| mytrac_last_modified | timestamp | yes | MyTrac-Companion  |
| user_id | string | yes | MyTrac-Companion |
| time | timestamp | yes | MyTrac-Companion |

### user_views_activity

| Field Name | Field Type | Required | Source |
| ---------- | ---------- | -------- | ------ |
| mytrac_id | long | yes | MyTrac-Companion  |
| mytrac_is_valid | boolean | yes | MyTrac-Companion  |
| mytrac_last_modified | timestamp | yes | MyTrac-Companion  |
| user_id | string | yes | MyTrac-Companion |
| activity_id | string | yes | MyTrac-Companion |
| time | timestamp | yes | MyTrac-Companion |

