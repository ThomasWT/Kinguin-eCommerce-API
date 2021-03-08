# Webhooks

* [Product updated webhook](#product-updated-webhook)
* [Order completed webhook](#order-completed-webhook)
* [Order status changed webhook](#order-status-changed-webhook)

# Headers

Each webhook contains a set of predefined headers:

Header name | Header value
--------- | ---------
`X-Event-Name` | Webhook event name
`X-Event-Secret` | Your secret key


## Product updated webhook

The webhook is triggered when product was changed, or when new offer became available.

At least one of the bellowed product/offer fields should be changed to trigger a webhook:

Field |
--------- |
`qty` |
`textQty` |
`totalQty` |
`offersCount` |
`price` |
`status` |
`releaseDate` |
`merchantName` |

### Example payload

Content-Type: `aplication/json`

`X-Event-Name` header: `product.update`

Request method: `POST`

```json
{
   "kinguinId": 1949,
   "productId": "5c9b5f6b2539a4e8f172916a",
   "updatedAt": "2020-10-16T11:24:08+00:00"
}
```

Field | Type | Description
--------- | :-----: | -----------
`kinguinId` | int | Product ID
`productId` | string | Another product ID
`updatedAt` | string | Date of change in format `Y-m-d\TH:i:sP`


## Order completed webhook

The webhook is triggered when order was dispatched and its status was changed to `completed`. Purchased keys are ready to download.

### Example payload

Content-Type: `aplication/json`

`X-Event-Name` header: `order.complete`

Request method: `POST`

```json
{
   "orderId": "PHS84FJAG5U",
   "orderExternalId": "AL2FEEHOO2OHF",
   "updatedAt": "2020-10-16T11:24:08+00:00"
}
```

Field | Type | Description
--------- | :-----: | -----------
`orderId` | string | Order ID
`orderExternalId` | string | Order external ID
`updatedAt` | string | Date of change in format `Y-m-d\TH:i:sP`


## Order status changed webhook

The webhook is triggered when order status was changed.

### Example payload

Content-Type: `aplication/json`

`X-Event-Name` header: `order.status`

Request method: `POST`

```json
{
   "orderId": "PHS84FJAG5U",
   "orderExternalId": "AL2FEEHOO2OHF",
   "status": "canceled",
   "updatedAt": "2020-10-16T11:24:08+00:00"
}
```

Field | Type | Description
--------- | :-----: | -----------
`orderId` | string | Order ID
`orderExternalId` | string | Order external ID
`status` | string | [Order status](../api/v1/order/README.md#order-statuses)
`updatedAt` | string | Date of change in format `Y-m-d\TH:i:sP`


### How to respond for webhooks

For each webhook your endpoint should respond with status `2xx`.
After the first failure response we will try to resend webhook a couple of times at appropriate intervals.

> Keep in mind, that we are allowed to disable your endpoint when we detect too many failed responses. You should be notified about that case by e-mail.


### How to register webhooks

1. Login to your [Dashboard](https://www.kinguin.net/integration/dashboard/stores).
2. Go to **MY STORES** section and view store details.
3. Click on **WEBHOOKS** button.
4. Fill configuration form and click **SUBMIT** button.
5. Before saving, you can check if your endpoint responds correctly by clicking on **TEST URL** button.
6. Configure secret key to authorize incoming webhooks.
