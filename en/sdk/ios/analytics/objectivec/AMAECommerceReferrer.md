# AMAECommerceReferrer class

This class contains information about the source of traffic. For example, a link to the page or screen that shows a product profile.

## Instance methods {#instance_summary}

#|
|| [-initWithType:identifier:screen:](#method_initWithType__identifier__screen) | Initializes the instance of the `AMAECommerceReferrer` class with information about the source of traffic. ||
|#

## Properties {#property_summary}

#|
|| [type](#property_type) | Traffic source type: The type of object that traffic comes from. For example: <q>button</q>, <q>banner</q>, or <q>href</q>. Allowed size: Up to 100 characters. ||
|| [identifier](#property_identifier) | Traffic source ID. Allowed size: Up to 2048 characters. ||
|| [screen](#property_screen) | Traffic source screen: The screen that traffic comes from. ||
|#

## Method descriptions {#method_detail}

### -initWithType:identifier:screen: {#method_initWithType__identifier__screen}

```objectivec translate=no
- (instancetype)initWithType:(nullable NSString *)type
                  identifier:(nullable NSString *)identifier
                      screen:(nullable AMAECommerceScreen *)screen
```

Initializes the instance of the `AMAECommerceReferrer` class with information about the source of traffic.

**Parameters:**

#|
|| `type` | Traffic source type: The type of object that traffic comes from. For example: <q>button</q>, <q>banner</q>, or <q>href</q>. Allowed size: Up to 100 characters. ||
|| `identifier` | Traffic source ID. Allowed size: Up to 2048 characters. ||
|| `screen` | Traffic source screen: The screen that traffic comes from. ||
|#

**Returns:**

The `AMAECommerceReferrer` class instance.

## Property descriptions {#property_detail}

### type {#property_type}

`(nonatomic, copy, readonly, nullable) NSString *type`

Traffic source type: The type of object that traffic comes from. For example: <q>button</q>, <q>banner</q>, or <q>href</q>. Allowed size: Up to 100 characters.

### identifier {#property_identifier}

`(nonatomic, copy, readonly, nullable) NSString *identifier`

Traffic source ID. Allowed size: Up to 2048 characters.

### screen {#property_screen}

`(nonatomic, strong, readonly, nullable) AMAECommerceScreen *screen`

Traffic source screen: The screen that traffic comes from.
