
- [Allure TestOps Python](#allure-testops-python)
  - [Интеграция Jenkins и Allure TestOps](#интеграция-jenkins-и-allure-testops)
  - [Авторизация в Allure TestOps](#авторизация-в-allure-testops)
  - [Добавляем Allure TestOps в jenkins джобу](#добавляем-allure-testops-в-jenkins-джобу)
  - [Добавляем отображение проекта Allure TestOps в jenkins джобе](#добавляем-отображение-проекта-allure-testops-в-jenkins-джобе)
  - [Как подключить интеграцию и запуск джобы в Jenkins через Allure TestOps](#как-подключить-интеграцию-и-запуск-джобы-в-jenkins-через-allure-testops)
    - [Как узнать свой Username в Jenkins](#как-узнать-свой-username-в-jenkins)
    - [Как создать API token в Jenkins](#как-создать-api-token-в-jenkins)
  - [Как подключить интеграцию с Jira](#как-подключить-интеграцию-с-jira)
  - [Живая документация](#живая-документация)
  - [Автоматизация](#автоматизация)
  - [Запуск тестов](#запуск-тестов)
  - [Разбор отчётов](#разбор-отчётов)


# Allure TestOps Python 

Allure TestOps — это TMS(тест-менеджмент система) для автоматизированных тестов. Она позволяет хранить тест-кейсы, запускать тесты и смотреть результаты их выполнения. Allure TestOps позволяет интегрироваться с различными фреймворками, такими как JUnit, TestNG, PyTest и интегрироваться с CI/CD системами, такими как Jenkins, TeamCity и другими. А также взаимодействовать с различными системами управления задачами, такими как Jira, Trello и другими.

Репозиторий с примером проекта можно найти [тут](https://github.com/eroshenkoam/allure-pytest-example).

## Интеграция Jenkins и Allure TestOps
Пример реализации самой простой "джобы" в jenkins с Allure TestOps:

1. Параметризованная сборка с параметрами `ENDPOINT` и `BROWSER`, и значением по умолчанию `https://testing.github.com` и `firefox`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jenkins_testops.jpeg)

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jenkins_testops_2.jpeg)

2. Отметка в чек боксе `Restrict where this project can be run` и указание значения `python` позволяет запускать тесты только там, где установлен Python(данная настройка нужна, только если у вас есть отдельные ноды(агенты) на разных языках программирования и вы хотите запускать тесты на ноде с Python).

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/label_jenkins.jpeg)

3. В блоке `Source Code Management` выбрать `Git`, указываем URL репозитория и ветку.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/git_jenkins.jpeg)

4. В блоке `Build Environment` выбрать `Delete workspace before build starts` (параметры очистки рабочего пространства).
   Это необходимо для того, чтобы перед каждым запуском тестов удалять старые файлы и не допускать их влияния на результаты тестирования.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/delete_workspace_jenkins.jpeg)

5. В блоке `Build Steps` указана команда запуска сборки тестов. Важно отметить, что в примере указано `|| true`, это нужно для того, чтобы джоба не падала при возникновении ошибок в тестах.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/command_jenkins.jpeg)

6. В блоке `Post-build Actions` указываем в разделе `Allure Report` путь до папки, по умолчанию `allure-results`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/allure_jenkins.jpeg)


## Авторизация в Allure TestOps

Для авторизации в Allure TestOps необходимо ввести логин и пароль которые представлены в уроке. Регистрироваться самому НЕ НУЖНО.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/testops_login.jpeg)


## Добавляем Allure TestOps в jenkins джобу

1. Если не нужно отображение результатов прогона в Allure Results, то указываем отметку в чек боксе `Disabled` в разделе `Allure Report`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/allure_jenkins_disabled.jpeg)

2. В блоке `Build Environment` указываем отметку в чек боксе `Allure: upload results`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jenkins_allure_testops.jpeg)

3. В отобразившимся блоке `Allure TestOps` необходимо указать данные, а именно:

   - В строке `Server` в выпадающем списке выбираем `allure-server`
   - В строке `Project` в выпадающем списке выбираем название проекта, который был создан ранее, и к которому можно подключиться через `Allure TestOps`(отображение проекта в данном выпадающем списке описано ниже в разделе [Добавляем отображение проекта Allure TestOps в jenkins джобе](#добавляем-отображение-проекта-allure-testops-в-jenkins-джобе))
   - В строке `Launch Name` оставляем значение по умолчанию `${JOB_NAME} - #${BUILD_NUMBER}`
   - В строке `Launch tags` можно указать теги для прогона (это не обязательно)
   - В блоке `Results` кликаем на кнопку `Add results` и на таб `Results`. В отобразившемся блоке в строке `Path` указываем путь до папки с результатами тестов, по умолчанию `allure-results`.
   
4. Сохраняем изменения(кнопка `Save`). 

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jenkins_allure_testops_2.jpeg)

## Добавляем отображение проекта Allure TestOps в jenkins джобе

1. Создаем проект в Allure TestOps. Для этого переходим в Allure TestOps и авторизируемся
2. На главной странице с `Projects` нажимаем на кнопку `Create new project`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/testops_create_project.jpeg)

3. В отобразившимся попапе заполняем данные:
   - В поле `Name` указываем название проекта
   - В поле `Description` указываем описание проекта (не обязательно)
   - Указываем отметку в чек боксе `Public` если хотим чтобы проект был доступен всем пользователям
   - Нажимаем на кнопку `Submit`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/create_project.jpeg)

4. В созданном проекте нажимаем на иконку шестеренки для перехода в настройки проекта.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/open_project.jpeg)

5. В настройках переходим на таб `Access`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/access_settings.jpeg)

   - В блоке `Outside Collaborators` необходимо кликнуть на иконку `+` 

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/outside_collaborators.jpeg)

   - В отобразившемся попапе `Add collaborator` в выпадающем списке `Select a collaborator to grant permissions to` необходимо выбрать `jenkins_agent_service_acc`. А в выпадающем списке `Permission Set` выбрать `Project Write`.
  
![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_collaborator.jpeg)

   - Нажимаем на кнопку `Submit`

Конечный результат должен выглядеть так:

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/last_result.jpeg)


## Как подключить интеграцию и запуск джобы в Jenkins через Allure TestOps

1. Для того чтобы джобу можно было запускать через Allure TestOps, необходимо в настройках проекта добавить интеграцию с Jenkins.
   - Переходим в настройки проекта на таб `Integrations`.
   - На странице `Integrations` в строке с названием `Jenkins` нажимаем на кнопку `Add integration`.
  
![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/integrations_jenkins.jpg)

   - В отобразившемся попапе `Add Jenkins integration to project` заполняем данные:
     - В строке `Username` указываем юзернейм пользователя Jenkins
     - В строке `API token` указываем токен к аккаунту Jenkins
     - Нажимаем на кнопку `Test connection` и проверяем что все данные введены верно. Если всё верно указано, то отобразиться сообщение `Connection established`
     - Нажимаем на кнопку `Add integration`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/connection_jenkins_testops.jpg)

После добавления интеграции с Jenkins, в блоке `Added integrations` отобразиться информация о добавленной интеграции.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/added_integration.jpg)

2. После запуска джобы из Jenkins, джоба отобразиться в allure testops. Если необходимо настроить джобу, то нужно перейти в боковом меню на вкладку `Jobs`. 
Если в джобе есть параметризация и дефолтное значение для параметров не отображено в Allure TestOps, то необходимо в строке с джобой нажать на иконку со стрелками `Update job` и после обновления все параметры и их значения будут отображены.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jenkins_testops_job.jpg)

3. Если необходимо вручную добавить джобу в Allure TestOps, то необходимо перейти в боковом меню на вкладку `Jobs` и нажать на кнопку `New job`. 

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_new_job.jpg)

В отобразившемся попапе `Create job` заполняем данные:
   - Кликнув на строку `Build server` выбираем из выпадающего списка адрес школьного сервера. 
   - Далее отображается дополнительное поле `Job`, и чек бокс `Can run tests`. Если необходимо запускать джобу через Allure TestOps, то необходимо отметить чек бокс `Can run tests`.
   - В строке `Job` кликаем на поле и из выпадающего списка ищем нужную джобу (данные в списке можно отфильтровать указав название джобы в строке поиска).
   - После добавления джобы отображается кнопка `Add parameter`, по клику на которую можно добавить параметры для джобы.
   - Нажимаем на кнопку `Submit`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/add_job.jpg)

После сохранения, джоба отобразится в списке джоб в Allure TestOps в блоке `Jobs`.

### Как узнать свой Username в Jenkins

Для того чтобы узнать свой `Username` необходимо перейти в Jenkins.
 - Для отображения `Username` необходимо кликнуть в верхнем правом углу на свой профиль.
 - На вкладке `Status` можно увидеть `User ID`, это и есть ваш `Username`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/username_jenkins.jpg)

### Как создать API token в Jenkins

Для того чтобы создать свой `API token` необходимо перейти в Jenkins.
 - В боковом меню выбираем `Configure`
 - В блоке `API Token` нажимаем на кнопку `Add new Token`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/api_token.jpg)

 - После, отобразиться поле ввода для ввода названия токена(имя может быть любым) и кнопка `Generate`. Вводим название токена и нажимаем на кнопку `Generate`.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/api_create_token.jpg)

 - Далее отобразиться токен, который необходимо скопировать и вставить в поле `API token` в Allure TestOps.
  
![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/token_number.jpg)

  
## Как подключить интеграцию с Jira

1. Для того чтобы добавить интеграцию с Jira, необходимо:
   - Переходим в настройки проекта на таб `Integrations`.
   - На странице `Integrations` в строке с названием школьной `Jira` нажимаем на кнопку `Add integration`.
  
![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jira_integration.jpg)

   - В отобразившемся попапе `Add jira integration to project` заполняем данные:
     - В строке `Username` указываем юзернейм пользователя Jira (данные отображены в уроке)
     - В строке `Password` указываем пароль к аккаунту Jira (данные отображены в уроке)
     - Нажимаем на кнопку `Test connection` и проверяем что все данные введены верно. Если всё верно указано, то отобразиться сообщение `Connection established`
     - Нажимаем на кнопку `Add integration`

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/jira_connect.jpg)

После добавления интеграции с Jira, в блоке `Added integrations` отобразиться информация о добавленной интеграции.

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/python/allure-py/added_integration_jira.jpeg)






## Живая документация
Allure TestOps позволяет собирать в одном месте тест-кейсы, к которым могут иметь доступ все члены команды. Это позволяет экономить время и не отвлекаться от разработки тестов, так как каждый может посмотреть покрытие и сценарий каждого теста.

Интерфейс «живой документации»:

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/allure/allure-3.png)

## Автоматизация
Обычно тестирование начинается с ручных тестировщиков, которые погружаются в архитектуру, изучают её и пишут тест-кейсы. После этого приходят автоматизаторы, которые по готовым сценариям пишут автоматические тесты. Allure TestOps позволяет автоматически переносить сценарии тестирования в код и после этого их можно дополнять кодом.

## Запуск тестов
Allure TestOps позволяет из интерфейса запускать автоматические тесты и смотреть результат их выполнения. При этом можно выбирать какие именно тесты запускать. Также к системе имеют доступ все члены команды, которые для своих нужд могут пользоваться тестами.

## Разбор отчётов
Часто бывает такое, что после релиза автотестов, некоторые из них могут содержать ошибки. Члены команды, которые запускают их, будут видеть эти ошибки до тех пор, пока их не исправят. В Allure TestOps позволяет отслеживать дефекты и добавлять к ним комментарии. После этого все будут видеть понятное сообщение об ошибке, а не данные из консоли.
