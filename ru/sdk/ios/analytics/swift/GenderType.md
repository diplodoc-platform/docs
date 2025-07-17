# GenderType

Содержит возможные значения пола для класса [GenderAttribute](GenderAttribute.md).

## Перечисления {#enum_summary}

#|
|| [GenderType](#enum_GenderType) | Содержит возможные значения пола для класса [GenderAttribute](GenderAttribute.md). ||
|#

## Описание перечислений {#enum_detail}

### GenderType {#enum_GenderType}

`enum GenderType : UInt`

#|
|| **Константа** | **Описание** ||
|| `GenderType.male` | Мужской пол. ||
|| `GenderType.female` | Женский пол. ||
|| `GenderType.other`| Другое (например, недостаточно информации для определении пола).

{% note info %}

Вы можете установить `GenderType.other` в качестве значения атрибута и передать дополнительную информацию с помощью пользовательских атрибутов.

{% endnote %} ||
|#
