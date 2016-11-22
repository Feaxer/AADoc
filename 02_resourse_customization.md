Работа с ресурсами
=======

Каждый ресурс в Active Admin соответствует Rails модели. Поэтому прежде чем создавать ресурс в Active Admin, сначала нужно создать модель в Rails.

Создание ресурса
--------

Базовой командой для создания ресурса является ```rails g active_admin:resourse Post``` . Генератор создаст ```app/admin/post.rb`` файл следующего содержания:

```
ActiveAdmin.register Post do
  # everything happens here :D
end
```

Настройка strong parameters
------

```attr_accessible`` в Rails 4  был заменен strong parameters, который перемещает атрибут в белый список из модели в контроллер.

Используйте метод ```permit_params``` чтобы определить, какие атрибуты могут быть изменены:


	ActiveAdmin.register Post do
	  permit_params :title, :content, :publisher_id
	end

Для любого поля формы, которое отправляет множественное значение