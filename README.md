## Admin API
----------------------------------------------------------------
* #### Get user sessions

> POST /admin/user/sessions/get

    content-type: application/json

 > Request body
|parameter|value type|
|---------|----------|
|request_id|integer|
|access_token|AA.BB.CC|

    responce: {
        "request_id": integer,
        "result":     integer,
        "sessions":   (JSON_ARRAY)
    }

    result: {
        fail_by_invalid_parameters,          = -5,
        fail_by_service_temporary_not_valid, = -4,
        fail_by_access_denied,               = -3,
        fail_by_token_expired,               = -2,
        fail_by_token_invalid,               = -1,
        success,                             = 0
    }

    "sessions": [
                  {
                    "client_id":     string,
                    "created_dt":    uint64,
                    "expiration_dt": uint64,
                    "ip":            string,
                    "session_id":    string
                  },
                  {...}
                ]

----------------------------------------------------------------
* #### User sessions logout

> POST /admin/user/sessions/logout

    content-type: application/json

    body: {
        "request_id":   integer,
        "access_token": AA.BB.CC,
        "sessions_id":  [JSON_ARRAY]
    }

    responce: {
        "request_id": integer,
        "result":     integer
    }

    result: {
        fail_by_invalid_parameters,          = -5,
        fail_by_service_temporary_not_valid, = -4,
        fail_by_access_denied,               = -3,
        fail_by_token_expired,               = -2,
        fail_by_token_invalid,               = -1,
        success,                             = 0
    }

----------------------------------------------------------------
