# Настройка GitLab Runner-сервера

Подготовьте сервер `GitLab-Runner` с Docker и зарегистрируйте раннер в проекте GitLab.

## 1. Установка Docker
```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable --now docker
sudo usermod -aG docker $USER
newgrp docker
```
Проверьте, что Docker доступен без sudo:
```bash
docker info
```

## 2. Установка GitLab Runner
```bash
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh | sudo bash
sudo apt install -y gitlab-runner
```

## 3. Регистрация раннера
Запустите регистрацию и ответьте на вопросы:
```bash
sudo gitlab-runner register
```
- **URL**: `http://192.168.0.50`
- **Token**: токен проекта из **Settings → CI/CD → Runners**
- **Description**: `flask-runner-local`
- **Tags**: `docker`
- **Executor**: `docker`
- **Default Docker image**: `python:3.12`

Проверьте статус:
```bash
sudo gitlab-runner list
sudo gitlab-runner verify
```

Если требуется автообновление runner, включите службу:
```bash
sudo systemctl enable --now gitlab-runner
```
