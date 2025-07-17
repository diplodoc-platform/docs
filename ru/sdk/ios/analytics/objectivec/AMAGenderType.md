# AMAGenderType

Содержит возможные значения пола для класса [AMAGenderAttribute](AMAGenderAttribute.md).

## Перечисления {#enum_summary}

#|
|| [AMAGenderType](#enum_AMAGenderType) | Возможные значения пола для класса [AMAGenderAttribute](AMAGenderAttribute.md). ||
|#

## Описание перечислений {#enum_detail}

### AMAGenderType {enum_AMAGenderType}

`typedef NS_ENUM(NSUInteger, AMAGenderType)`

#|
|| **Константа** | **Описание** ||
|| `AMAGenderTypeMale` | Мужской пол. ||
|| `AMAGenderTypeFemale` | Женский пол. ||
|| `AMAGenderTypeOther` | Другое (например, недостаточно информации для определения пола).

{% note info %}

Вы можете установить `AMAGenderTypeOther` в качестве значения атрибута и передать дополнительную информацию с помощью пользовательских атрибутов.

{% endnote %} ||
|#
