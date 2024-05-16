# Лаба №6. gRPC(Windows)
-----
## Необходимые инструменты
-----
Для реализации этой лабы будет необходимо установить 
* [docker](https://docs.docker.com/desktop/install/windows-install/). С этим вам может помочь или [этот](https://www.youtube.com/watch?v=ZyBBv1JmnWQ&ab_channel=TheBinaryBits) видос, или любой другой на просторах ютуба.
* vscode и пара расширений для него(ниже приложу скрин)

### Подробнее про расширения
Основное:
* c/c++ Extension Pack. Как раз для комфортной работы с плюсами. +там сразу докачиваются CMake расширения.
* vscode-proto3. Чтоб было комфортнее работать с прото файлом.

Мб понадобится:
* Docker
* Dev Containers. 
-----
## Ставим себе gRPC
Создаём на компе папку, можно на рабочем столе. Открываем эту папку в vscode и создаём в ней **Dockerfile**.
Записываем в него следующее:
```
FROM ubuntu:latest

RUN apt-get update && apt-get install -y cmake build-essential git

WORKDIR /deps

RUN git clone --recurse-submodules -b v1.62.0 --depth 1 --shallow-submodules https://github.com/grpc/grpc

RUN mkdir -p /deps/grpc/build && cd /deps/grpc/build && \
    cmake -DgRPC_INSTALL=ON \
      -DgRPC_BUILD_TESTS=OFF \
      .. && \
      make -j8 install
```
> Не забываем сохранять файлы при их изменении

Открываем в vscode терминал и вводим `docker build -t .`
Далее начнётся установка. Она может занять около 15-20 минут.
![](https://drive.google.com/drive/folders/1wA3oYeyZstWto-JtYQTQVqhII4GGujDs)


## Ремарки
-----
### Ремарка №1


