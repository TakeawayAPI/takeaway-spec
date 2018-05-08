# Unofficial Takeaway.com API specification

This is an unofficial description of the Takeaway.com API, used by their mobile apps.

## Communication
The Takeaway.com API is an HTML API which closely resembles XML-RPC. All requests take the form of remote procedure calls and return XML data, but requests are given as form data rather than XML. Furthermore, the data sent to the backend is signed. The data returned by the backend is not signed.

Every request goes to https://citymeal.com/android/android.php. All requests are `POST` requests, with the body describing what the client wants from the backend.

A request consists of a method and arguments for the method. They are named `var1` and `var2`, `var3`, ..., respectively. For example, if we were to call `getdatafromgeolocation(52, 6, 1)`, we would end up with the following data:

```
var1 = getdatafromgeolocation
var2 = 52
var3 = 6
var4 = 1
```

After composing the data, the values of all `var`s are concatenated. The `md5` hash of this string with the string '4ndro1d' appended is then set as `var0`.

Furthermore, the following values should also be sent. Some methods do not require them though.

|Name|Value|Description|
|--|--|--
|`version`|`5.7`|Version of the Takeaway.com app
|`systemversion`|`24`|_Unknown_
|`appname`|`Takeaway.com`|Name of the Takeaway.com app
|`language`|`en`|Language of the user

All values are then encoded as `x-www-form-urlencoded` form data with a UTF-8 content type and sent to the server.

The server _may_ reply with an XML body. If anything is not up to spec, the server may return an empty body, along with a HTTP 412 Precondition Failed status. If a request is up to spec, but fails on the server side, the server _may_ fail with an HTTP 500 Internal Server Error status and _may_ return an XML object. This XML object takes many forms, as many components of the Takeaway.com framework may emit errors from different locations, including external libraries.

Upon success, the XML body has a different form depending on the specification. To find out what the data exactly means, refer to one of our libraries and checkout the source code. There are plans to formalize the XML specification to language-agnostic data.

## Available methods

- `getcurrenttime(countryCode, restaurantId, orderingMode)`
- `getrestaurants(postalCode, countryCode, lat, lon, language)`
- `getdiscounts(restaurantId | postalCode, countryCode, language, 'zipcode' | 'restid')`
- `getcountriesdata()`
- `getrestaurants(postcode, countryCode, lat, lon, language)`
- `getdiscounts(restaurantId | postcode, countryCode, language, 'zipcode' | 'restid')`
- `getdatafromgeolocation(lat, lon, countryCode)`
- `getrestaurantdata(restaurantId, postcode, '1', lat, lon, clientId | '')`
- `getrestaurantdatacheckout(restaurantId, postcode, '1', lat, lon, clientId | '')`
- `restaurantreviews(restaurantId, page)`
- `getidealmobielbanks(restaurantId)`
- `userauth(userName, userCredentials, countryCode, clientId, siteCode, (1, socialType, socialToken) | (0, '', ''))`
- `importoldorders(userName, userCredentials, countryCode, clientId, siteCode)`
- `resetpassword(email, countryCode, language, siteCode)`
- `getaddresslist(userName, userCredentials, countryCode, siteCode)`
- `getorderhistory((email, clientId) | (userName, userCredentials), countryCode, page, siteCode, isLoggedIn)`
- `getorderdetails((email, clientId) | (userName, userCredentials), countryCode, orderId, siteCode, isLoggedIn)`
- `checkvoucher(voucherCode, siteCode, restaurantId, email, clientId | '', productIds)`
- `recurringpayments(action, paymentMethod, clientId | '', (userName, userCredentials) | ('', ''), isLoggedin, countryCode, siteCode)`

If the `paymentMethod` is `13` (a voucher code), an order may be reserved like so:

```
reserveorder(
    '', name, companyName, street, '', postcode, city, phone, email,
    deliveryTime, paymentPart, remarks, newsletter, restaurantId,
    formattedOrder, siteCode, language, countryCode, clientId | '',
    paymentMethod, '', foodTrackerId, deliveryAreaId, '',
    orderingMode == 3 ? extraAddressJson : '', userName | '',
    userCredentials | '', addressId | '', deliveryMethod, '0',
    voucherCode | '', '', lat, lon
)
```

Otherwise, an order may be placed by using `placeorder` with the exact same arguments, but leaving `voucherCode` blank.

Furthermore, a method exists for each payment method. The name for such a method _is_ the payment method, and the arguments are `paymentId, androidPayToken | (saveReference, userName | '', userCredentials | ''`.
