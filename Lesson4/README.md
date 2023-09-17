# Урок 4. Dockerfile и слои
1. Создадим директорию, где будем создавать Dockerfile

    ``sudo mkdir /homework4``
2. Создадим Dockerfile и зайдем в него

    ``sudo nano /homework4/Dockerfile``
3. Редактируем Dockerfile
![image1](image1.png)
4. Код который помещен в контенер.
![image2](image2.png)
5. Собираем контейнер

    ``docker build -t myjava .``
6. Запускаем контейнер

    ``docker run -i myjava``

![image3](image3.png)
