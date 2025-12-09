# Настройка GitLab CE

Инструкция для первого входа в веб-интерфейс, восстановления пароля и импорта проекта.

## 1. Первый вход в веб-интерфейс
1. Откройте `http://192.168.0.50`.
2. Задайте новый пароль для пользователя `root` и войдите под ним.
3. В разделе **Admin Area → Settings → General** при необходимости проверьте `External URL` и почтовые настройки.

## 2. Сброс пароля root через консоль (опционально)
Если веб-интерфейс недоступен или пароль утерян, выполните:
```bash
sudo gitlab-rails console
user = User.find_by_username("root")
user.password = "NewStrongPassword"
user.password_confirmation = "NewStrongPassword"
user.save!
user.confirm
```

## 3. Импорт существующего проекта
Работайте на сервере `GitLab-Server`:
```bash
git clone https://github.com/zaharchik372/flask-ci-demo.git
cd flask-ci-demo
git remote remove origin
```

Создайте пустой проект в GitLab: `http://192.168.0.50/root/flask-ci-demo`.

Привяжите репозиторий к новому origin и отправьте код:
```bash
git remote add origin http://192.168.0.50/root/flask-ci-demo.git
git push -u origin main
```

При необходимости создайте токен доступа (**User Settings → Access Tokens**) и используйте его вместо пароля при push через HTTP.
