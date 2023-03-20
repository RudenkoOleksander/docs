## Admin API
----------------------------------------------------------------
### $\color{#ba3925}{\textrm{Health Probe}}$ 

Value              | Description 
-------------------|---------------
URI                | https://rs0.hypersecureid.com/health.html
Sandbox URI        | https://rs0_sandbox.hypersecureid.com/health.html
Method             | GET 

### **Example**

```
GET /health.html
Host: rs0.hypersecureid.com
```

## Responce
 
if success status code 200 else 403

----------------------------------------------------------------
### $\color{#ba3925}{\textrm{Get user sessions}}$ 

**Request**

Value              | Description 
-------------------|---------------
URI                | https://rs0.hypersecureid.com/admin/user/sessions/get
Sandbox URI        | https://rs0_sandbox.hypersecureid.com/admin/user/sessions/get
Method             | POST     
Authorization      | Bearer AA.BB.CC     
Content-type       | application/json


**Body Json Field**
Name               | Required | Type          | Description
-------------------|----------|----------------|---------------------
request_id         | false    | int64          | Opaque value used to maintain id between the request and response.


### **Example**

```
POST /admin/user/sessions/get
Host: rs0.hypersecureid.com
Authorization: Bearer AA.BB.CC
content-Type: application/json
{
       "request_id": 42
}
```

## Responce

**Body Json Field**     

Name          | Type         | Description
--------------|---------------|---------------------
request_id    | int64         | Opaque value used to maintain id between the request and response.
result        | int           | See table below
sessions      | json_array    | 

**Result**

| Value  | Name 
| ------ | ----------------------------------- 
| 0      | success                             
| -1     | fail by token invalid               
| -2     | fail by token expired               
| -3     | fail by access denied               
| -4     | fail by service temporary not valid 
| -5     | fail by invalid parameters          

### **Example**

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=UTF-8
{
        "request_id": 42,
        "result":     0,
        "sessions":
        [
            {
                "client_id":     "id",
                "created_dt":    1679314049,
                "expiration_dt": 1679315049,
                "ip":            "xxx.xxx.xxx.xxx",
                "session_id":    "session-id"
            },
            {...}
        ]
}
```

----------------------------------------------------------------
### $\color{#ba3925}{\textrm{User sessions logout}}$ 

**Request**

Value              | Description 
-------------------|---------------
URI                | https://rs0.hypersecureid.com/admin/user/sessions/logout
Sandbox URI        | https://rs0_sandbox.hypersecureid.com/admin/user/sessions/logout
Method             | POST     
Authorization      | Bearer AA.BB.CC     
Content-type       | application/json

**Body Json Field**
Name               | Required | Type          | Description
-------------------|----------|----------------|---------------------
request_id         | false    | int64          | Opaque value used to maintain id between the request and response.
sessions_id        | true     | json_array     | 


### **Example**

```
POST /admin/user/sessions/get
Host: rs0.hypersecureid.com
Authorization: Bearer AA.BB.CC
content-Type: application/json
{
       "request_id":   42,
       "sessions_id":  ["id1", "id2", ...]
}
```

## Responce

**Body Json Field**     

Name          | Type         | Description
--------------|---------------|---------------------
request_id    | int64         | Opaque value used to maintain id between the request and response.
result        | int           | See table below

**Result**

| Value  | Name 
| ------ | ----------------------------------- 
| 0      | success                             
| -1     | fail by token invalid               
| -2     | fail by token expired               
| -3     | fail by access denied               
| -4     | fail by service temporary not valid 
| -5     | fail by invalid parameters          

### **Example**

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=UTF-8
{
        "request_id": 42,
        "result":     0
}
```

----------------------------------------------------------------
### $\color{#ba3925}{\textrm{User devices get}}$

**Request**

Value              | Description 
-------------------|---------------
URI                | https://rs0.hypersecureid.com/admin/user/devices/get
Sandbox URI        | https://rs0_sandbox.hypersecureid.com/admin/user/devices/get
Method             | POST     
Authorization      | Bearer AA.BB.CC     
Content-type       | application/json

**Body Json Field**
Name               | Required | Type          | Description
-------------------|----------|----------------|---------------------
request_id         | false    | int64          | Opaque value used to maintain id between the request and response.

### **Example**

```
POST /admin/user/sessions/get
Host: rs0.hypersecureid.com
Authorization: Bearer AA.BB.CC
content-Type: application/json
{
       "request_id": 42
}
```

## Responce

**Body Json Field**     

Name          | Type         | Description
--------------|---------------|---------------------
request_id    | int64         | Opaque value used to maintain id between the request and response.
result        | int           | See table below
devices       | json_array    | 

**Result**

| Value  | Result name                         
| ------ | ----------------------------------- 
| 0      | success                             
| -1     | fail by token invalid               
| -2     | fail by token expired               
| -3     | fail by access denied               
| -4     | fail by service temporary not valid 
| -5     | fail by invalid parameters          

### **Example**

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=UTF-8
{
        "request_id": 32,
        "result":     0,
        "devices":
        [
            {
                "created_dt":     1679314049,
                "device_desc":    JSON string,
                "device_id":      "device-id",
                "device_state":   1,
                "last_access_dt": 1679314049,
                "last_client_id": "client-id",
                "last_ip":        "xxx.xxx.xxx.xxx",
                "last_ip_location":
                {
                    "city_name":               "city-name",
                    "continent_code":          "c-code",
                    "continent_name":          "c-name",
                    "country_iso_code":        "iso-code",
                    "country_name":            "country-name",
                    "latitude":                42.42,
                    "longitude":               42.42,
                    "network":                 "network",
                    "subdivision_1_iso_code":  "value",
                    "subdivision_1_name":      "value",
                    "subdivision_2_iso_code":  "value",
                    "subdivision_2_name":      "value"
                },
                "sessions":
                [
                    {
                        "client_id":     "id",
                        "created_dt":    1679314049,
                        "expiration_dt": 1679315049,
                        "ip":            "xxx.xxx.xxx.xxx",
                        "session_id":    "session-id"
                    }
                ]
            },
            {...}
        ]
}
```

**Device State**

| Value  | Name 
| ------ | ----------------------------------- 
| 0      | waiting for approve  
| 1      | approved 
| 2      | blocked 

----------------------------------------------------------------
### $\color{#ba3925}{\textrm{User devices blocked update}}$

**Request**

Value              | Description 
-------------------|---------------
URI                | https://rs0.hypersecureid.com/admin/user/devices/is-blocked-update
Sandbox URI        | https://rs0_sandbox.hypersecureid.com/admin/user/devices/is-blocked-update
Method             | POST     
Authorization      | Bearer AA.BB.CC     
Content-type       | application/json

**Body Json Field**
Name               | Required | Type          | Description
-------------------|----------|----------------|---------------------
request_id         | false    | int64          | Opaque value used to maintain id between the request and response.
devices_id         | true     | json_array     | 
is_blocked         | true     | boole          | 

### **Example**

```
POST /admin/user/sessions/get
Host: rs0.hypersecureid.com
Authorization: Bearer AA.BB.CC
content-Type: application/json
{
       "request_id": 42
       "devices_id": ["device-id1", "device-id2", ...]
       "is_blocked": false
}
```

## Responce

**Body Json Field**

Name          | Type         | Description
--------------|---------------|---------------------
request_id    | int64         | Opaque value used to maintain id between the request and response.
result        | int           | See table below

**Result**

| Value  | Result name                         
| ------ | ----------------------------------- 
| 0      | success                             
| -1     | fail by token invalid               
| -2     | fail by token expired               
| -3     | fail by access denied               
| -4     | fail by service temporary not valid 
| -5     | fail by invalid parameters          

### **Example**

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=UTF-8
{
        "request_id": 42
        "result":     0
}
```


----------------------------------------------------------------
### $\color{#ba3925}{\textrm{Users load}}$

**Request**

Value              | Description 
-------------------|---------------
URI                | https://rs0.hypersecureid.com/admin/users/load
Sandbox URI        | https://rs0_sandbox.hypersecureid.com/admin/users/load
Method             | POST     
Authorization      | Bearer AA.BB.CC     
Content-type       | application/json

**Body Json Field**
Name               | Required | Type          | Description
-------------------|----------|----------------|---------------------
request_id         | false    | int64          | Opaque value used to maintain id between the request and response.
filter_mode        | true     | integer        | See table below
filter_value       | true     | string         | 

**Filter modes**

Value  | Mode                                |
------ | ----------------------------------- |
0      | twitter_id                          |
1      | telegram_id                         |
2      | wallet_address                      |
3      | telegram_user_name                  |
4      | twitter_user_name                   |
5      | email                               |
6      | kyc_applicant_id                    |


## Responce

**Body Json Field**

Name          | Type         | Description
--------------|---------------|---------------------
request_id    | int64         | Opaque value used to maintain id between the request and response.
result        | int           | See table below
sessions      | json_array    | 

**Result**

| Value  | Result name                         
| ------ | ----------------------------------- 
| 0      | success                             
| -1     | fail by token invalid               
| -2     | fail by token expired               
| -3     | fail by access denied               
| -4     | fail by service temporary not valid 
| -5     | fail by invalid parameters          
| -6     | fail by invalid grant          

### **Example**

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=UTF-8
{
    "request_id": 42,
    "result":     0,
    "users": 
    [
        {
            "email":                     "xxx@xx.xx",
            "user_id":                   "uid",
            "phone_number":              "xxxx",
            "twitter_id":                "twitter-id",
            "telegram_id":               "telegram-id",
            "verification_level":        4,
            "review_complete_dt":        1679314049,
            "id_country_a3":             "xxx",
            "pn_country_a3":             "xxx",
            "kyc_applicant_id":          "aaplicant-id",
            "telegram_user_name":        "telegram-user-name",
            "twitter_user_name":         "twitter-user-name",
            "wallets":
            [
                {
                    "address":
                    {
                        "chain":    "eth",
                        "address":  "0x039dfslksfh"
                    }
                    "signed":       true
                    "tags":
                    [
                        "tag1",
                        "tag2"
                    ]
                },
                {...}
            ]
            "projects":
            [
                "name":      "project-name",
                "sub_name":  "project-subname"
            ]
            "ip_countries_a3":
            [
                "aaa",
                "aaa"
            ],
        },
        {...}
    ]
}
```

**Verification level**

Value  | Level                               |
------ | ----------------------------------- |
0      | user                                |
1      | phone number                        |
2      | social                              |
3      | kyc basic                           |
4      | kyc full                            |
