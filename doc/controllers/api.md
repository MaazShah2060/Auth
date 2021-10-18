# API

```php
$aPIController = $client->getAPIController();
```

## Class Name

`APIController`

## Methods

* [Auth Login](/doc/controllers/api.md#auth-login)
* [API](/doc/controllers/api.md#api)


# Auth Login

```php
function authLogin(array $options): void
```

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `email` | `string` | Query, Required | - |
| `password` | `string` | Query, Required | - |

## Response Type

`void`

## Example Usage

```php
$collect = [];

$email = 'superadmin@email.com';
$collect['email'] = $email;

$password = 'admin123$';
$collect['password'] = $password;

$aPIController->authLogin($collect);
```


# API

```php
function aPI(string $address): void
```

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `address` | [`string (Types)`](/doc/models/types-enum.md) | Template, Required | - |

## Response Type

`void`

## Example Usage

```php
$address = Models\TypesEnum::USERPROFILE;

$aPIController->aPI($address);
```

