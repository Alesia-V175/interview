**Язык Liquid** — это язык шаблонов с открытым исходным кодом, встроенный в порталы. Он может использоваться для добавления динамического содержимого на страницы и создания множества разнообразных настраиваемых шаблонов.

Языки шаблонов также можно сравнить с функцией «Поиск и замена» в текстовых редакторах. Shopify осуществляет поиск всех заглушек Liquid и затем заменяет их данными из магазина. После чего, финальная версия документа отправляется браузеру в формате HTML.

Заглушка или *placeholder* представляет собой фрагмент кода, который заменяется данными, когда шаблон посылается в браузер.
В Liquid можно выделить два типа заглушек. 
- двойные фигурные скобки {{ }}, которые изображают вывод, `<h2>{{ product.title }}</h2>`
- фигурные скобки плюс знак процента {% %}, который отражает логику.

`{% if product.available %}`

Этот товар есть на складе

`{% else %}`

Извините, этот товар распродан

`{% endif %}`

Последняя строка в нашем примере – это завершающее выражение. Оно закрывает весь код, который должен быть сгенерирован в рамках текущего цикла.

Операторы в Liquid:

- == равно;
- != не равно;
- >больше чем;
- <меньше чем;
- >=больше или меньше;
- <=меньше или равно;
и т. д.

`{% for image in product.images %} 
<img src="{{ image | product_img_url: 'small' }}">
{% endfor %}`

где | - обозначение фильтр

========================================================================

`{{ 'style.css' | asset_url | stylesheet_tag }}`

Здесь мы используем два фильтра с общей целью: создать полноценный элемент style в нашем файле разметки.

Начинаем с названия CSS-файла слева, и сначала применяем к нему фильтр asset_url. Так как мы понятия не имеем, где в Shopify расположен необходимый нам файл style.css, нам нужно, чтобы платформа самостоятельно разобралась с нужным адресом.
Для этого и нужен фильтр asset_url. Он берет название нашего файла, style.css и составляет полноценный путь до этого файла в папке assets. Важно отметить, что он не осуществляет проверку наличия этого файла. Примерно так все будет выглядеть в итоге:

//cdn.shopify.com/s/files/1/0222/9076/assets/style.css

Второй фильтр, stylesheet_tag, берет этот URL, и оборачивает его в тег style, который позже выводится в файл разметки. Таким будет финальный результат:

`<link href="//cdn.shopify.com/s/files/1/0222/9076/t/10/assets/style.css?756" rel="stylesheet"  media="all"  />`

Каждый фильтр берет результат из предшествующего фильтра, а затем изменяет его по-своему. Если после него больше нет фильтров, то результат отправляется в шаблон в HTML-формате. 

========================================================================

Ссылка на шпаргалку http://cheat.markdunkley.com/
