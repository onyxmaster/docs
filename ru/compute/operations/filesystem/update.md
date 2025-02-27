# Изменить файловое хранилище

После создания файлового хранилища вы можете изменить его имя, описание и размер.

{% list tabs %}

- Консоль управления

  1. В [консоли управления]({{ link-console-main }}) выберите каталог, в котором находится файловое хранилище.
  1. Выберите сервис **{{ compute-name }}**.
  1. На панели слева выберите ![image](../../../_assets/compute/storage.svg) **Файловые хранилища**.
  1. В строке нужного файлового хранилище нажмите ![image](../../../_assets/options-grey.svg) и выберите пункт **Редактировать**.
  1. Измените параметры файлового хранилища: например, переименуйте его, отредактировав поле **Имя**.
  1. Нажмите кнопку **Сохранить**.
  
- API
   
  Используйте метод [FilesystemService/Update](../../api-ref/grpc/filesystem_service.md#Update) gRPC API или метод [update](../../api-ref/Filesystem/update.md) ресурса Filesystem REST API.
  
{% endlist %}