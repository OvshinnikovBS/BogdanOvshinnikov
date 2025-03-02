# BogdanOvshinnikov К-ИСП-39-1
Установливаем Linux Oracle на VirtualBox, для этого нужно:

•  Иметь образ Linux;

•  Выделить 4 ядер;

•  Выделать 4096+ МБ оперативы;

•  При установки операционной системы выбраем английский язык.


1. Установка гостевых дополнений
   
![Без имени](https://github.com/user-attachments/assets/f43aed0f-cd3d-4707-8da0-6556894d96de)


2. Установка утилиты wget, которая позволяет скачивания файлы из интернета. ТАкже она очень полезна для автоматизации загрузки файлов, например, скриптами.
  
Команда:`sudo yum install wget`

Возникла ошибка:

![Без имени](https://github.com/user-attachments/assets/59f9a79c-535b-44b5-bfd5-bfb73e4d2154)

Решение:

![Без имени](https://github.com/user-attachments/assets/2878f5a5-7901-4a67-9785-8122c732bfce)

Успешная установка:

![Без имени](https://github.com/user-attachments/assets/ebaf268f-95d1-4270-adfd-5cc058ef2b68)


3. Установка утилиты curl (cURL, Client for URLs), которая нужна для передачи данных с использованием различных сетевых протоколов, таких как HTTP, HTTPS, FTP, и прочих.  Она используется для загрузки файлов из интернета, отправки данных на серверы и выполнения различных сетевых операций. (в данном случае она уже установлена, данной командй выполняется проверка этого)

Команда:`sudo yum install curl`

![Без имени](https://github.com/user-attachments/assets/a68b7174-5a82-4093-ba22-98167aad066b)



4. Используется команда, которая обеспечивает доступ к необходимым пакетам, делая возможным установку (развертывание) и использование возможностей репозиторий Docker для разработки, развертывания и управления приложениями. Без выполнения этого шага установка Docker невозможна.

Команда:`sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

![Без имени](https://github.com/user-attachments/assets/f8d89986-ee4a-4228-b008-6b14c0808a32)


5. Используем команду, которая устанавливает полную экосистему (необходимые компоненты) Docker.

Команда:`sudo yum install docker-ce docker-ce-cli containerd.io`

![Без имени](https://github.com/user-attachments/assets/62755360-da2b-420c-b464-d6d44be036ef)

![Без имени](https://github.com/user-attachments/assets/4f03e6b9-efe6-4817-93f0-427e60ce5a8c)

6. Далее используем команду, которая делает две вещи: включает Docker для автоматического запуска при каждой загрузке системы, а также немедленно запускает службу Docker.

Команда:`sudo systemctl enable docker --now`

![Без имени](https://github.com/user-attachments/assets/1e03f13b-7e62-4402-9518-8be40ee2e2e6)

7. Выполняем команду, которая используется для получения последней версии Docker Compose из репозитория GitHub и сохранения её номера в переменной окружения COMVER.

Команда:`COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

![Без имени](https://github.com/user-attachments/assets/e22d9f53-eaed-4329-95b7-a08a1346f4c4)

8. Запишем команду, которая выполняет загрузку и установку последней версии Docker Compose,  автоматически выбирая подходящий бинарный файл для текущей системы.

Команда:`sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`

![Без имени](https://github.com/user-attachments/assets/4bc29882-4e26-4f76-80fe-442a5e1fac17)

9. Последующая команда предоставляет права на выполнение файлу /usr/bin/docker-compose, а так же выполняется команда, выводящая на экран информацию о версии установленного Docker Compose.

Команда:`sudo chmod +x /usr/bin/docker-compose`

Команда:`docker-compose --version`

![Без имени](https://github.com/user-attachments/assets/4ac5456a-c13f-4896-a32b-7c85edb3628e)

10. Следующим шагом скачиваются все файлы и историю изменений из репозитория git.

Команда:`git clone https://github.com/skl256/grafana_stack_for_docker.git`

![Без имени](https://github.com/user-attachments/assets/e9125995-3e4a-4fb8-b7c3-fd2a2703dfa9)
