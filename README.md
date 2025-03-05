# BogdanOvshinnikov К-ИСП-39-1
Установливаем Linux Oracle на VirtualBox, для этого нужно:

•  Иметь образ Linux;

•  Выделить 4 ядер;

•  Выделать 4096+ МБ оперативы;

•  При установки операционной системы выбраем английский язык.


1. Установка гостевых дополнений
   
![рис 1](https://github.com/user-attachments/assets/f43aed0f-cd3d-4707-8da0-6556894d96de)


2. Установка утилиты wget, которая позволяет скачивания файлы из интернета. ТАкже она очень полезна для автоматизации загрузки файлов, например, скриптами.
  
Команда:`sudo yum install wget`

Возникла ошибка:

![рис 2](https://github.com/user-attachments/assets/59f9a79c-535b-44b5-bfd5-bfb73e4d2154)

Решение:

![рис 3](https://github.com/user-attachments/assets/2878f5a5-7901-4a67-9785-8122c732bfce)

Успешная установка:

![рис 4](https://github.com/user-attachments/assets/ebaf268f-95d1-4270-adfd-5cc058ef2b68)


3. Установка утилиты curl (cURL, Client for URLs), которая нужна для передачи данных с использованием различных сетевых протоколов, таких как HTTP, HTTPS, FTP, и прочих.  Она используется для загрузки файлов из интернета, отправки данных на серверы и выполнения различных сетевых операций. (в данном случае она уже установлена, данной командй выполняется проверка этого)

Команда:`sudo yum install curl`

![рис 5](https://github.com/user-attachments/assets/a68b7174-5a82-4093-ba22-98167aad066b)



4. Используется команда, которая обеспечивает доступ к необходимым пакетам, делая возможным установку (развертывание) и использование возможностей репозиторий Docker для разработки, развертывания и управления приложениями. Без выполнения этого шага установка Docker невозможна.

Команда:`sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

![рис 6](https://github.com/user-attachments/assets/f8d89986-ee4a-4228-b008-6b14c0808a32)


5. Используем команду, которая устанавливает полную экосистему (необходимые компоненты) Docker.

Команда:`sudo yum install docker-ce docker-ce-cli containerd.io`

![рис 7](https://github.com/user-attachments/assets/62755360-da2b-420c-b464-d6d44be036ef)

![рис 8](https://github.com/user-attachments/assets/4f03e6b9-efe6-4817-93f0-427e60ce5a8c)

6. Далее используем команду, которая делает две вещи: включает Docker для автоматического запуска при каждой загрузке системы, а также немедленно запускает службу Docker.

Команда:`sudo systemctl enable docker --now`

![рис 9](https://github.com/user-attachments/assets/1e03f13b-7e62-4402-9518-8be40ee2e2e6)

7. Выполняем команду, которая используется для получения последней версии Docker Compose из репозитория GitHub и сохранения её номера в переменной окружения COMVER.

Команда:`COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

![рис 10](https://github.com/user-attachments/assets/e22d9f53-eaed-4329-95b7-a08a1346f4c4)

8. Запишем команду, которая выполняет загрузку и установку последней версии Docker Compose,  автоматически выбирая подходящий бинарный файл для текущей системы.

Команда:`sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`

![рис 11](https://github.com/user-attachments/assets/4bc29882-4e26-4f76-80fe-442a5e1fac17)

9. Последующая команда предоставляет права на выполнение файлу /usr/bin/docker-compose, а так же выполняется команда, выводящая на экран информацию о версии установленного Docker Compose.

Команда:`sudo chmod +x /usr/bin/docker-compose`

Команда:`docker-compose --version`

![рис 12](https://github.com/user-attachments/assets/4ac5456a-c13f-4896-a32b-7c85edb3628e)

10. Следующим шагом скачиваются все файлы и историю изменений из репозитория git.

Команда:`git clone https://github.com/skl256/grafana_stack_for_docker.git`

![рис 13](https://github.com/user-attachments/assets/e9125995-3e4a-4fb8-b7c3-fd2a2703dfa9)

При выполнении команды выдается ошибка, исправляемая следующей командой, которая позволяет установить пакеты git.

Команда:`sudo yum install git`

![рис 14](https://github.com/user-attachments/assets/626f6655-4e0a-49b9-aab4-8ce963998555)

![рис 15](https://github.com/user-attachments/assets/202f3fd8-e3ce-4a0b-815b-24f0e7646f35)

После этого все осуществляется корректно.

![рис 16](https://github.com/user-attachments/assets/b4b6fd7d-2dfc-4aa6-af8f-f642f67013d0)


11. Далее используется утилита cd (change directory) для смены текущего рабочего каталога в командной строке Linux, после чего выполняется ряд команд.

Команда:`cd grafana_stack_for_docker`

![рис 17](https://github.com/user-attachments/assets/00ed03e0-cc6a-4d8a-a4cc-e2273fc135eb)

12. Эта команда использует утилиту mkdir для создания каталогов (директорий) на файловой системе.

Команда:`sudo mkdir -p /mnt/common_volume/swarm/grafana/config`

![рис 18](https://github.com/user-attachments/assets/7aee427b-4221-4ad2-a8df-2b1f7b0b4c9c)

13. Эта команда использует утилиту mkdir с опцией -p и расширением фигурных скобок (brace expansion) для создания нескольких каталогов в файловой системе.

Команда:`sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}`

![рис 19](https://github.com/user-attachments/assets/4a7e123c-a018-457a-bec8-ba477e566611)


14. Эта команда использует утилиту chown для изменения владельца (owner) и группы (group) файлов и каталогов.

Команда:`sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`

![рис 20](https://github.com/user-attachments/assets/fc6f7b2d-2220-47f9-a169-27917be4564a)

15. Эта команда использует утилиту touch для создания пустого файла.

Команда:`touch /mnt/common_volume/grafana/grafana-config/grafana.ini`

![рис 21](https://github.com/user-attachments/assets/4d39c14f-fa61-4358-a88b-631f9efccc90)

16. Эта команда использует утилиту cp (copy) для копирования файлов.

Команда:`cp config/* /mnt/common_volume/swarm/grafana/config/`

![рис 22](https://github.com/user-attachments/assets/88fe1edf-3e58-4d4a-975e-fafc6876684d)


17. Эта команда использует утилиту mv (move) для переименования файла, обычно приводя имя файла к стандартному или ожидаемому.

Команда:`mv grafana.yaml docker-compose.yaml`

![рис 23](https://github.com/user-attachments/assets/a020b191-af0d-4288-9d5b-40ac09bdc8fa)

18. Эта команда использует docker compose для запуска и управления приложением, определенным в файле docker-compose.yaml. Она позволяет легко разворачивать и управлять сложными Docker-приложениями

Команда:`sudo docker compose up -d`

* -d - Параметр -d в команде docker-compose up означает демонизирование процесса — запуск контейнеров в фоновом режиме.

![рис 24](https://github.com/user-attachments/assets/da266533-2e04-4822-ab14-c87aed6ce8f8)

![рис 25](https://github.com/user-attachments/assets/32826b16-11c2-4d3a-a817-065c38e6a70f)
