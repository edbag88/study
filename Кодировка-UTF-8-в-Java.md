Что нужно сделать, чтобы не было проблем с кодировкой UTF-8 и отображением непонятных символов:
1. В IDE в верхней панели меню нажать `Help -> Edit Custom VP Options` и добавить в конец текста две строчки:  
```
-Dconsole.encoding=UTF-8
-Dfile.encoding=UTF-8
```

2. Далее в IDE зайти в меню `File -> Settings -> Editor -> File Encodings`:
в верхних двух полях должно стоять `UTF-8`, в самой нижней – `with NO BOM`. Далее следует сохранить изменения;

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/utf8_1.jpg)

3. В файл  `build.gradle` после блока с репозиторием добавить блок:
```groovy
compileJava {
    options.encoding = 'UTF-8'
}
compileTestJava {
    options.encoding = 'UTF-8'
}
```
> **Примечание:** Строка и блок кода `compileJava` относится к коду и выводу в терминал из папки `main -> Java`, а блок кода `compileTestJava` к коду `test -> Java`. 

4. Обновить Gradle после внесенных изменений;
5. Перезапустить IDE (полностью выйти из нее и зайти заново).   

Всё, теперь можно запускать код, всё должно корректно отображаться.
