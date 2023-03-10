<h1 align="center">⚙️ Example readme for docker-app start ⚙️</h1>

### Оглавление:
- [Подготовка docker 🔨](#подготовка-docker-)
  - [Запуск iptables](#запуск-iptables)
  - [Настройка iptables](#настройка-iptables)
  - [Установка docker](#установка-docker)
  - [Настройка прав docker](#настройка-прав-docker)
- [Запуск приложения ▶️](#запуск-приложения-▶️)

## Подготовка docker 🔨

Для работы докера необходимо:
 - Что бы у Вас был включен iptables;
 - Настройка iptables;
 - Установлен docker и Docker Compose;
 - Настроены правильные права для docker, что бы осуществлять запуск контейнеров не из под рута https://docs.docker.com/engine/install/linux-postinstall/.

### Запуск iptables:
На дистрибьютивах debian обычно iptables установлен и включен по умолчанию. Поэтому дополнительных действий выполнять для debian не нужно. 

### Настройка iptables:
Докер сам умеет пробрасывать порты через iptables и об этом стоит помнить. В нашем приложении все проброшенные порты должны смотреть в интернет, поэтому нет необходимости выполнять дополнительные настройки. Но рекомендую ознакомится с этим гайдом на будущее: https://codepoetry.ru/post/docker-user-iptables/

### Установка docker:
Раздел можно пропустить, если докер уже установлен. Далее следую команды из официальной документации https://docs.docker.com/engine/install/debian/ В случае возникновения проблем нужно будет ознакомится с ней.
Обновите apt-get:
```bash
sudo apt-get update
```
```bash
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
Добавьте официальный GPG-ключ Docker:
```bash
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
Настройте репозиторий
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Обновите apt-get (Снова):
```bash
sudo apt-get update
```
Установите сам докер:
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Запустите докер контейнер, что бы убедится в успешной установке
```bash
sudo docker run hello-world
```

### Настройка прав docker:
Необходимо для запуска докера без sudo
Далее следую команды из официальной документации https://docs.docker.com/engine/install/linux-postinstall/ В случае возникновения проблем нужно будет ознакомится с ней.

Создайте docker группу.
```bash
sudo groupadd docker
```
Добавьте пользователя в docker группу.
```bash
sudo usermod -aG docker $USER
```
Выйдите из системы и войдите снова, чтобы новые права вступили в силу.
Убедитесь, что вы можете запускать docker команды без sudo.
```bash
docker run hello-world
```


## Запуск приложения ▶️
Скачиваем проект на машину
```bash
git clone git@github.com:overload127/example_readme_docker.git
```
Переходим в папку проекта
```bash
cd example_readme_docker
```
Запускаем сборку проекта в режиме демона с автоматическим запуском
```bash
docker-compose -f ./docker-compose-prod.yaml up -d
```
