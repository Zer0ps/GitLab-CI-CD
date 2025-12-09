# Настройка GitLab CE

Инструкция для первого входа в веб-интерфейс GitLab, сброса пароля root и импорта существующего проекта.

## Первый вход

1. Откройте в браузере `http://192.168.0.50`.
2. Задайте новый пароль для пользователя `root` и войдите под ним.

## Сброс пароля root через консоль (если нужно)

```bash
sudo gitlab-rails console
user = User.find_by_username("root")
user.password = "NewStrongPassword"
user.password_confirmation = "NewStrongPassword"
user.save!
user.confirm
```

## Импорт существующего проекта из GitHub

На сервере с GitLab CE:

```bash
git clone https://github.com/zaharchik372/flask-ci-demo.git
cd flask-ci-demo
git remote remove origin
```

Создайте пустой проект в GitLab по адресу `http://192.168.0.50/root/flask-ci-demo`, затем привяжите репозиторий к новому origin и отправьте код:

```bash
git remote add origin http://192.168.0.50/root/flask-ci-demo.git
git push -u origin main
```
