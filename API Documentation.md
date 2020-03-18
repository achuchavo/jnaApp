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

### jnalogin

#### rpc

http://211.54.245.8:8080/jnalogin

#### Parameters (Body)

| #    | Type                               | Description                                                  |
| ---- | ---------------------------------- | ------------------------------------------------------------ |
| 1    | {[`aname`](`string`)}                  | user id (address)                                |
| 2    | {[`apwd`](#Quantity)|`string`} | user password |

Raw Body Example
```
{
"aname" : "t080b15d896c896dc721714992da1f3205abb3aa20",
"aspwd" : "acm",
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
 


