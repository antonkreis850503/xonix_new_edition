<h1>Требования к проекту “Xonix New Edition”</h1>
<h2>1 Введение</h2>
<p align = "justify">Проект направлен на разработку сетевой многопользовательской игры под названием “Xonix New Edition”. Два пользователя будут иметь возможность подключаться к общему серверу и играть в режиме реального времени. Оформление игры двухмерное.</p>
<h2>2 Требования пользователя</h2>
<h3>2.1 Программные интерфейсы</h3>
<p align = "justify">Разработка будет вестись с использованием языка программирования Java. Будут задействованы как стандартные библиотеки, так и сторонние, например, LibGDX. Разработка будет вестись в Intellij Idea. В Таблице 1 собраны сведения об основных программных продуктах, которые будут использоваться в процессе разработки.</p>

Таблица 1 - Используемое в разработке стороннее ПО
<table align = "center">
  <tr>
    <td>Название</td>
    <td>Oracle Java SE 11</td>
    <td>libGDX</td>
    <td>JetBrains IntelliJ IDEA Community Edition </td>
  </tr>
    <tr>
    <td>Мнемоника</td>
    <td>Java</td>
    <td>libGDX</td>
    <td>IntelliJ IDEA</td>
  </tr>
    <tr>
    <td>Версия</td>
    <td>11.0.5</td>
    <td>1.9.10</td>
    <td>2019.3.5+</td>
  </tr>
</table>
<h3>2.2 Интерфейс пользователя</h3>
<p align = "justify">Создаваемый программный продукт будет иметь классический графический пользовательский интерфейс. При запуске пользователю предоставлено меню, в котором он сможет ввести свой Никнейм, а также данные для локального соединения с другим игроком, а также пункт “Настройки”. Меню будет оформлено в соответствии с тематикой игры. На рисунке 1 представлен набросок меню.
<img src="images/image_1.png" alt="Меню игры">
<p align = "center">Рисунок 1 - Меню игры</p>

<p align = "justify">После установления соединения с другим игроком пользователь включается в игровой процесс. На игровом поле будет происходить непосредственно игровой процесс (завоевание территорий игроками и т.д.), справа на информационном поле будет размещена прочая информация (например, текущий счет, текущее положение игроков, пункты управления и т.д.). На рисунке 2 представлена разметка и игрового процесса.</p>
<img src="images/image_2.png" alt="Разметка игрового процесса">
<p align = "center">Рисунок 2 - Разметка игрового процесса</p>

<h3>2.3 Характеристики пользователей</h3>
<p align = "justify">Программный продукт нацелен на рядового пользователя, обладающего компьютерными навыками и имеющим опыт в многопользовательских играх. Он должен уметь устанавливать соединение по локальной сети.</p>
<h3>2.4 Предположения и зависимости</h3>
<p align = "justify">На перечисленные в данном документе требования к создаваемому программному продукту могут влиять сроки, отведенные для разработки, а также новые идеи.</p>
<h2>3 Системные требования</h2>
<p align = "justify">Создаваемый программный продукт создается для работы в операционной системе Windows. Игроки должны подключиться к общей точке доступа. Для передачи данных по сети будут использоваться сокеты.</p>
<h3>3.1 Функциональные требования</h3>
<ul>
 <li>Понятный пользовательский интерфейс</li>
 <li>Красивые текстуры и анимация</li>
 <li>Третий пункт</li>
 <li>Оригинальность и хорошие игровые свойства</li>
 <li>Наличие многопользовательского режима</li>
 <li>(В перспективе) поддержка другими платформами</li>
</ul>
<h3>3.2 Нефункциональные требования</h3>
<h4>3.2.1 Атрибуты качества</h4>
<p align = "justify">Для создаваемого продукта необходимы такие атрибуты, как стабильность работы многопользовательского режима, невысокая требовательность к ресурсам компьютера.</p>
