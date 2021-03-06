<h1>Спецификации разработки ПО</h1>
<h2>1 Введение</h2>
<h3>1.1 Цель</h3>
<p align = "justify">Данный документ содержит детали реализации требований к проекту «Xonix New Edition».</p>
<h3>1.2 Обзор системы</h3>
<p align = "justify">Данный продукт представляет собой сетевую многопользовательскую игру. Он позволяет игроку создавать игровой сеанс, к которому может подключиться другой игрок (максимальное количество игроков - 2). Каждый из игроков может придумать и ввести свое пользовательское имя (Nickname). Игра происходит в реальном времени, игроки упрваляют мячиками и стремятся захватить определенное количество территорий за ограниченный промежуток времени. В конце игры пользователям будет предоставлена статистика завершенного игрового сеанса. Игра будет также предоставлять пользователю возможность настроек параметров сеанса и самого приложения игры. Пользователь сможет также ознакомиться с правилами игры.</p>
<h3>1.3 Карта документа</h3>
<p align = "justify">В данном документе содержатся информациях об основных решениях, которые будут использоваться при разработке проекта. В разделе 3 содержится информация о взаимодействии программ игроков, общая информация о классах приложения, диаграмма последовательности.</p>
<h3>1.4 Термины и сокращения</h3>
<p align = "justify">Для обозначения непосредственно игрового процесса между двумя игроками (уже после установления соединения) используется термин «Игровой сеанс».</p>
<p align = "justify">Для удобства обозначения двух игроков будем называть того игрока, работа программы которого описывается, «игроком», а игрока, использующего удаленный компьютер – «соперником».</p>
<h2>2 Обзор системы</h2>
<h3>2.1 Допущения</h3>
<p align = "justify">Количество игроков не будет превышать двух.</p>
<h3>2.2 Ограничения</h3>
<p align = "justify">Ограничения, серьезно влияющие на ход разработки, отсутствуют.</p>
<h3>2.3 Системная среда</h3>
<p align = "justify">Создаваемый программный продукт будет работать в операционной системе Windows 10.</p>
<h3>2.4 Методология разработки</h3>
<p align = "justify">Для создания данного программного продукта была выбрана объектно-ориентированная методология разработки ПО.</p>
<p align = "justify">Для сетевого взаимодействия используются сокеты.</p>
<h3>2.5 Риски и опасные места</h3>
<p align = "justify">Не выявлены.</p>
<h2>3 Архитектура</h2>
<h3>3.1 Обзор</h3>
<p align = "justify">Особенности архитектуры создаваемого приложения обусловлены объектно-ориентированной парадигмой разработки, а также тем, что данное приложение является сетевым.</p>
<h3>3.2 Протокол сетевого взаимодействия</h3>
<p align = "justify">Для реализации многопользовательского режима создаваемой игры использованы сокеты. В качестве сетевого протокола выбран протокол TCP. Приложения на разных компьютерах используют их для обмена информацией о текущем статусе игры. </p>
<p align = "justify">Перед началом игрового сеанса приложение, в котором он был создан, пересылает информацию о его конфигурации приложению второго игрока примерно в следующем формате (рис. 1):</p>
<p align="center">
<img src="../images/config_packet.png" alt="Формат пересылаемого сообщения до начала игрового сеанса">
</p> 
<p align = "center">Рисунок 1 – Формат пересылаемого сообщения до начала игрового сеанса</p>
<p align = "justify">Приложение второго игрока отвечает пересылкой своего никнейма (16 байт).</p> 
<p align = "justify">В соответствии с полученной от приложения соперника информацией, приложение игрока обновляет игровое поле и предоставляет пользователю новую информацию об игре. На рисунке 2 показан примерный формат передаваемого сообщения:</p> 
<p align="center">
<img src="../images/packet.png" alt="Формат пересылаемого сообщения во время игрового сеанса">
</p>
<p align = "center">Рисунок 2 – Формат пересылаемого сообщения во время игрового сеанса</p>
<p align = "justify">После получения сообщения приложение анализирует в первую очередь набор флагов. Среди основных флагов можно выделить следующие:</p> 
<ul>
 <li><p align = "justify">Флаг прерывания сеанса – соперник прервал игровой сеанс, получив такой флаг приложение игры сообщит об этом игроку и предложит вернуться в главное меню;</p></li>
 <li><p align = "justify">Флаг паузы – соперник поставил игру на паузу, игровой сеанс приостанавливается;</p></li>
 <li><p align = "justify">Флаг окончания игры – приложение соперника сообщило, что игра закончена.</p></li>
</ul>
<p align = "justify">Возможно использование и других служебных флагов.</p> 
<p align = "justify">Если игра продолжается, то приложение анализирует новое положение мячика соперника (поля «Новая позиция по оси Х» и «Новая позиция по оси Y»). В соответствии с этой информацией приложение игрока отрисовывает новое расположение мячика соперника. Данные пересылки происходят регулярно.</p> 
<p align = "justify">По завершении игрового сеанса программа игрока-создателя сеанса подводит итоги прошедшей партии и высылает другому игроку ее статистику примерно в следующем формате (рис. 3):</p> 
<p align="center">
<img src="../images/statistics_packet2.png" alt="Формат пересылаемого сообщения со статистикой игрового сеанса">
</p>
<p align = "center">Рисунок 3 – Формат пересылаемого сообщения со статистикой игрового сеанса</p>
<p align = "justify">Взаимодействие между программами игроков отражено на диаграмме последовательности (рис. 4).</p> 
<p align="center">
<img src="../images/seq6.png" alt="Диаграмма последовательности">
</p>
<p align = "center">Рисунок 4 – Диаграмма последовательности игры «Xonix New Edition»</p>
<h3>3.3 Классы</h3>
<p align = "justify">В соответствии с парадигмой объектно-ориентированного программирования за каждую важную деталь создаваемой игры отвечает отдельный класс. К основным классам можно отнести:</p>
<ul>
 <li><p align = "justify">MyBall – отвечает за мячик игрока;</p></li>
 <li><p align = "justify">EnemyBall – отвечает за мячик соперника;</p></li>
 <li><p align = "justify">Background – отвечает за фон;</p></li>
 <li><p align = "justify">SocketCommunication – отвечает за сетевое взаимодействие;</p></li>
 <li><p align = "justify">MainWindow – отвечает за главное меню;</p></li>
 <li><p align = "justify">SettingsWindow – отвечает за меню настроек;</p></li>
 <li><p align = "justify">SessionConfigurationWindow – отвечает за окно создания игрового сеанса;</p></li>
 <li><p align = "justify">GameResultsWindow – отвечает за окно, отображающее результаты игрового сеанса;</p></li>
 <li><p align = "justify">MessageWindow – отвечает за различные уведомления (такие как пауза, прерывание игры);</p></li>
 <li><p align = "justify">XonixGame – основной игровой класс;</p></li>
 <li><p align = "justify">DesktopLauncher – класс, отвечающий за запуск приложения на десктопе;</p></li>
 <li><p align = "justify">GameWindow – отвечает за игровое поле.</p></li>
</ul>
<h3>3.4 Диаграмма вариантов использования и интерфейс пользователя</h3>
<p align = "justify">На рисунке 5 изображена диаграмма вариантов использования создаваемой многопользовательской игры.</p>
<p align="center">
<img src="../images/use_case.png" alt="Диаграмма вариантов использования">
</p>
<p align = "center">Рисунок 5 – Диаграмма вариантов использования игры «Xonix New Edition»</h2>
<p align = "justify">Создаваемый программный продукт будет иметь классический графический пользовательский интерфейс. При запуске пользователю предоставлено меню, в котором он сможет ввести свой Никнейм, данные для локального соединения с другим игроком, а также сможет выбрать пункт “Настройки” или “Помощь”. Игрок может также создать игровой сеанс сам. В пункте "Помощь" пользователь может получить информацию о правилах игры и как установить соединение с соперником. Имеется пункт "Настройки" для конфигурирования приложения. Оформление меню и самой игры минималистичное, на фоне допускаются картинки, соответсвующие общему оформлению игры. На рисунке 6 представлен набросок меню.
<p align="center">
<img src="../images/image_1_new5.png" alt="Меню игры">
</p>
<p align = "center">Рисунок 6 - Меню игры</p>
<p align = "justify">Компьютеры соперников должны быть подключены к общей локальной сети (общий Wi-fi или точка доступа). Перед началом игрового процесса игрок, создающий игру, может выбрать ее длительность и количество захваченных территорий, необходимых для досрочного выигрыша. Предложен выход в главное меню. Далее игрок ожидает подключения своего соперника. Если соперник пытается подключиться к игре, он должен ввести IP адрес компьютера, на котором была создана игра (это значение будет указано на главном меню). Если она не была создана, то ему будет выведено соответствующее сообщение и будет предложен возврат в главное меню.(рис. 7)</p>
<p align="center">
<img src="../images/image_4_new.png" alt="Настройка партии">
</p> 
<p align = "center">Рисунок 7 - Настройка партии</p>
<p align = "justify">После установления соединения со свои соперником игрок включается в игровой процесс. На игровом поле будет происходить непосредственно игровой процесс (завоевание территорий игроками и т.д.), справа на информационном поле будет размещена прочая информация (например, текущие достижения игроков, кнопки выхода в главное меню и паузы и т.д.). Игроки управляют мячиками, отрезая тем самым себе территории. В начале игры мячики находятся в противоположных углах игрового поля. Создатель игрового сеанса управляет синим мячиком, его соперник - красным. Управление осуществляется стрелками клавиатуры, по диагонали мячики двигаться не могут. Игроки также мешают друг другу отрезать территории, пересекая след соперника (след существует до тех пор, пока территория не отрезана полностью.) При пересечении следа тот начинает постепенно пропадать, пока не достигнет мячика (исчезновение следа начинается в месте пересечения). Если мячик успел достигнуть отрезанной территории или края игрового поля, то след восстанавливается и мячик успешно отрезает территорию. Если два пользователя пересекают следы друг друга одновременно, то в проигрыше окажется тот игрок, чей след был пересечен ближе к его мячику. В результате след пропадает, и игрок вынужден начинать процесс отрезания территории заново. Для этого он должен попасть на отрезанную территорию и двигаться по "пустым" (неотрезанным) территориям. На рисунке 8 представлена разметка и игрового процесса.</p>
<p align="center">
<img src="../images/image_2_new++.png" alt="Разметка игрового процесса">
</p> 
<p align = "center">Рисунок 8 - Разметка игрового процесса</p>
<p align = "justify">Во время игры игрок может захотеть поставить игру на паузу. Для этого он длжен нажать соответствующую кнопку на экране (см. рис. 8). После этого он увидит следующее окно (рис. 9)</p> 
<p align="center">
<img src="../images/my_pause.png" alt="Окно паузы">
</p>
<p align = "center">Рисунок 9 - Окно паузы</p>
<p align = "justify">Его соперник будет ожидать окончания паузы, а может покинуть игровой сеанс. (рис. 10)</p> 
<p align="center">
<img src="../images/pause_enemy.png" alt="Окно паузы соперника">
</p>
<p align = "center">Рисунок 10 - Окно паузы соперника</p>
<p align = "justify">В конце игры игроку будет предоставлена статистика о завершенном сеансе. В ней будет содержаться информация о количестве захваченных территорий, о затраченном на сеанс времени и т.д. Будет предложен выход в главное меню.(рис. 11)</p> 
<p align="center">
<img src="../images/image_3_new.png" alt="Статистика сеанса">
</p>
<p align = "center">Рисунок 11 - Статистика сеанса</p>
<p align = "justify">Окно справки будет представлять собой текстовое поле с прокруткой, в котором будут содержаться правила игры и инструкция по подключению. (рис. 12)</p>
<p align="center">
<img src="../images/reference.png" alt="Окно справки">
</p>
<p align = "center">Рисунок 12 - Окно справки</p>
<p align = "justify">Окно настроек будет содержать те пункты, которые окажутся необходимы в процессе разработки. Если таких пунктов не будет, то пункт настроек можно убрать из главного меню. (рис. 13)</p>
<p align="center">
<img src="../images/settings.png" alt="Окно настроек">
</p>
<p align = "center">Рисунок 13 - Окно настроек</p>
<p align = "justify">В процессе работы программы возможно появление различных информационных сообщений (например, ожидание соперника). Формат такого сообщения приведен на рисунке 14.</p>
<p align="center">
<img src="../images/wait.png" alt="Окно сообщения">
</p>
<p align = "center">Рисунок 14 - Окно сообщения</p>
