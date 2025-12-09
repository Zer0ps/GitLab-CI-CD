# Настройка GitLab Runner-сервера

Документ описывает, как подготовить сервер `GitLab-Runner` с Docker и зарегистрировать раннер в GitLab-проекте.

## 1. Установка Docker

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable --now docker
sudo usermod -aG docker $USER
newgrp docker
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
- **Описание**: `flask-runner-local` (или любое удобное имя)
- **Executor**: `docker`
- **Docker image**: `python:3.12`

Проверьте, что раннер активен:

```bash
sudo gitlab-runner list
```
