# JnA REST API

#### Error Message
 If you encounter an error, the `result` will return `error` and there will be a `message` member
 returning the error message.
 
 
| Message              | Meaning                            | 
| -------------------- | ---------------------------------- | 
| system error         | Invalid JSON                       | 
| empty                | database returns empty record set  | 
| connection failed    | connection to database failled     | 
 
Error Code Example :

```
{
    "result": "error",
    "message": "system error"
}
```

## RPC Methods

- [jnalogin](#jnalogin)
- [jnajoin](#jnajoin)
- [jnajoinmessage](#jnajoinmessage)
- [jnahome](#jnahome)
- [jnavotestate](#jnavotestate)

### jnalogin

#### rpc

http://211.54.245.8:8080/jnalogin

#### Parameters (Body)

| #    | Type                               | Description                                                  |
| ---- | ---------------------------------- | ------------------------------------------------------------ |
| 1    | {[`aname`](`string`)}                  | user id (address)                                |
| 2    | {[`apwd`](`string`)} | user password |

Raw Body Example
```
{
"aname" : "t080b15d896c896dc721714992da1f3205abb3aa20",
"apwd" : "acm",
}
```

#### Returns

- {[`result`](#result)} - value is `success` when data is returned
- {[`id`](#id)} - unique id of user
- {[`address`](#address)} - unique address of user
- {[`telegram`](#telegram)} - telegram username of user
- {[`autovote`](#autovote)} - value returned is `YES` or `NO` 
- {[`kakao`](#kakao)} - kakao id of user

Result Body Example
```
{
    "result": "success",
    "id": "2171",
    "address": "t080b15d896c896dc721714992da1f3205abb3aa20",
    "telegram": "아츄",
    "autovote": "YES",
    "kakao": "chavo"
}
```

### jnajoin

#### rpc

http://211.54.245.8:8080/jnajoin

#### Parameters (Body)

| #    | Type                               | Description                                                  |
| ---- | ---------------------------------- | ------------------------------------------------------------ |
| 1    | {[`address`](`string`)}                  | user id (address)                                |
| 2    | {[`telegram`](`string`)} | Telegram |
| 3    | {[`kakao`](`string`)} | Kakao Talk ID |
| 4    | {[`pwd`](`string`)} | Login Password |

Raw Body Example
```
{
    "address": "t00055fCEC80054f53FE76Fe026149799Cd614906A",
    "telegram": "티그리스",
    "kakao": "tigris",
    "pwd": "tigris"
}
```

#### Returns

- {[`result`](#result)} - value is `success` when data is returned
- {[`address`](#id)} - unique address of user
- {[`balance`](#address)} - current balance of user
- {[`telegram`](#telegram)} - telegram username of user
- {[`kakao`](#kakao)} - kakao id of user
- {[`exception`](#autovote)} - exception message if exception occurred 

Result Body Example

If user is successfully registered, result will show as below :
```
{
    "result": "success",
    "address": "t00055fCEC80054f53FE76Fe026149799Cd614906A",
    "balance": "3,468,206",
    "telegram": "티그리스",
    "kakao": "tigris",
    "exception": ""
}
```

If user already exist, result will show as below :
```
{
    "result": "error",
    "message": "user already exist"
}
```

If address is invalid, result will show as below :
```
{
    "result": "error",
    "message": "invalid address format"
}
```

### jnajoinmessage

#### rpc

http://211.54.245.8:8080/jnajoinmessage

#### Parameters (Body)

none

#### Returns

- {[`message`](#message)} - returns text

Result Body Example
```
{
   "message":"Line 1\n Line 2\n Line 3"
}
```

### jnahome

#### rpc

http://211.54.245.8:8080/jnahome

#### Parameters (Body)

| #    | Type                               | Description                                                  |
| ---- | ---------------------------------- | ------------------------------------------------------------ |
| 1    | {[`address`](`string`)}                  | user id (address - lenghth = 42)                                |

Raw Body Example
```
{
"address" : "t0bb44599fd077db0e7b38e7fd19a6299454181269"
}
```

#### Returns

- {[`result`](#result)} - value is `success` when data is returned
- {[`ttc`](#ttc)} - curreent user's TTC balance
- {[`yesterday`](#yesterday)} - previous day rewards
- {[`yesterday_rate`](#yesterday_rate)} - previous day reward rate
- {[`month`](#month)} - current month reward 
- {[`month_rate`](#month_rate)} - current month reward rate
- {[`total`](#total)} - total reward
- {[`total_rate`](#total_rate)} - total reward rate
- {[`vote_status`](#vote_status)} - current vote status of user, value returned is `YES` or `NO`
- {[`hour_gain`](#hour_gain)} - previous hour voting reward
- {[`hour_rate`](#hour_rate)} - previous hour voting reward rate
- {[`day_gain`](#day_gain)} - previous 24 hour reward
- {[`day_rate`](#day_rate)} - previous 24 hour reward rate

Result Body Example
```
{
    "result": "success",
    "ttc": "84,781",
    "yesterday": "+42",
    "yesterday_rate": "+.0495%",
    "month": "+980%",
    "month_rate": "+1.1559%",
    "total": "+4,340",
    "total_rate": "+5.1185%",
    "vote_status": "YES",
    "hour_gain": "2.071",
    "hour_rate": "+0.0024%",
    "day_gain": "103.981",
    "day_rate": "+0.1226%"
}
``` 

### jnavotestate

#### rpc

http://211.54.245.8:8080/jnavotestate

#### Parameters (Body)

| #    | Type                               | Description                                                  |
| ---- | ---------------------------------- | ------------------------------------------------------------ |
| 1    | {[`address`](`string`)}                  | user id (address - lenght = 42)                                |
| 2    | {[`vote_status`](`string`)} | Vote Status (Value is Either `YES` or `No`) |

Raw Body Example
```
{
    "address": "t080b15d896c896dc721714992da1f3205abb3aa20",
    "vote_status": "YES"
}
```

#### Returns

- {[`result`](#result)} - value is `success` when data is returned
- {[`vote_status`](#vote_status)} - returns updated vote status - Value is Either `YES` or `No`
- {[`pk_status`](#pk_status)} - Value is Either `YES` or `No`, `YES` if user agress to Use Private key
- {[`message`](#message)} - other

Result Body Example

If user is successfully changes vote state, result will show as below :
```
{
    "result": "sucess",
    "vote_status": "YES",
    "pk_status": "YES",
    "message": ""
}
```

If user didn't agree to use Private Key, result will show as below :
```
{
    "result": "sucess",
    "vote_status": "NO",
    "pk_status": "NO",
    "message": ""
}
```

If vote_status is invalid, result will show as below :
```
{
    "result": "error",
    "message": "invalid status format"
}
```


