# Jenkins

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java/Jenkins/jenkins-banner-1.jpg)

Каждый день в компания по разработке ПО одновременно работает большое количество разработчиков, тестировщиков, исследователей и других технических специалистов. Такое большое количество людей необходимо как-то координировать и снабжать свежими версиями продукта.

Для этого используется Jenkins — веб-приложение, написанное н Java, для обеспечения непрерывной интеграции и непрерывной поставки ПО. Разработчики с помощью Jenkins могут настроить автоматическую сборку проектов и изменение репозитория с кодом, а тестировщики могут легко получить доступ к свежей версии продукта и автоматизировать процесс тестирования.

Работу Jenkins можно рассмотреть на примере большого конвейера на автомобильном заводе, который практически в автоматическом режиме собирает машины из отдельных запчастей, а в самом процессе участвует в разы меньше людей, чем при ручной сборке. Тестировщики используют Jenkins для автоматизации процесса тестирования. Тесты практически всегда состоят из множества модулей и инструментов, которые необходимо связать между собой и вызывать одновременно или поочерёдно. В ручную это бы занимало много времени и для этого понадобились бы отдельные специалисты в команде, а в больших проектах — целый отдел.

С Jenkins тесты можно запускать после выхода каждой новой версии продукта или по заданному расписанию. К тому же Jenkins будет запускать не только код автотестов, но и инструменты для аналитики тестов, сбора данных и формирования отчётов. Всё в это в автоматическом режиме. Поэтому если проекта подразумевает запускать все тесты каждый час, то это не надо будет делать вручную, а можно один раз настроить CI-конфигурацию в Jenkins.

## Как это работает
Запуск тестов на локальной машине обычно происходит через среду разработки. Которая берёт исходный код тестов из памяти компьютера, запуск все подключенные библиотеки, собирает необходимые инструменты и прогоняет тесты в браузере. Всё это происходит на локальном компьютере и доступно только одному тестировщику.

В случае с Jenkins тесты запускаются на выделенном сервере, актуальный код берётся из репозитория GitHub, а прогоняются тесты в Selenoid. В этом случае результаты тесты доступны не только автору кода, но и всем участникам команды, которые работают над проектом. Запускать тесты тоже может любой участник, что ускоряет разработку.

## Установка
Jenkins представляет собой веб-приложение, поэтому его нельзя установить на свой компьютер в виде отдельного приложения. В компаниях обычно разворачивают собственный стенд для тестирования на базе Jenkins. Но инструмент полностью бесплатный и с открытым исходным кодом, поэтому при необходимости и желании можно развернуть Jenkins на собственном сервере.
