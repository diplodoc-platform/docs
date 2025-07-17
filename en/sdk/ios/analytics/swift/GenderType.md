# GenderType

Contains possible gender values for the [GenderAttribute](GenderAttribute.md) class.

## Enumerations {#enum_summary}

#|
|| [GenderType](#enum_GenderType) | Contains possible gender values for the [GenderAttribute](GenderAttribute.md) class. ||
|#

## Enumeration descriptions {#enum_detail}

### GenderType {#enum_GenderType}

`enum GenderType : UInt`

#|
|| **Constant** | **Description** ||
|| `GenderType.male` | Male. ||
|| `GenderType.female` | Female. ||
|| `GenderType.other`| Other. For example, there is not enough info to detect the gender.

{% note info %}

You can set `GenderType.other` as the attribute value and pass additional information using custom attributes.

{% endnote %} ||
|#
