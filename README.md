# BogdanOvshinnikov
Установливаем Linux Oracle на VirtualBox, для этого нужно:
•  Иметь образ Linux;
•  Выделить 4 ядер;
•  Выделать 4096+ МБ оперативы;
•  При установки операционной системы выбраем английский язык.



1. Установка гостевых дополнений
![Без имени](https://github.com/user-attachments/assets/f43aed0f-cd3d-4707-8da0-6556894d96de)


2. Далее устанавливаем утилиту wget для скачивания файлов из интернета при помощи команды.
  
`sudo yum install wget`

blob:https://web.telegram.org/767ccb91-2dfa-4fc7-9a5b-c2cdd6bc51c2

3. Следующим шагом является установка утилиты curl (в данном случае она уже установлена, данной командй выполняется проверка этого)

`sudo yum install curl`

4. После этого используется команда, которая добавляет репозиторий Docker в список доступных репозиториев для yum, что позволяет впоследствии установить Docker.

`sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

5. Последующим шагом является использование команды, которая устанавливает необходимые компоненты Docker

`sudo yum install docker-ce docker-ce-cli containerd.io`


6. Далее запускается команда, которая делает две вещи: включает Docker для автоматического запуска при каждой загрузке системы, а также немедленно запускает службу Docker.

`sudo systemctl enable docker --now`


7. После выполнении команды, переменная COMVER будет содержать версию последнего релиза Docker Compose.

`COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`


8. После выполнения следующей команды, исполняемый файл Docker Compose будет доступен для запуска.

`sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`


9. Последующая команда предоставляет права на выполнение файлу /usr/bin/docker-compose, а так же выполняется команда, выводящая на экран информацию о версии установленного Docker Compose.

`sudo chmod +x /usr/bin/docker-compose`
`docker-compose --version`
