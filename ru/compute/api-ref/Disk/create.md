# Метод create
Создает диск в указанном каталоге.
 
Вы можете создать пустой диск или восстановить его из снимка
или образа.
 
## HTTP-запрос
`POST /compute/v1/disks`
 
## Параметры в теле запроса {#body_params}
 
```json 
 {
  "folderId": "string",
  "name": "string",
  "description": "string",
  "labels": "object",
  "typeId": "string",
  "zoneId": "string",
  "size": "string",

  // включает только одно из полей `imageId`, `snapshotId`
  "imageId": "string",
  "snapshotId": "string",
  // конец списка возможных полей

}
```

 
Поле | Описание
--- | ---
folderId | **string**<br><p>Обязательное поле. Идентификатор каталога, в котором создается диск. Чтобы получить идентификатор каталога, используйте запрос <a href="/docs/resource-manager/api-ref/Folder/list">list</a>.</p> <p>Максимальная длина — 50 символов.</p> 
name | **string**<br><p>Имя диска.</p> <p>Значение должно быть длиной от 3 до 63 символов и соответствовать регулярному выражению <code>^[a-z][-a-z0-9]{1,61}[a-z0-9]$</code>.</p> 
description | **string**<br><p>Описание диска.</p> <p>Максимальная длина — 256 символов.</p> 
labels | **object**<br><p>Метки ресурса в формате ключ-значение.</p> <p>Не более 64 на ресурс. Каждый ключ должен быть длиной от 1 до 63 символов и соответствовать регулярному выражению <code>[a-z][-_0-9a-z]*</code>. Максимальная длина каждого значения — не более 63 символов. Каждое значение должно соответствовать регулярному выражению <code>[-_0-9a-z]*</code>.</p> 
typeId | **string**<br><p>Идентификатор типа диска. Чтобы получить список доступных типов дисков, используйте запрос <a href="/docs/compute/api-ref/DiskType/list">list</a>.</p> <p>Максимальная длина — 50 символов.</p> 
zoneId | **string**<br><p>Обязательное поле. Идентификатор зоны доступности, где находится диск. Чтобы получить список доступных зон, используйте запрос <a href="/docs/compute/api-ref/Zone/list">list</a>.</p> <p>Максимальная длина — 50 символов.</p> 
size | **string** (int64)<br><p>Обязательное поле. Размер диска в байтах. Если диск был создан из образа, это значение должно быть больше, чем значение <a href="/docs/compute/api-ref/Image#representation">Image.minDiskSize</a>.</p> <p>Допустимые значения — от 4194304 до 4398046511104 включительно.</p> 
imageId | **string** <br> включает только одно из полей `imageId`, `snapshotId`<br><br><p>Идентификатор образа для создания диска из него.</p> <p>Максимальная длина — 50 символов.</p> 
snapshotId | **string** <br> включает только одно из полей `imageId`, `snapshotId`<br><br><p>Идентификатор снимка для восстановления диска из него.</p> <p>Максимальная длина — 50 символов.</p> 
 
## Ответ {#responses}
**HTTP Code: 200 - OK**

Ресурс Operation. Дополнительные сведения см. в разделе
[Объект Operation](/docs/api-design-guide/concepts/operation).
 
Поле | Описание
--- | ---
id | **string**<br><p>Идентификатор операции.</p> 
description | **string**<br><p>Описание операции. Длина описания должна быть от 0 до 256 символов.</p> 
createdAt | **string** (date-time)<br><p>Время создания ресурса в формате в <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> 
createdBy | **string**<br><p>Идентификатор пользователя или сервисного аккаунта, инициировавшего операцию.</p> 
modifiedAt | **string** (date-time)<br><p>Время, когда ресурс Operation последний раз обновлялся. Значение в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> 
done | **boolean** (boolean)<br><p>Если значение равно <code>false</code> — операция еще выполняется. Если <code>true</code> — операция завершена, и задано значение одного из полей <code>error</code> или <code>response</code>.</p> 
metadata | **object**<br><p>Метаданные операции. Обычно в поле содержится идентификатор ресурса, над которым выполняется операция. Если метод возвращает ресурс Operation, в описании метода приведена структура соответствующего ему поля <code>metadata</code>.</p> 
error | **object** <br> включает только одно из полей `error`, `response`<br><br><p>Описание ошибки в случае сбоя или отмены операции.</p> 
error.<br>code | **integer** (int32)<br><p>Код ошибки. Значение из списка <a href="https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto">google.rpc.Code</a>.</p> 
error.<br>message | **string**<br><p>Текст ошибки.</p> 
error.<br>details | **object**<br><p>Список сообщений с подробными сведениями об ошибке.</p> 
response | **object** <br> включает только одно из полей `error`, `response`<br><br><p>Результат операции в случае успешного завершения. Если исходный метод не возвращает никаких данных при успешном завершении, например метод Delete, поле содержит объект <a href="https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#empty">google.protobuf.Empty</a>. Если исходный метод — это стандартный метод Create / Update, поле содержит целевой ресурс операции. Если метод возвращает ресурс Operation, в описании метода приведена структура соответствующего ему поля <code>response</code>.</p> 