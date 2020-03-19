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

- {[`message`](#message)} - returns texte

Result Body Example
```
{
   "message":"Line 1\n Line 2\n Line 3"
}
```
 


