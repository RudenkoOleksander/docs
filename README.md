## Admin API
----------------------------------------------------------------
* #### Get user sessions

> POST /admin/user/sessions/get

> **Headers**
  + content-type: application/json

> **Request body**

| Parameters   | Schema     |
| ------------ | ---------- |
| request_id   | Integer    |
| access_token | AA.BB.CC   |

> **Responce**


| Parameters   | Schema     |
| ------------ | ---------- |
| request_id   | Integer    |
| result       | Result     |
| sessions     | JSON_ARRAY |

> **Result**

| Result name | Value |
| ----------- | ----- |
| success                             | 0      |
| fail_by_token_invalid               | -1     |
| fail_by_token_expired               | -2     |
| fail_by_access_denied               | -3     |
| fail_by_service_temporary_not_valid | -4     |
| fail_by_invalid_parameters          | -5     |

> **sessions**

  [
      {
      "client_id":     string,
      "created_dt":    uint64,
      "expiration_dt": uint64,
      "ip":            string,
      "session_id":    string
      },
      {...}
  ]
