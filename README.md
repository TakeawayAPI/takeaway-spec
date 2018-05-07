# Unofficial Takeaway.com API specification

```
getcurrenttime(countryCode, restaurantId, orderingMode)
getcountriesdata()
getrestaurants(postcode, countryCode, lat, lon, language)
getdiscounts(restaurantId | postcode, countryCode, language, 'zipcode' | 'restid')
getdatafromgeolocation(lat, lon, countryCode)
getrestaurantdata(restaurantId, postcode, '1', lat, lon, clientId | '')
getrestaurantdatacheckout(restaurantId, postcode, '1', lat, lon, clientId | '')
restaurantreviews(restaurantId, page)
getidealmobielbanks(restaurantId)
if (paymentMethod == 13) {
    reserveorder('', name, companyName, street, '', postcode, city, phone, email, deliveryTime, paymentPart, remarks, newsletter, restaurantId, formattedOrder, siteCode, language, countryCode, clientId | '', paymentMethod, '', foodTrackerId, deliveryAreaId, '', orderingMode == 3 ? extraAddressJson : '', userName | '', userCredentials | '', addressId | '', deliveryMethod, '0', voucherCode | '', '', lat, lon)
} else {
    placeorder('', name, companyName, street, '', postcode, city, phone, email, deliveryTime, paymentPart, remarks, newsletter, restaurantId, formattedOrder, siteCode, language, countryCode, clientId | '', paymentMethod, '', foodTrackerId, deliveryAreaId, '', orderingMode == 3 ? extraAddressJson : '', userName | '', userCredentials | '', addressId | '', deliveryMethod, '0', voucherCode | '', '', lat, lon)
}
{paymentMethod}(paymentId, androidPayToken | (saveReference, userName | '', userCredentials | ''))
userauth(userName, userCredentials, countryCode, clientId, siteCode, (1, socialType, socialToken) | (0, '', ''))
importoldorders(userName, userCredentials, countryCode, clientId, siteCode)
resetpassword(email, countryCode, language, siteCode)
getaddresslist(userName, userCredentials, countryCode, siteCode)
getorderhistory((email, clientId) | (userName, userCredentials), countryCode, page, siteCode, isLoggedIn)
getorderdetails((email, clientId) | (userName, userCredentials), countryCode, orderId, siteCode, isLoggedIn)
checkvoucher(voucherCode, siteCode, restaurantId, email, clientId | '', productIds)
recurringpayments(action, paymentMethod, clientId | '', (userName, userCredentials) | ('', ''), isLoggedin, countryCode, siteCode)
```

