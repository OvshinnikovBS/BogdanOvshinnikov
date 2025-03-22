# BogdanOvshinnikov К-ИСП-39-1

![Без имени](https://github.com/user-attachments/assets/58e2fc47-9866-4cae-b409-433423a098ef)

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

* -d - это флаг, который запускает контейнеры в фоновом режиме. После выполнения команды терминал останется доступным для других задач, а контейнеры будут работать независимо.  Без `-d` команда будет выводить логи в консоль, и терминал будет заблокирован до тех пор, пока сервисы работают.

![рис 24](https://github.com/user-attachments/assets/da266533-2e04-4822-ab14-c87aed6ce8f8)

![рис 25](https://github.com/user-attachments/assets/32826b16-11c2-4d3a-a817-065c38e6a70f)

19. Команда останавливает запущенные контейнеры без их удаления.

Команда:`sudo docker compose stop`

![изображение](https://github.com/user-attachments/assets/22a478f8-17a8-4df8-8d66-d91d865fb7bc)

20. Используемая команда для остановки и удаления контейнеров, сетей и томов, определенных в файле docker-compose.yml.

Команда:`sudo docker compose down`

![изображение](https://github.com/user-attachments/assets/24a9810c-a45e-4a48-a4c8-29caae288fbf)

21. Команда показывает информацию о контейнерах, управляемых Docker Compose, определенных в файле docker-compose.yml.

Команда:`sudo docker compose ps`

![изображение](https://github.com/user-attachments/assets/2445f67b-054c-4de4-96ad-e3c37f8ebe17)



22. Команда выводит на экран абсолютный путь к текущей рабочей директории.

Команда:`pwd`

![изображение](https://github.com/user-attachments/assets/9989c873-a2a1-49d4-9610-6e6ec4826aa7)


23. При помощи этой команды происходит комирование репрозитория с Github. Также была использована команда ls для просмотра файлов в папке.

Команда:`sudo git clone https://github.com/OvshinnikovBS/BogdanOvshinnikov`

![изображение](https://github.com/user-attachments/assets/466697e8-27ef-4f60-8123-3c9a0c484b24)


Команда:`ls`

![изображение](https://github.com/user-attachments/assets/d88975fc-0615-46cb-a5dd-4cdc4081aa87)

24. Команда предназначена для открытия или создания файла docker-compose.yaml в текстовом редакторе vi с правами суперпользователя (root).

Команда:`sudo vi docker-compose.yaml`

![изображение](https://github.com/user-attachments/assets/e38d7d79-54a1-49b5-913b-62f4e508ceba)


![изображение](https://github.com/user-attachments/assets/8eaf990d-f22a-456e-a556-c878f2b06acf)

![изображение](https://github.com/user-attachments/assets/1bb37458-22e6-4fc3-961a-cd3129d77966)

![изображение](https://github.com/user-attachments/assets/bc76ec91-5e8d-485d-83fd-ea7d8018d4fb)

![изображение](https://github.com/user-attachments/assets/355e279f-1d96-4b18-becb-d20d099e48b6)

25. Команда также используется для открытия или создания файла с именем prometheus.yaml в текстовом редакторе vi с правами суперпользователя (root).

Команда:`sudo vi prometeus.yaml`

![изображение](https://github.com/user-attachments/assets/0729b9b4-7c99-4dbf-8432-1d89ac95210f)


![изображение](https://github.com/user-attachments/assets/968019af-b185-40aa-9806-49b6b032e185)


# Grafana

1. Переходим на сайт: `localhost:3000` 
2. Вводим user & password: `admin`

![422935761-d29cf7a6-17e6-4dec-8ec9-4bab9042a95a](https://github.com/user-attachments/assets/c03fb91f-c890-4a53-b2ea-a02787e2032b)

3. Зайдя на сайт выбирается `Dashboards` для создания Dashboard

![423066991-e1e23bea-22d9-49e7-85e4-8c77d4e4bba0](https://github.com/user-attachments/assets/c552ade2-c990-4581-847d-9aa89255b6d2)

4. Следующий шаг: нажимаем `+Add visualization`, после `Configure a new data source` и выбирается `Prometheus`

![422938456-3a1c545e-dd4f-4b31-9104-4b01e0021932](https://github.com/user-attachments/assets/2748d3b5-8b8c-4276-b2a4-c64ffe55dad8)

![изображение](https://github.com/user-attachments/assets/f667d885-45d9-4500-9e72-6efa16cd3fbb)

![422938923-16011d77-5f71-4432-81b9-831c8fe6c8ec](https://github.com/user-attachments/assets/438e806c-0d59-4d54-bc87-107a5907a9fa)

5. Настройка: Connection: http://prometheus:9090 Authentication: `Basic authentication`

![изображение](https://github.com/user-attachments/assets/f3b52d45-f21c-42b0-beae-12da9a5499a2)

![422939674-d06d4bb1-31b7-4134-96da-1ad69f3f585f](https://github.com/user-attachments/assets/ec9dabfd-328f-46a4-aadc-b4f7b3ba46bc)

6. В завершении `Save & test`

![422939795-967a704c-572d-42ae-b128-5ae825ec659b](https://github.com/user-attachments/assets/5cd04a2f-8143-4f6f-bbc1-e70a78c4d663)

7. Далее, при помощи `Import dashboard` созданный Dashboard импортируется.

8. В строке `Find and import dashboards for common applications at grafana.com/dashboards` пишем `1860`

![422945491-167d4d85-c661-4a78-a389-a11474759266](https://github.com/user-attachments/assets/9587999c-17cb-4342-bbf9-bbbdbbc2d0ea)

9. В конце `Select Prometheus` и `Import`.

![422946716-16f0b5c2-882f-4871-be5a-0bae49f5d6eb](https://github.com/user-attachments/assets/91576945-7f79-45d4-8000-926229c4a27e)

10. Получаем следующий результат

![изображение](https://github.com/user-attachments/assets/e8c695c6-95e3-49fa-aa79-673fb0db6fd7)


# VictoriaMetrics

1. Victoria Metrics создаем также как и Prometheus только меняем URl на `http://victoriametrics:8428` и ставим `No autentification`

![423075451-7f13072f-8373-413f-822c-8275cc5dfc28](https://github.com/user-attachments/assets/a6d8a73e-5c51-48a4-a4a5-2fd8f458a291)

2. Возращаемся на пару шагов назад и выбираем имя которое мы указали

![423075613-172aaf23-fff5-40e5-a016-a6de9d27e692](https://github.com/user-attachments/assets/50c3c4b1-8956-4c63-b743-64d9069f8a65)

3. Выбираем `Victoriametrics` и смоотрим результат

![изображение](https://github.com/user-attachments/assets/216d0421-c242-43d3-a8a3-785afa671844)

![423076235-679cca14-baa7-4824-bbc7-b038fede758f](https://github.com/user-attachments/assets/7933541b-bc5f-49a6-a9f6-540e3c4e68f0)

4. Далее вводим следующую команду
    
Команда: `echo -e "# TYPE light_metric1 gauge\nlight_metric1 0" | curl --data-binary @- http://localhost:8428/api/v1/import/prometheus`

![423076893-cd0eab69-20d3-48a5-9c0a-f4c2d3299932](https://github.com/user-attachments/assets/84d11d15-d7e1-4595-afed-58164b705bc9)

5. Потом переходим на Victoria metrics и выбираем `vmui`

![423078324-6ae580bd-68fb-48b9-a026-509f6bb8886d](https://github.com/user-attachments/assets/a1948d14-f998-44de-904d-40fb23956f8c)

6. Вводим в строку `light_metric1`

![423077682-b64cf07c-4ddd-4a38-be4c-3903b115f646](https://github.com/user-attachments/assets/e1c898db-7e57-4cd6-94be-dcebf70da975)

7. Переходим обратно в Grafana и вставляем в строку `light_metric1` и нажимаем `Run queries`

![423078230-51a9f8e8-4f5f-4154-b835-732169efdde8](https://github.com/user-attachments/assets/abd2a40a-5c10-4910-b6f8-ae82e6107c4f)








