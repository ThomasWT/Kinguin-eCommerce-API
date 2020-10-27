# Changelog

## [Unreleased]

### Breaking change (release: end of September 2020)
- type of `orderId` and `offerId` fields/parameters will be transformed to `string`, current is `mixed` (`string` or `integer`). The change includes endpoints:
    - `POST /api/v1/order`
    - `GET /api/v1/order`
    - `GET /api/v1/order/{orderId}`
    - `POST /api/v1/order/dispatch`
    - `GET /api/v1/products`
    - `GET /api/v1/products/{kinguinId}`
- new error response format, [details here](apidocs/ErrorsCodes.md#list-of-error-kinds)
- `image` choice from `keyType` property will be removed
- `imageQty` property from product and offer will be removed
- all failed transactions will be moved from merchant's dashboard

### Added (release: end of September 2020)
- added `couponCode` property to order request payload, [details here](features/CouponCode.md#ask-for-coupon)
- added `orderExternalId` property to order request payload, [details here](features/OrderExternalId.md)
- added `orderExternalId` filter for `/api/v1/order` endpoint
- added `offerId` property to response from `/api/v1/order/dispatch/keys` endpoint
- added `paymentPrice`, `requestTotalPrice`, `products.requestPrice` fields to order, [details here](features/CouponCode.md#using-coupon)
- added `X-Api-Key` header as a replacement/alias for `Api-Ecommerce-Auth`
- added `/api/v2/order/{orderId}/dispatch` endpoint, [details here](apidocs/order/v2/README.md#dispatch-order)
- added `/api/v2/order/{orderId}/keys` endpoint, [details here](apidocs/order/v2/README.md#get-order-keys)
- added multiple values search for `genre` and `platform` filters,

### Changed
- product `preorder_from_date` and `preorder_to_date` fields set as **DEPRECATED** and will be removed on July. Now `releaseDate` field stores information about activity of preorder.
- product `origin_score` field set as **DEPRECATED** and will be removed on July
- product `type` field set as **DEPRECATED** and will be removed on July (values are always `serial`)
- product `status` field set as **DEPRECATED** and will be removed on July (values are always `Active`)
- offer `type` field set as **DEPRECATED** and will be removed on July (values are always `serial`)
- offer `offerId` field will be typeof `integer` or `string` (this change will be also applicable in ordered products)
- offer `vendorName` will be renamed to `merchantName`
- offer `isCheapest` field set as **DEPRECATED** and will be removed on July
- filter `vendorName` for products will be renamed to `merchantName`
- `steam gift` and `preorder` tags set as **DEPRECATED** and will be removed on July

## [2019-12-10]

### Added
- possibility to select key type (`text` or `image`), [details here](how_to/KeyType.md#how-to-select-key-type)
- possibility to buy selected offer, [details here](how_to/BuyOffer.md#how-to-buy-selected-offer)
- added `vendorName` and `onlyText` filters to products, [details here](apidocs/products/README.md#list-products)
- added `textQty`, `imageQty` to product, [details here](apidocs/products/README.md#product-object)
- added `offers`, `offersCount`, `totalQty` to product, [details here](apidocs/products/README.md#offer-object)

### Removed
- removed `newsFromDate`, `newsToDate`, `stock` from product (was DEPRECATED before)

## [2019-03-27]

### Added
- min length validation for `name` filter, [details here](apidocs/products/README.md#list-products)

### Changed
- `kinguinId` filter accepts multiple `kinguinId` values, [details here](apidocs/products/README.md#list-products)
- `stock` field is **DEPRECATED** and will be removed, use `qty` field instead

### Removed
- removed `steamScore` from products fields
- removed `stock` filter

## [2019-02-28]

### Added
- added `isPreorder` filter to orders endpoint, [details here](apidocs/order/README.md#get-orders)
- added `isPreorder` to `order.products` collection, [details here](apidocs/order/README.md#get-orders)

## [2019-02-21]

### Added
- added `coverImageOriginal` to product, [details here](apidocs/products/README.md#product-object)
- added `genre` filter, [details here](apidocs/products/README.md#list-products)

### Changed
- updated products genres list, [details here](apidocs/products/README.md#genres)

## [2019-01-23]

### Added
- add `offerId` to `order.products` collection, [details here](apidocs/order/README.md#get-orders)

## [2019-01-09]

### Added
- postback notifications for products updates, [details here](features/Postback.md#products-updates-notifications)

## [2018-11-20]

### Added
- new endpoint GET /order, [details here](apidocs/order/README.md#get-orders)

## [2018-11-14]
### Changed
- product `regionalLimitations` field now stores a *name of region* instead of url to icon
- fields such as `originalName`, `description`, `coverImage`, `screenshots`, `videos`, `developers`, `publishers` and `releaseDate` have become optional fields and may not be accessible for all products
- product `sortBy` field has been limited to `kingiunId`, `name`, `qty` and `price` values
- product `sortType` filed has been limited to `asc` and `desc`
  
### Added
- product `regionId` filed which stores id of *region name*, [details here](apidocs/products/README.md#regions)
- `originalName` field which stores base name of product
- `isPreorder` field
- `status` filed which indicates if offer is active and ready to buy at Kinguin platform. The valid product should have `active` status. *IMPORTANT: Products only with that status can be ordered at Kinguin platform*
- `type` field which stores the type of product. For now there is only one `serial` available value. *IMPORTANT: Only `serial` products will be exposed by Product Api*
- `systemRequirements` field which stores list of hardware requirements for the product
- `tags` field which stores list of product's tags, [details here](apidocs/products/README.md#tags)
- added `isPreorder` parameter to query filters (acceptable values are `yes` and `no`)
- added `activePreorder` parameter to query filters (acceptable value is `yes`). It checks only the date of preorder activity, so if you want get only active preorders just use both parameters `isPreorder=yes` and `activePreorder=yes`
- added `regionId` parameter to query filters
- added `tags` parameter to query filters. It should be comma separated list of tags
- added `updatedSince` and `updatedTo` parameters to query filters. Both should be a valid UTC date. It allows to filter products by last update date

## [2018-11-13]
### Changed
- improved [errors and messages](apidocs/ErrorsCodes.md)

### Added
- `kinguinId` in order/dispatch/keys endpoint
