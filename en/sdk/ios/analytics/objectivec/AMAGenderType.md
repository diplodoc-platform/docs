# AMAGenderType

Contains possible gender values for the [AMAGenderAttribute](AMAGenderAttribute.md) class.

## Enumerations {#enum_summary}

#|
|| [AMAGenderType](#enum_AMAGenderType) | Possible gender values for the [AMAGenderAttribute](AMAGenderAttribute.md) class. ||
|#

## Enumeration descriptions {#enum_detail}

### AMAGenderType {enum_AMAGenderType}

`typedef NS_ENUM(NSUInteger, AMAGenderType)`

#|
|| **Constant** | **Description** ||
|| `AMAGenderTypeMale` | Male. ||
|| `AMAGenderTypeFemale` | Female. ||
|| `AMAGenderTypeOther` | Other. For example, there is not enough info to detect the gender.

{% note info %}

You can set `AMAGenderTypeOther` as the attribute value and pass additional information using custom attributes.

{% endnote %} ||
|#
