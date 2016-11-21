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
