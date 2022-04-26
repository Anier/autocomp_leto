# autocomp_leto

<p>
RUS: <b>Компонент на VUE.JS для автоматического заполнения поля ввода вариантами значений из предоставленного списка данных</b><br>
ENG: VUE.JS component for automatically filling the input field with value options from the provided list
</p>

<h3><a href="https://codepen.io/anier/full/jOYjmgM" target="_blank">DEMO here!!!</a></h3>

<p>
    Данный компонент создан без использования сторонних библиотек и может быть применён в любом приложении, созданном с помощью vue.js (ver. >= 2.x). 
    В работе с компонентом можно использовать стрелки на клавиатуре для перемещения по списку, а также Enter, для выбора нужного значения и отправки его родительскому компоненту.
</p>

<p>
    Для использования компонента необходимо настроить родительский компонент для передачи данных к <b>autocomp_leto</b>
</p>

```
<tools-autocomplect
      style="width: 200px"
      :datareturn="datareturn"
      :id="component_id"
      :css="css"
      :items="items">
</tools-autocomplect>
```

<p>
  Код выше, из родительского компонента, и в нем указываются: <br>
<table>
    <tr><td>style</td><td>width: 200px</td><td>Любые CSS стили для подчиненного компонента</td></tr>
    <tr><td>:datareturn</td><td>[method_name]</td><td>Название метода, который принимает выбранное в компоненте значение</td></tr>
    <tr><td>:id</td><td>[component_id]</td><td>ID компонента. При использовании нескольких компонентов на одной странице, нужно использовать разные ID</td></tr>
    <tr><td>:css</td><td>[css_styles]</td><td>Стили для кастомизации элементов компонента. Задаются в формате JS объекта, в секции data(). Объект может быть пустым.</td></tr>
    <tr><td>:items</td><td>[data_object]</td><td>Объект с обязательным полем "name". Объявляется в секции data() родительского компонинта.</td></tr>
</table>
</p>

```
 css: [
        {"ac-wrapper": {"zIndex": 3, "height": "50px"}},  // внешний блок компонента
        {"ac-input": {"backgroundColor": "#f5f5f5", "fontSize": "115%"}}, // стили для строки ввода
        {"ac-button": {"color":"green"}}, // стили для "кнопки отправки результата"
        {"ac-items": {"backgroundColor": "#eee"}}, // стили для контейнера всплывающего списка
        {"ac-item": {"fontSize": "80%", "color": "#666"}}, // стили для строки из списка
      ]
```
<p>
    При объявлении стилей, следует использовать "camelCase" написание свойств стилей (Пример: вместо z-index следует писать zIndex)
</p>

## Using component

Данный компонент поставляется в виде открытого кода и может использоваться и редактироваться под свои задачи без ограничений.

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).

