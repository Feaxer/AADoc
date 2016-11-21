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

