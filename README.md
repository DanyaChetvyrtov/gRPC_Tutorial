# Лаба №6. gRPC(Windows)
## Необходимые инструменты
Для реализации этой лабы будет необходимо установить 
* [docker](https://docs.docker.com/desktop/install/windows-install/). С этим вам может помочь или [этот](https://www.youtube.com/watch?v=ZyBBv1JmnWQ&ab_channel=TheBinaryBits) видос, или любой другой на просторах ютуба.
* vscode и пара расширений для него(ниже приложу скрин)

### Подробнее про расширения
Основное:
* c/c++ Extension Pack. Как раз для комфортной работы с плюсами. +там сразу докачиваются CMake расширения.
* vscode-proto3. Чтоб было комфортнее работать с прото файлом.

Мб понадобятся:
* Docker
* Dev Containers. 

![Все расширения](https://drive.google.com/uc?export=view&id=1LtVnlYsT1SfW0VEDPCb-S6e30a2GI4GQ)

## Ставим gRPC
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

> _Не забываем сохранять файлы при их изменении_
---

Открываем в vscode терминал и вводим `docker build -t mygrpc .`
Далее начнётся установка, которая может занять около 15-20 минут.
![Процесс установки](https://drive.google.com/uc?export=view&id=1paEmANhL-X77LTC7iiB20NSpGRCJeH1l)

---

После установки пишем в терминале `docker images`. Если у вас в появившейся таблице будет поле с **mygrpc**, то всё гуд и можно двигаться дальше.
  

![Должно быть так](https://drive.google.com/uc?export=view&id=1Mni5R-pJM5R8TsR02aPGoHlALhG7oKI1)

---

Далее жмём на кнопку в левом нижнем углу. Откроется окно, где нужно будет нажать _Attach to Running Container_.
![](https://drive.google.com/uc?export=view&id=10nzekakDi9soY60MLDggxS2o0teuuOhp)

После чего vscode вам предложит выбрать контейнер 
  

![](https://drive.google.com/uc?export=view&id=1UD6DErRfbnuCXz90GxXpdj1G73gK4hOi)
  
После выбора контейнера в редакторе откроется новое окно, возможно сразу в папке root, а возможно в папку нужно будет перейти самому.

![](https://drive.google.com/uc?export=view&id=1yFmXN330cCcIdezdYdIhyBKsRMxKrOjC)
1. Тут можно прописать путь(/root)
2. Тут по-идее должны быть какие-то файлы, как на скрине. Если их нет, то мб что-то было сделано не так(но я не уверен, можете перепроверить правильность своих прошлых шагов или попробовать пойти дальше)

## Ремарки
### Ремарка №1


