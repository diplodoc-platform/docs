# Подключение CSS

CSS-стили позволяют адаптировать оформление документации под различные требования — от тонкой настройки отдельных элементов до создания единого визуального стиля.

Вы можете использовать CSS-стили как для отдельных элементов на странице, так и для всего проекта.

## Применение стиля к отдельной странице

Чтобы использовать стиль на странице документации:

1. В конец страницы документации пропишите тег <style> с атрибутом scoped.
1. В тело тега <style> добавьте код для стилизация элемента.

{% cut "Пример использования кастомного стиля" %}

  {% cut "Код для стилизации кнопки" %}

  ```
  <style scoped>
  .button {
    border: none;
    outline: none;
    display: inline-block;
    text-align: center;
    text-decoration: none;
    cursor: pointer;
    font-size: 28px;
    font-family: var(--yc-text-body-font-family);
    padding: 8px 8px;
    border-radius: 10px;
    background-color: #e4edff;
    margin-top: 20px;
    transition: all .4s ease;
    }

  .button:hover{
    transform: scale(1.1);
  }

  .button:active {
    box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.2);
    text-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
    background: #ffd633;
  }
  </style>
  ```

  {% endcut %}

Результат:

<span class="button">Кнопка</span>

{% endcut %}

## Применение стиля к проекту

Чтобы подключить стиль к проекту:

1. В корне проекта создайте файл с css-стилем: `_assets/style/custom.css` 
1. Добавьте в файл код для стилизации.
1. В конфигурационном файле .yfm добавьте следующий блок:
    ```
    resources:
      style:
        - _assets/style/custom.css
    ```
1. Соберите проект с флагом `--allow-custom-resources`.

Пример использования стилей см. в [репозитории Diplodoc](https://github.com/diplodoc-platform/docs).

<style scoped>
.button {
  border: none;
  outline: none;
  display: inline-block;
  text-align: center;
  text-decoration: none;
  cursor: pointer;
  font-size: 28px;
  font-family: var(--yc-text-body-font-family);
  padding: 8px 8px;
  border-radius: 10px;
  background-color: #e4edff;
  margin-top: 20px;
  transition: all .4s ease;
  }
  .button:hover{
    transform: scale(1.1);
  }
  .button:active {
    box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.2);
    text-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
    background: #ffd633;
  }
</style>