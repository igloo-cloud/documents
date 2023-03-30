# Philippine pet insurance API(`DRAFT` 0.0.1)

## Send a verification code to an email

#### Request
| Name  | Type | Required | Description |
| ------------- | ------------- | ------------- | ------------- |
| email  | string  | true | Email address to be verified  |

#### Response
| Name  | Type | Description |
| ------------- | ------------- | ------------- |
| message  | string  | Error message, an empty string will be returned if there is no error |
| code  | string  | Error code, an empty string will be returned if there is no error  |

```
POST https://api.qa.iglooinsure.com/v1/agency-platform-ph/agency/public/email_verification/send_code
```

#### Sample
```json
{
    "email": "example@iglooinsure.com",
}
```

## Sign up an Agent
#### Request
| Name  | Type | Required | Description |
| ------------- | ------------- | ------------- | ------------- |
| email  | string  | true | Email address  |
| verification_code  | true | string  | Verification code of email address  |
| given_names  | string  | false | Given names  |
| last_name  | string  | false | Last name  |
| first_name  | string  | false | First name  |
| password  | string  | true | Password  |
| phone.area_code  | string  | true | Area code of phone, eg: 63  |
| phone.number  | string  | true | Number of phone  |
| date_of_birth  | string  | false | yyyy-MM-dd  |


#### Response
| Name  | Type | Description |
| ------------- | ------------- | ------------- |
| message  | string  | Error message, an empty string will be returned if there is no error |
| code  | string  | Error code, an empty string will be returned if there is no error  |

```
POST https://api.qa.iglooinsure.com/v1/agency-platform-ph/public/agent/sign-up
```
```json
{
    "email": "example@iglooinsure.com",
    "verification_code": "111111",
    "given_names": "Igloo",
    "last_name": "Great",
    "phone": {
        "area_code": "63",
        "number": "123443211221"
    },
    "password": "p@ssword01",
    "date_of_birth": "2000-01-01"
}
```

### Sign in an Agent
#### Request
| Name  | Type | Required | Description |
| ------------- | ------------- | ------------- | ------------- |
| password  | string  | true | Password  |
| phone.area_code  | string  | true | Area code of phone, eg: +63  |
| phone.number  | string  | true | Number of phone  |

#### Response
| Name  | Type | Description |
| ------------- | ------------- | ------------- |
| message  | string  | Error message, an empty string will be returned if there is no error |
| code  | string  | Error code, an empty string will be returned if there is no error  |
| user_token  | string  | Token of agent  |

```
POST https://api.qa.iglooinsure.com/v1/agency-platform-ph/public/agent/sign-in
```

### Request
```json
{
    "phone": {
        "area_code": "+63",
        "number": "123443211221"
    },
    "password": "p@ssword01"
}
```

### Response
```json
{
    "user_token":"eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Imdpaml2aTg3NjRAbHViZGUuY29tIiwiZXhwIjoxNjgwMjU1OTg4LCJwaG9uZV9hcmVhX2NvZGUiOiI2MyIsInBob25lX251bWJlciI6IjE2NDg4OTg2NTY0IiwidWlkIjo0MDkwfQ.XqAtSKlMkpI5oU3qVEImYgjbGGucTaUV5LT8XOmfg1R3p0iLRniD7zq5JN279g0_BTsqX7Q2H98PAhYAlC1NKA"
}
```

### Get plans of a pet insurance

### Auth
add token in http header
```
X-Axinan-Authorization:Bearer {TOKEN}
```
#### Response
| Name  | Type | Description |
| ------------- | ------------- | ------------- |
| message  | string  | Error message, an empty string will be returned if there is no error |
| code  | string  | Error code, an empty string will be returned if there is no error  |
| plans  | [Plan]  | Plans, it's an array  |

#### Response.Plan
| Name  | Type | Description |
| ------------- | ------------- | ------------- |
| name  | string  | Error message, an empty string will be returned if there is no error |
| product_key  | string  | Product key  |
| plan_key  | [Plan]  | Plan key  |


```
GET https://api.qa.iglooinsure.com/v1/agency-platform-ph/agency/pet/plans
```
### Response
```json
{
    "plans": [
        {
            "name": "Pet Insurace (Dogs）- 1 Month",
            "plan_key": "3778e0b6-ca0b-42ac-9901-146c90ce2a01",
            "product_key": "b29579f5-50c9-4901-978d-a2d94e1e727e"
        },
        {
            "name": "Pet Insurace (Dogs）- 3 Months",
            "product_key": "b29579f5-50c9-4901-978d-a2d94e1e727e",
            "plan_key": "7cdd9526-dea7-4260-b9ab-0a73d2c54889"
        },
        {
            "name": "Pet Insurace (Dogs）- 1 Year",
            "product_key": "b29579f5-50c9-4901-978d-a2d94e1e727e",
            "plan_key": "116e62d8-6bac-4521-a093-5019f630f631"
        }
    ]
}
```

### Fast quote
### Auth
add token in http header
```
X-Axinan-Authorization:Bearer {TOKEN}
```

#### Request
| Name  | Type | Required | Description |
| ------------- | ------------- | ------------- | ------------- |
| fast_quote  | Object  | true | Pet's information |

#### Pet
| Name  | Type | Required | Description |
| ------------- | ------------- | ------------- | ------------- |
| name  | string | true | Name of a pet |

#### Response
| Name  | Type | Description |
| ------------- | ------------- | ------------- |
| quotation.premium.total  | string | Total premium |
| quotation.premium.base  | string | Base premium |
| quotation.premium.add_on  | string | Premium of add on |
| quotation.premium.tax  | string | Tax |

```
POST https://api.qa.iglooinsure.com/v1/agency-platform-ph/agency/pet/{product_key}/{plan_key}/fast_quote
```

Request
```json
{
    "fast_quote": {
        "object": {
            "name": "Name of dog"
        }
    }
}
```

Response
```json
{
    "quotation": {
        "premium": {
            "total": "1260",
            "base": "903.6",
            "add_on": "0",
            "tax": "356.4"
        }
    }
}
```

### Application

### Auth
add token in http header
```
X-Axinan-Authorization:Bearer {TOKEN}
```

#### Request
| Name  | Type | Required | Description |
| ------------- | ------------- | ------------- | ------------- |
| application  | Object  | true | Application information |

#### Application
| Name  | Type | Required | Description |
| ------------- | ------------- | ------------- | ------------- |
| object  | Object | true | Pet |
| policyholder  | Object | true | Policyholder |

#### Application.object(pet)
| Name  | Type | Required | Description |
| ------------- | ------------- | ------------- | ------------- |
| name  | string | true | Name |
| date_of_birth  | uint64(unixmilli) | true | Date of birth |
| gender  | string(male,female) | true | Gender |
| breed  | string | true | Breed |
| color  | string | true | Color |
| photos  | [string] | true | photos of pet |

#### Application.policyholder
| Name  | Type | Required | Description |
| ------------- | ------------- | ------------- | ------------- |
| first_name  | string | true | First name |
| middle_name  | string | true | Middle name |
| last_name  | string | true | Last name |
| given_names  | string | true | Given names |
| date_of_birth  | uint64(unixmilli) | true | Date of birth |
| gender  | string(male,female) | true | Gender |
| id_type  | string | true | Id type, eg: `Philippine Passport`,`SSS ID or SSS UMID Card`,`GSIS ID or GSIS UMID Card`,`Driver's License`,`PRC ID` |
| id_number  | string | true | Id number |
| phone.area_code  | string | true | Area code of phone |
| phone.number  | string | true | Number phone |
| email  | string | true | Email |

#### Response
| Name  | Type | Description |
| ------------- | ------------- | ------------- |
| policy.id  | string | Policy id |
| policy.display_id  | string | Policy display id |
| policy.coi_doc  | string | coi doc file of a policy  |
| policy.coi_no  | string | coi number of a policy  |
| policy.object  | Pet | It's the information of an pet in a pet insurance |
| policy.policyholder  | Policyholder | policyholder |
| policy.premium.total  | string | Total premium |
| policy.premium.base  | string | Base premium |
| policy.premium.add_on  | string | Premium of add on |
| policy.premium.tax  | string | Tax |
| policy.state  | string | State of a policy  |
| policy.periods.policy.start_time  | string | Start time of the policy  |
| policy.periods.policy.end_time  | string | End time of the policy  |
| policy.periods.waiting.period  | string | Waiting period  |
| policy.periods.coverage.period  | string | Coverage period  |
| policy.periods.coverage.start_time  | string | Start time of the coverage  |
| policy.periods.coverage.end_time  | string | End time of the coverage  |
| policy.periods.claim.start_time  | string | Start time of the claim  |
| policy.periods.claim.end_time  | string | End time of the claim  |

Request
```json
{
    "application": {
        "object": {
            "name": "Hoo",
            "date_of_birth": 1580193991365,
            "gender": "male",
            "breed": "Ju",
            "color": "Red",
            "photos": [
                "https://api.qa.iglooinsure.com/v1/admin/fileapi/common_file/proxy/turbo/aXBzLXBoLTIwMjMtMDMtMGI0OWE5LWRvZy1wdXBweS1vbi1nYXJkZW4tcm95YWx0eS1mcmVlLWltYWdlLTE1ODY5NjYxOTEuanBlZw==?sign=turbo"
            ]
        },
        "policyholder": {
            "first_name": "Hh",
            "middle_name": "hh",
            "last_name": "hh",
            "given_names": "hh",
            "gender": "male",
            "date_of_birth": 950770010428,
            "id_type": "Philippine Passport",
            "id_number": "1",
            "phone": {
                "area_code": "+63",
                "number": "1"
            },
            "email": "jinlong.chen@iglooinsure.com"
        },
        "igloo_terms": true,
        "malayan_pravicy": true
    }
}
```

Response
```json
{
    "policy": {
        "id": "1641356955404472320",
        "display_id": "20230330IGPET3M0014",
        "coi_doc": "",
        "coi_no": "K0011641",
        "created_at": 1680164967000,
        "updated_at": 1680164968000,
        "object": {
            "name": "Hoo",
            "date_of_birth": 1580193991365,
            "gender": "male",
            "breed": "Ju",
            "color": "Red",
            "photos": [
                "https://api.qa.iglooinsure.com/v1/admin/fileapi/common_file/proxy/turbo/aXBzLXBoLTIwMjMtMDMtMGI0OWE5LWRvZy1wdXBweS1vbi1nYXJkZW4tcm95YWx0eS1mcmVlLWltYWdlLTE1ODY5NjYxOTEuanBlZw==?sign=turbo"
            ]
        },
        "policyholder": {
            "id_type": "Philippine Passport",
            "id_number": "1",
            "last_name": "hh",
            "first_name": "Hh",
            "middle_name": "hh",
            "date_of_birth": 950770010428,
            "email": "jinlong.chen@iglooinsure.com",
            "mobile_number": {
                "area_code": "+63",
                "number": "1"
            },
            "occupation": ""
        },
        "premium": {
            "total": "1260",
            "base": "903.6",
            "add_on": "0",
            "tax": "356.4"
        },
        "state": "PolicyInit",
        "periods": {
            "policy": {
                "start_time": 1680251368000,
                "end_time": 1688200168000
            },
            "waiting": {
                "period": "14d"
            },
            "coverage": {
                "period": "",
                "start_time": 0,
                "end_time": 0
            },
            "claim": {
                "start_time": 0,
                "end_time": 0
            }
        }
    }
}
```

### Get payment

### Auth
add token in http header
```
X-Axinan-Authorization:Bearer {TOKEN}
```

#### Request
| Name  | Type | Required | Description |
| ------------- | ------------- | ------------- | ------------- |
| application_id  | string  | true | The id of an application(from the response of `Application`) |

#### Response
| Name  | Type | Description |
| ------------- | ------------- | ------------- |
| payments  | [Payment] | Array of payment methods |

#### Payment
| Name  | Type |  Description |
| ------------- | ------------- | ------------- |
| transaction_id  | string | Transaction id |
| payment_url  | string | Payment URL, open this URL in a webbrowser for payment  |


```
POST https://api.qa.iglooinsure.com/v1/agency-platform-ph/agency/{application_id}/get_payments
```

Response
```json
{
    "payments": [
        {
            "transaction_id": "123",
            "payment_url": "https://payment_url"
        }
    ]
}
```
