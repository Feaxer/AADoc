# ActiveAdmin докуметация

## Установка

ActiveAdmin является гемом для Ruby.

```
gem 'activeadmin'

# Plus integrations with:
gem 'devise'
gem 'cancan' # or cancancan
gem 'draper'
gem 'pundit'
```

Точнее, это [Rails Engine](http://guides.rubyonrails.org/engines.html), который может быть внедрен в уже существующее Ruby on Rails приложение

### Настройка Active Admin

После установки гема, вам нужно запустить генератор. Вот варианты:

- Если вы не хотите использовать Devise, запустите генератор с параметром ```--skip-users```

	```rails g active_admin:install --skip-users```
	
- Если вы хотите использовать существующий класс пользователя, тогда укажите его в параметре:

	```rails g active_admin:install User```

- Если же вызвать генератор без параметров, тогда будет создан класс AdminUser для использования вместе с гемом Devise

	```rails g active_admin:install```

Генератор создаст эти файлы:
```
app/admin/dashboard.rb
app/assets/javascripts/active_admin.js.coffee
app/assets/stylesheets/active_admin.scss
config/initializers/active_admin.rb
```
Теперь запустите миграции и заполнение вашей базы данных, после чего запустите сервер:
```
rake db:migrate
rake db:seed
rails server
```
Перейдите по ссылке ```http://localhost:3000/admin``` и авторизуйтесь по следующим данным:

* **Пользователь**: admin@example.com
* **Пароль**: password

Вуаля! Вы находитесь в вашей новосозданной Active Admin  панели.

Чтобы зарегистрировать существующую модель в Active Admin введите в терминале:
```
rails g active_admin:resource MyModel
```
Это создаст файл ```app/admin/my_model.rb``` для настройки интерфейса. Обновите страницу в браузере, чтобы увидеть его.

## Обновление

Когда обновляете Active Admin до новой версии, советуем посмотреть [CHANGELOG](https://github.com/activeadmin/activeadmin/blob/master/CHANGELOG.md).
Чтобы обновить JS и CSS ассеты используйте команду:
```
rails g active_admin:assets
```
Также вам нужно синхронизировать свои файлы с исходниками из новой версии:

* app/admin/dashboard.rb [~>](https://github.com/activeadmin/activeadmin/blob/master/lib/generators/active_admin/install/templates/dashboard.rb)
* config/initializers/active_admin.rb [~>](https://github.com/activeadmin/activeadmin/blob/master/lib/generators/active_admin/install/templates/active_admin.rb.erb)

## Совместимость с гемами

### will_paginate

Если вы используете ```will_paginate``  в своем приложении, вам нужно настроить инициализатор для Kaminari для избежания конфликтов.

```
# config/initializers/kaminari.rb
Kaminari.configure do |config|
  config.page_method_name = :per_page_kaminari
end
```

Если вы также используете [Draper](), возможно вы захотите убедиться, что ```per_page_kaminari``` передан правильно:

```
Draper::CollectionDecorator.send :delegate, :per_page_kaminari
```

### simple_form

Если вы получаете ошибку ```wrong number of arguments (6 for 4..5)```,  посмотрите [issue #2703](https://github.com/activeadmin/activeadmin/issues/2703#issuecomment-38140864).