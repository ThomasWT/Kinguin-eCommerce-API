# Orders API

Version: `v2`

## Table of Contents

- [Place order](#place-order)
- [Dispatch](#dispatch)
- [Get keys](#get-keys)
- [Key object](#key-object)

## Place order

`POST /v2/order`

### Input

Content-Type: `application/json`

```json
{
    "products": [
        {
            "productId": [string],
            "qty": [int],
            "price": [float],
            "name": [string],
            "keyType": [string],
            "offerId": [string]
        },
        (...)
    ],
    "orderExternalId": [string],
    "couponCode": [string]
}
```

Field | Type | Description
--------- | :-----: | --------
`products.productId` | string | Another product ID
`products.qty` | int | Ordered quantity (max: `100`)
`products.price` | float | Requested price
`products.name` | string | Product name
`products.keyType`* | string | [Key type](../../../features/KeyType.md)
`products.offerId`* | string | [Offer ID](../../../features/BuyOffer.md)
`orderExternalId` | string | [Order external ID](../../../features/OrderExternalId.md)
`couponCode`* | string | [Discount code](../../../features/CouponCode.md)

> *feature property, in case of use please contact your business manager

### Output

HTTP Status: `201`

Content-Type: `application/json`

Returns the [Order Object](../v1/README.md#order-object)

### Example request

```bash
curl -X POST \
     -H 'X-Api-Key: [api-key]' \
     -H 'Content-Type: application/json' \
     -d '{"products":[{"productId":"5c9b68662539a4e8f17ae2fe","qty":1,"name":"Counter-Strike: Source Steam CD Key","price":5.79"}]}' \
     https://gateway.kinguin.net/esa/api/v2/order
```

## Dispatch

`POST /v2/order/{orderId}/dispatch`

### Path parameters

Content-Type: No payload required.

Parameter | Type | Description
--------- | :-----: | -----------
`orderId` | string | Order ID

### Output

HTTP Status: `201`

Content-Type: `application/json`

```json
{
    "dispatchId": [int]
}
```

### Example request

```bash
curl -X POST \
     -H 'X-Api-Key: [api-key]' \
     -H 'Content-Type: application/json' \
     https://gateway.kinguin.net/esa/api/v2/order/PHS84FJAG5U/dispatch
```

### Example response

```json
{
    "dispatchId": 14169762
}
```



## Get keys

`GET /v2/order/{orderId}/keys`

### Path parameters

Parameter | Type | Description
--------- | :-----: | -----------
`orderId` | string | Order ID

### Output

HTTP Status: `200`

Content-Type: `application/json`

### Example request

```bash
curl -X GET \
     -H 'X-Api-Key: [api-key]' \
     https://gateway.kinguin.net/esa/api/v2/order/PHS84FJAG5U/keys
```

### Example response

```json
[
    {
        "serial": "0ddbebb2-559d-42e9-a8e1-fd4b2bdea858",
        "type": "text/plain",
        "name": "Counter-Strike: Source Steam CD Key",
        "kinguinId": 1949,
        "offerId": "5f7efd272f3a650001f42722",
        "productId": "5c9b68662539a4e8f17ae2fe"
    }
]
```

### Key Object

Field | Type | Description
--------- | ----- | --------
`name` | string | Product name
`type`| string | Serial content type. Can be `text/plain` or `image/jpeg`, `image/png` or `image/gif`
`serial` | string | Plain text serial key or in case of `image/*` base64 encoded content of the image
`kinguinId` | int | Product ID
`offerId` | string | Offer ID
`productId` | string | Another product ID
