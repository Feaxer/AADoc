# Настройка  Active Admin

Вы можете изменить настройки Active Admin в файле ```config/initializers/active_admin.rb```

## Аутентификация

Active Admin требует два параметра для аутентификации и использования текущего пользователя в вашем приложении.

* Метод контроллера, используемый для принудительной аутентификации

	```configuration.authentification_method = :authentificate_admin_user```

* Метод, используемый для доступа к текущему пользователю

```configuration.current_user_method = :current_admin_user```

Эти оба параметра могут быть установлены в false, чтобы выключить аутентификацию.

```
config.authentication_method = false
config.current_user_method   = false
```

## Параметр "Site title"

Каждая страница имеет, что называется, "site title" в левой стороне верхнего меню (имеется ввиду логотип админки). Если вы хотите,  можете кастомизировать его:

```
config.site_title       = "My Admin Site"
config.site_title_link  = "/"
config.site_title_image = "site_image.png"
config.site_title_image = "http://www.google.com/images/logos/google_logo_41.png"
config.site_title_image = ->(context) { context.current_user.company.logo_url }
```

## Интернационализация (I18n)

Для перевода Active Admin на новый язык или для изменения существующего, вы можете скопировать ```config/locales/en.yml```  в одноименную папку в вашем приложении и изменить его.

## Формат локализации даты и времени

В Active Admin по-умолчанию установлен формат ```:long``` для даты и времени. Если хотите, можете изменить его:

```
config.localize_format = :short
```

## Пространства имен

При регистрации ресурсов в Active Admin они загружаются в пространство имен. Пространство имен по-умолчанию: "admin".

```
# app/admin/posts.rb
ActiveAdmin.register Post do
  # ...
end
```

 Ресурс "Post" будет загружен в пространство имен "admin" и будет доступен по ```/admin/posts```.  Каждое пространство имен имеет свои настройки, наследующиеся из конфигурации приложения.

Например, если у вас есть два пространства имен (:admin и :super_admin) и вы хотите установить разный "site title" для каждого из них, то вы можете использовать ```config.namespace(name)```  блок в файле инициализации, чтобы настроить их по-отдельности.

```
ActiveAdmin.setup do |config|
  config.site_title = "My Default Site Title"

  config.namespace :admin do |admin|
    admin.site_title = "Admin Site"
  end

  config.namespace :super_admin do |super_admin|
    super_admin.site_title = "Super Admin Site"
  end
end
```

Каждый параметр, доступный для настройки в блоке конфигурации Active Admin, доступен и для каждого пространства имен.

##  Пути загрузки

По-умолчанию файлы Active Admin находятся в ```app/admin/```. Вы можете изменить этот путь в файле инициализации:

    ActiveAdmin.setup do |config|
      config.load_paths = [File.join(Rails.root, "app", "ui")]
    end
   

Комментарии
-----------

Изначально Active Admin включает комментарии для ресурсов. Иногда, это не нужно. Чтобы отключить комментарии:

    # For the entire application:
    ActiveAdmin.setup do |config|
      config.comments = false
    end
    
    # For a namespace:
    ActiveAdmin.setup do |config|
      config.namespace :admin do |admin|
        admin.comments = false
      end
    end
    
    # For a given resource:
    ActiveAdmin.register Post do
      config.comments = false
    end

Вы можете изменить имя, по которым комментарии будут зарегистрированы:

    config.comments_registration_name = 'AdminComment'

Также вы можете изменить порядок и поле сортировки комментариев:

    config.comments_order = 'created_at ASC'

Можете отключить отображение ссылки на главную страницу комментариев в верхнем меню:

    config.comments_menu = false

Для изменения пункта меню комментариев:

    config.comments_menu = { parent: 'Admin', priority: 1 }