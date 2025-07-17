# ECommerceReferrer class

This class contains information about the source of traffic. For example, a link to the page or screen that shows a product profile.

## Instance methods {#instance_summary}

#|
|| [init(type:identifier:screen:)](#method_initWithType__identifier__screen) | Initializes the instance of the `ECommerceReferrer` class with information about the source of traffic. ||
|#

## Properties {#property_summary}

#|
|| [type](#property_type) | Traffic source type: The type of object that traffic comes from. For example: <q>button</q>, <q>banner</q>, or <q>href</q>. Allowed size: Up to 100 characters. ||
|| [identifier](#property_identifier) | Traffic source ID. Allowed size: Up to 2048 characters. ||
|| [screen](#property_screen) | Traffic source screen: The screen that traffic comes from. ||
|#

## Method descriptions {#method_detail}

### init(type:identifier:screen:) {#method_initWithType__identifier__screen}

```swift translate=no
init(type: String?, identifier: String?, screen: ECommerceScreen?)
```

Initializes the instance of the `ECommerceReferrer` class with information about the source of traffic.

**Parameters:**

#|
|| `type` | Traffic source type: The type of object that traffic comes from. For example: <q>button</q>, <q>banner</q>, or <q>href</q>. Allowed size: Up to 100 characters. ||
|| `identifier` | Traffic source ID. Allowed size: Up to 2048 characters. ||
|| `screen` | Traffic source screen: The screen that traffic comes from. ||
|#

**Returns:**

The `ECommerceReferrer` class instance.

## Property descriptions {#property_detail}

### type {#property_type}

`var type: String? { get }`

Traffic source type: The type of object that traffic comes from. For example: <q>button</q>, <q>banner</q>, or <q>href</q>. Allowed size: Up to 100 characters.

### identifier {#property_identifier}

`var identifier: String? { get }`

Traffic source ID. Allowed size: Up to 2048 characters.

### screen {#property_screen}

`var screen: ECommerceScreen? { get }`

Traffic source screen: The screen that traffic comes from.
