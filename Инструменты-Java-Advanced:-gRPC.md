# gRPC

![](https://raw.githubusercontent.com/qa-guru/knowledge-base/main/img/tools-java-plus/gRPC/grpc-banner.jpg)

gRPC - это высокопроизводительный открытый фреймворк, разработанный Google, для создания распределенных систем на основе протокола HTTP/2. Он использует Protocol Buffers - компактный и быстрый способ сериализации структурированных данных, позволяя легко и эффективно обмениваться сообщениями между клиентом и сервером. gRPC также поддерживает множество языков программирования, в том числе Java, что делает его очень гибким и удобным для создания многоплатформенных приложений.

gRPC позволяет быстро и эффективно создавать клиент-серверные приложения, обеспечивая надежность и безопасность передаваемых данных. Он использует протокол HTTP/2, который поддерживает множество возможностей, таких как мультиплексирование, стриминг и сжатие данных, что делает его значительно быстрее, чем стандартный HTTP/1.1. Кроме того, gRPC предоставляет гибкую систему интерсепторов, которые позволяют добавлять дополнительную логику и функциональность к вашим сервисам. В Java для работы с gRPC можно использовать библиотеку grpc-java.

[Сайт проекта](https://grpc.io)

## Установка
Для установки библиотеки grpc-java в файле `build.gradle` необходимо указать следующую зависимость:

```gradle
plugins {
    id 'java'
}

dependencies {
    implementation 'io.grpc:grpc-netty-shaded:1.54.0'
    implementation 'io.grpc:grpc-protobuf:1.54.0'
    implementation 'io.grpc:grpc-stub:1.54.0'
}
```

Актуальную версию grpc-java можно узнать на сайте [MVN Repository](https://mvnrepository.com/artifact/io.grpc?p=1).
