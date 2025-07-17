# MutableRevenueInfo class

The mutable version of the [RevenueInfo](RevenueInfo.md) class with information about purchases.

The instance of the `MutableRevenueInfo` class should be sent to the AppMetrica server using the [reportRevenue](AppMetrica.md#method_reportRevenue) method of the [AppMetrica](AppMetrica.md) class.

## Properties {#property_summary}

#|
|| [payload](#property_productID) | Additional information to be passed about the purchase. For instance, it can be used for categorizing your products. ||
|| [productID](#property_productID) | ID of the product purchased. The value can contain up to 200 characters. ||
|| [quantity](#property_quantity) | Quantity of products purchased. ||
|| [receiptData](#property_receiptData) | Details about the in-app purchase order from App Store. This property is used for validating purchases in the app. ||
|| [transactionID](#property_transactionID) | Transaction ID [transactionIdentifier](https://developer.apple.com/documentation/storekit/skpaymenttransaction/1411288-transactionidentifier) from the [SKPaymentTransaction](https://developer.apple.com/documentation/storekit/skpaymenttransaction) class. This property is used for validating purchases in the app. ||
|#

## Property descriptions {#property_detail}

### payload {#property_payload}

`var payload: [AnyHashable : Any]`

Additional information to be passed about the purchase. For instance, it can be used for categorizing your products.

You must pass the `AnyHashable` object that can be converted to a valid JSON. The maximum size of the value is 30 KB.

### productID {#property_productID}

`var productID: String`

ID of the product purchased. The value can contain up to 200 characters.

### quantity {#property_quantity}

`var quantity: UInt`

Quantity of products purchased.

It is used in the following formula:

```
Revenue = quantity * price.
```

{% note info %}

The value cannot be negative. If the value is equal to 0, the purchase is ignored.

{% endnote %}

### receiptData {#property_receiptData}

`var receiptData: Data`

Details about the in-app purchase order from App Store. This property is used for validating purchases in the app. For more information, see the [Apple documentation](https://developer.apple.com/library/content/releasenotes/General/ValidateAppStoreReceipt/Chapters/ValidateRemotely.html).

See the example of getting `receiptData` in the [Sending Revenue](../ios-operations.md#send-revenue) section.

{% note alert %}

The value must be received before invoking `SKPaymentQueue.default().finishTransaction(transaction)` and transmitted along with [transactionID](#property_transactionID).

{% endnote %}

### transactionID {#property_transactionID}

`var transactionID: String`

Transaction ID [transactionIdentifier](https://developer.apple.com/documentation/storekit/skpaymenttransaction/1411288-transactionidentifier) from the [SKPaymentTransaction](https://developer.apple.com/documentation/storekit/skpaymenttransaction) class. This property is used for validating purchases in the app.

See the example of getting `transactionIdentifier` in the [Sending Revenue](../ios-operations.md#send-revenue) section.

{% note alert %}

The value must be received before invoking `SKPaymentQueue.default().finishTransaction(transaction)` and transmitted along with [receiptData](#property_receiptData).

{% endnote %}
