## сборники рецептов jq ##

Мы все иногда сталкиваемся с необходимостью вытащить нужную
информацию из JSON или YAML файлов. Многие уже познакомились с мощью
утилиты jq. Судя по публикациям на Хабре, напр. <https://habr.com/ru/post/525808/>,
и вопросам в qna, тема до сих пор актуальна.

Мне в очередной раз пришлось вспомнить специфический DSL jq чтобы
восстановить накопленные за долгое время закладки в Хроме, не
сохранённые при апгрейде. Точнее, файл Bookmarks в формате .json сохранился,
но ни в какую не хотел импортироваться в новый Хром. Хочу поделиться
рецептом решения этой проблемы, заодно упорядочить собранные в
разных местах миниатюрные скрипты для решения похожих проблем.

JQ в действительности полноценный язык программирования со всеми
атрибутами - переменными, типами данных, арифметикой, циклами и
условными переходами, массой встроенных функций и возможностью
добавления новых. Удивительно, всё это в программке размером 30KB,
страницей "man jq" такого же размера и библиотекой libjq размером 300KB.

Итак, заглянув в свой Bookmarks с несколькими сотнями ссылок, первый
вопрос - какова структура этого .json файла? По счастью, я уже знал
как быстро её посмотреть и использовать в дальнейших запросах. Вот
эта команда:

  ... $ jq '[paths|join(".")]' Bookmarks|head -n 16
  [
    "checksum",
    "roots",
    "roots.bookmark_bar",
    "roots.bookmark_bar.children",
    "roots.bookmark_bar.children.0",
    "roots.bookmark_bar.children.0.children",
    "roots.bookmark_bar.children.0.children.0",
    "roots.bookmark_bar.children.0.children.0.children",
    "roots.bookmark_bar.children.0.children.0.children.0",
    "roots.bookmark_bar.children.0.children.0.children.0.date_added",
    "roots.bookmark_bar.children.0.children.0.children.0.guid",
    "roots.bookmark_bar.children.0.children.0.children.0.id",
    "roots.bookmark_bar.children.0.children.0.children.0.name",
    "roots.bookmark_bar.children.0.children.0.children.0.type",
    "roots.bookmark_bar.children.0.children.0.children.0.url",

Всего строк по количеству записей в json файле, нам достаточно
увидеть структуру самого первого блока данных, далее она в основном
повторяется. Уже видно, что Хромовские закладки организованы как
вложенные папки и собственно ссылки.  Папки здесь обозначены как
массивы children, а ссылки как хэши с соответствующими полями.

Хром умеет импортировать закладки в виде .html файла. Ссылка в этом файле
выглядит таким образом:

        <DT><A HREF="https://www.youtube.com/watch?v=qbEPae8YNbs&t=3142s" ADD_DATE="0">Deep Dive on Amazon ECS - Brent Langston</A>
        <DT><A HREF="https://aws.amazon.com/blogs/aws/new-import-existing-resources-into-a-cloudformation-stack/" ADD_DATE="0">Import Existing Resources into a CloudFormation Stack</A>

Таким образом, нам надо достать из json файла все значения .url и
.name, затем добавить их в таблицу .html как строки. Значение ADD_DATE не
обязательно.  Вот так это извлекается из уже знакомой нам структуры
данных .json файла:

    ... $ jq '.roots.bookmark_bar.children[].children[] | .url, .name' Bookmarks|tail -n 4
    "http://lib.rus.ec/b/285485/read"
    "Мир многих миров. Физики в поисках иных вселенных (fb2) | Либрусек"
    "https://picasaweb.google.com/Dr.Anticommunij"
    "Picasa Web Albums - ophil"

Здесь вместо индекса массива в .json файле использовано обозначение
[], означающее итерацию по всем элементам массива. Идём дальше. С
такой же лёгкостью можно добавить в вывод желаемые строки, чередуя
строки в фильтре со значениями из хэша:

    ... $ jq -jr '.roots.bookmark_bar.children[].children[] | ("<DT><A HREF=\"", .url, "\">", .name, "</A>\n")' Bookmarks|tail -n 2
    <DT><A HREF="http://lib.rus.ec/b/285485/read">Мир многих миров. Физики в поисках иных вселенных (fb2) | Либрусек</A>
    <DT><A HREF="https://picasaweb.google.com/Dr.Anticommunij">Picasa Web Albums - ophil</A>


Внимательный читатель заметил, что выше использованы 2 опции запуска jq:

  - -j --join-output - не вставлять новую строку в выводе, её можно задавать самому, см. символ **\n**
  - -r --raw-input - не выводить кавычки как в объектах json, их снова задаю вручную

Для сохранения всех закладок надо повторить эту команду для всех
вложенных папок, например, добавить ещё один уровень вложенности
.children[] и добавить результат в понятный Хрому .html файл. Начальный файл
можно сделать создав в Хроме одну ссылку и экспортировав в файл, в
который **добавим** извлечённые из старого Bookmarks закладки. Пару строк
закрытия таблицы в самом экспортированном файле нужно удалить
перед добавленными строками и вставить в самый конец:

        </DL><p>
    </DL><p>

Импорт покажет все закладки без разбиения на папки, но это лишь
хороший повод навести порядок, удалить ненужные и отсортировать
их в менеджере закладок Хрома с учётом прожитых лет.

Мощь jq работает точно также с файлами **.yaml** и **.xml**.
Автор проекта "[yq: Command-line YAML/XML processor](https://github.com/kislyuk/yq)" 
Андрей Кислюк для работы с этими форматами данных не стал изобретать
велосипед, а реализовал на языке python преобразование YAML/XML в JSON, затем
передачу команд и опций для выполнения в jq. Обратное преобразование
в yaml задаётся опциями -y или -Y, если необходимо, см. <https://kislyuk.github.io/yq/>

Замечательный сборник рецептов нашёл у Remy Sharp'а <https://remysharp.com/drafts/jq-recipes>.
Нашёл его поиском "jq cookbook", лучше него что-то сделать трудно.
Надеюсь, его рецепты будут доступны несмотря на текущий статус draft.

Нельзя не посоветовать также документацию автора **jq**  [Stephen Dolan'а](https://github.com/stedolan).
Кроме самой [документации](https://stedolan.github.io/jq/manual/), есть также 
[tutorial](https://stedolan.github.io/jq/tutorial/), [wiki](https://github.com/stedolan/jq/wiki),
[FAQ](https://github.com/stedolan/jq/wiki/FAQ) и [ещё один сборник рецептов](https://github.com/stedolan/jq/wiki/Cookbook).
