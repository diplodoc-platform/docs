# AMAMutableRevenueInfo class

The mutable version of the [AMARevenueInfo](AMARevenueInfo.md) class with information about purchases.

The instance of the `AMAMutableRevenueInfo` class must be sent to the AppMetrica server using the [reportRevenue](AMAAppMetrica.md#method_reportRevenue) method of the [AMAAppMetrica](AMAAppMetrica.md) class.

## Properties {#property_summary}

#|
|| [payload](#property_payload) | Additional information to be passed about the purchase. For instance, it can be used for categorizing your products. ||
|| [productID](#property_productID) | ID of the product purchased. The value can contain up to 200 characters. ||
|| [quantity](#property_quantity) | Quantity of products purchased. ||
|| [receiptData](#property_receiptData) | Details about the in-app purchase order from App Store. This property is used for validating purchases in the app. ||
|| [transactionID](#property_transactionID) | Transaction ID [transactionIdentifier](https://developer.apple.com/documentation/storekit/skpaymenttransaction/1411288-transactionidentifier) from the [SKPaymentTransaction](https://developer.apple.com/documentation/storekit/skpaymenttransaction) class. This property is used for validating purchases in the app. ||
|#

## Property descriptions {#property_detail}

### payload {#property_payload}

`(nonatomic, copy) NSDictionary *payload`

Additional information to be passed about the purchase. For instance, it can be used for categorizing your products.

It should contain the `NSDictionary` object that can be converted to valid JSON. The maximum size of the value is 30 KB.

### productID {#property_productID}

`(nonatomic, copy) NSString *productID`

ID of the product purchased. The value can contain up to 200 characters.

### quantity {#property_quantity}

`(nonatomic, assign) NSUInteger quantity`

Quantity of products purchased.

It is used in the following formula:

```
Revenue = quantity * price.
```

{% note info %}

The value cannot be negative. If the value is equal to 0, the purchase is ignored.

{% endnote %}

### receiptData {#property_receiptData}

`(nonatomic, copy) NSData *receiptData`

Details about the in-app purchase order from App Store. This property is used for validating purchases in the app. For more information, see the [Apple documentation](https://developer.apple.com/library/content/releasenotes/General/ValidateAppStoreReceipt/Chapters/ValidateRemotely.html).

See the example of getting `receiptData` in the [Sending Revenue](../ios-operations.md#send-revenue) section.

{% note alert %}

The value must be received before invoking `[[SKPaymentQueue defaultQueue] finishTransaction:transaction]` and transmitted along with [transactionID](#property_transactionID).

{% endnote %}

### transactionID {#property_transactionID}

`(nonatomic, copy) NSString *transactionID`

Transaction ID [transactionIdentifier](https://developer.apple.com/documentation/storekit/skpaymenttransaction/1411288-transactionidentifier) from the [SKPaymentTransaction](https://developer.apple.com/documentation/storekit/skpaymenttransaction) class. This property is used for validating purchases in the app.

See the example of getting `transactionIdentifier` in the [Sending Revenue](../ios-operations.md#send-revenue) section.

{% note alert %}

This value should be passed along with [receiptData](#property_receiptData).

{% endnote %}
