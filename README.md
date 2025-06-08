# Jenkins-practise на Ubuntu

В этом проекте демонстрируется начальная работа с Jenkins
---

## Устанавливаю необходимые плагины. В данном случае "Credentials"

Credentials в Jenkins — это безопасные данные, хранящиеся в среде Jenkins и облегчающие процессы аутентификации и авторизации, необходимые для автоматизации рабочих процессов. В них содержатся конфиденциальные данные, такие как имена пользователей, пароли, ключи API и SSH. Они адаптированы под различные требования к аутентификации. Credentials в Jenkins обеспечивают защиту конфиденциальной информации во время выполнения конвейеров, повышая общую безопасность и надёжность процессов непрерывной интеграции и развёртывания

--- 
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/5d387d6ba53050b91c462566ef16dc4b740af82e/img/1.png" alt="Header">
</p>
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/5d387d6ba53050b91c462566ef16dc4b740af82e/img/2.png" alt="Header">
</p>

<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/87c6a35dd2bcc8974594611ca71955f6dae73505/img/3.png" alt="Header">
</p>

Показываю все установленные плагины:

```bash
cd /var/lib/jenkins/plugins
ls
```
## Простейшие Jobs включая Deployment

Собрался сделать проект, который будет себя включать 2 deployment job. Они абсолютно одинаковые. У нас есть два web-сервера, они будут называться: WebServer-Test, а другой WebServer-Prod. То есть мы сначала будем делать деплоймент на тест и если всё хорошо, тогда будем и на второй. Сервера буду поднимать на виртуальной машине, linux локально (не aws, амазон).    1) Job-Deploy to TEST - в начале будем собирать, билдить маленькие web-странички, протестируем и сделаем деплоймент на web-сервер. 2) Job-Deploy to PROD - делает всё то же самое, просто отправляет наш файлик на другой сервер. Сейчас я оставлю здесь свои первые наброски своего начинания в Jenkins, а уже позже сделаем проект:

<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/86b373b4fd998480ac4c1c18136730d19367a181/img/4.png" alt="Header">
</p>
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/86b373b4fd998480ac4c1c18136730d19367a181/img/5.png" alt="Header">
</p>
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/86b373b4fd998480ac4c1c18136730d19367a181/img/6.png" alt="Header">
</p>
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/86b373b4fd998480ac4c1c18136730d19367a181/img/7.png" alt="Header">
</p>
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/86b373b4fd998480ac4c1c18136730d19367a181/img/8.png" alt="Header">
</p>
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/86b373b4fd998480ac4c1c18136730d19367a181/img/9.png" alt="Header">
</p>

После этого я пробовал изменить и использовать переменную окружения:

<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/86b373b4fd998480ac4c1c18136730d19367a181/img/10.png" alt="Header">
</p>
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/86b373b4fd998480ac4c1c18136730d19367a181/img/11.png" alt="Header">
</p>

Build Number (номер сборки) — это уникальный идентификатор, который Jenkins автоматически присваивает каждой запущенной сборке (Job/Build). Это числовое значение, которое увеличивается на +1 с каждым новым запуском задачи.

```bash
echo "Hello-world!"
echo "This is my Build Number $BUILD_NUMBER"
```
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/86b373b4fd998480ac4c1c18136730d19367a181/img/12.png" alt="Header">
</p>
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/86b373b4fd998480ac4c1c18136730d19367a181/img/13.png" alt="Header">
</p>

Изменим нашу консоль (эксперементирую). Допустим, sleep 5 - приостанавливает выполнение скрипта на 5 секунд (имитация долгой задачи, например, ожидания сервера)

```bash
echo "Hello-world!"
echo "This is my Build Number $BUILD_NUMBER"
pwd
sleep 5
whoami
```

<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/aae2b115276118ace8cbb73d2f1e45b6a17c35de/img/15.png" alt="Header">
</p>

На скриншоте видно, что у нас пока что одна Job 'MyJobNumber1'

```bash
cd /var/lib/jenkins/workspace/
ll
```
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/aae2b115276118ace8cbb73d2f1e45b6a17c35de/img/16.png" alt="Header">
</p>

На скриншоте можно увидеть количество сборок

```bash
cd  /var/lib/jenkins/jobs/MyJobNumber1
ll
cd builds
ll
```

<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/aae2b115276118ace8cbb73d2f1e45b6a17c35de/img/17.png" alt="Header">
</p>

Можно в настройках поставить функцию удаления сборок и ограничить до 5 по количеству

<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/aae2b115276118ace8cbb73d2f1e45b6a17c35de/img/18.png" alt="Header">
</p>

Сделаем сборку ещё раз и увидим, что сохраняет последние 5

## Приступаю к работе

<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/d59c9fbc31b8aae437285b566326fd6f4a831bdd/img/19.png" alt="Header">
</p>
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/d59c9fbc31b8aae437285b566326fd6f4a831bdd/img/20.png" alt="Header">
</p>

Создаём Deploy-to-TEST

<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/d59c9fbc31b8aae437285b566326fd6f4a831bdd/img/21.png" alt="Header">
</p>
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/d59c9fbc31b8aae437285b566326fd6f4a831bdd/img/22.png" alt="Header">
</p>

Сгенерировал свою Web-страничку index.html. Что он делает? Создаёт файл index.html, обычная страничка, которая пишет “Hello from Exeleron-IT” желтыми буковками и голубыми буквами “www.exeleron-it.net”. В общем самый простой билд. EOF (End Of File) — это маркер, используемый в heredoc (Here Document) — специальной конструкции в shell-скриптах для передачи многострочного текста в команду или файл. В нашем скрипте он применяется для создания HTML-файла

```bash
echo "---------------Build Started-----------------"
cat <<EOF> index.html
<html>
<body bgcolor=black>
<center>
<h2><font color=yellow>Hello from Exeleron-IT</font></h2>

<font color=blue>www.exeleron-it.net</font>

</center>
</body>
</html>
EOF

echo "---------------Build Started-----------------"
```

<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/37f203f34d1d6cb8b9910bf68da40b62696cbe50/img/23.png" alt="Header">
</p>

Теперь как мы это протестируем? Мы просто будем искать слово “Hello” в нашем файле. Если один раз есть в файле, то тест прошёл, если меньше или больше, то не прошёл. Можно по желанию добавить любые свои проверки для теста, но суть не меняется.

```bash
echo "-------------Test Started-------------------"
result=`grep "Hello" index.html | wc-l`
echo $result
  if [ "$result" = "1" ]
  then
    echo "Test Passed"
  else
    echo "Test Failed"
    exit 1
fi
echo "-----------Test Finished--------------------"
```
<p align="center">
  <img src="https://github.com/exeleron07/jenkins-practice/blob/37f203f34d1d6cb8b9910bf68da40b62696cbe50/img/24.png" alt="Header">
</p>

Тест прошёл успешно. Deploy to prod проходит аналогично, но на данный момент в России наблюдаются ограничения и из-за этого я не могу использовать AWS. Решением выступает использовать Yandex Cloud





