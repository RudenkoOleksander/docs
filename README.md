## Admin API
----------------------------------------------------------------
* #### Get user sessions

> POST /admin/user/sessions/get

> content-type
  + application/json

> Request body

| Parameters   | Schema     |
| ------------ | ---------- |
| request_id   | Integer    |
| access_token | AA.BB.CC   |

> Responce

| Parameters   | Schema     |
| ------------ | ---------- |
| request_id   | Integer    |
| result       | result     |
| sessions     | sessions   |

> Produces
  + application/json

| Result name | Value |
| ----------- | ----- |
| success                             | 0      |
| fail_by_token_invalid               | -1     |
| fail_by_token_expired               | -2     |
| fail_by_access_denied               | -3     |
| fail_by_service_temporary_not_valid | -4     |
| fail_by_invalid_parameters          | -5     |
