# Swagger\Client\ItemApi

All URIs are relative to *https://api.avito.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**applyVas**](ItemApi.md#applyvas) | **PUT** /core/v2/items/{itemId}/vas/ | Применение услуг продвижения
[**getItemInfo**](ItemApi.md#getiteminfo) | **GET** /core/v1/accounts/{user_id}/items/{item_id}/ | Получение информации по объявлению
[**getItemsInfo**](ItemApi.md#getitemsinfo) | **GET** /core/v1/items | Получение информации по объявлениям
[**itemStatsShallow**](ItemApi.md#itemstatsshallow) | **POST** /stats/v1/accounts/{user_id}/items | Получение статистики по списку объявлений
[**postCallsStats**](ItemApi.md#postcallsstats) | **POST** /core/v1/accounts/{user_id}/calls/stats/ | Получение статистики по звонкам
[**putItemVas**](ItemApi.md#putitemvas) | **PUT** /core/v1/accounts/{user_id}/items/{item_id}/vas | Применение дополнительных услуг
[**putItemVasPackageV2**](ItemApi.md#putitemvaspackagev2) | **PUT** /core/v2/accounts/{user_id}/items/{item_id}/vas_packages | Применение пакета дополнительных услуг
[**vasPrices**](ItemApi.md#vasprices) | **POST** /core/v1/accounts/{userId}/vas/prices | Получение информации о стоимости услуг продвижения и доступных значках

# **applyVas**
> map[string,\Swagger\Client\Model\ApplyVasResp] applyVas($authorization, $item_id, $body)

Применение услуг продвижения

С помощью этого метода вы можете применить к опубликованному объявлению одну или несколько услуг продвижения (например, «XL-объявление», «Выделение цветом» и «До 10 раз больше просмотров на 7 дней»). В рамках одного запроса услуга может быть применена только один раз.   Если для вашего объявления доступны значки (такие как «Без ДТП», «Срочно», «1 владелец»), при подключении услуги «XL-объявление» вы можете передать их список (не более трёх значков). В этом случае добавьте соответствующую услугу на 1, 2 или 3 значка.  [Подробнее об услугах продвижения](https://support.avito.ru/partitions/131)  Чтобы получить список доступных услуг и значков,  используйте метод `/core/v1/accounts/{userId}/vas/prices`.  Если заказ сформирован успешно, в ответ вы получите уникальные идентификаторы операций покупки для каждой из применяемых услуг. Позже эти идентификаторы можно будет использовать, чтобы узнать статус выполнения заказа.  В случае некорректного запроса метод вернет код ответа 400 и структуру, содержащую поле `code`. Возможные коды ошибок:   - **1001** – один или несколько заголовков неправильно передаются;   - **1002** – ошибка в URL;   - **1003** – неверный идентификатор объявления из запроса;   - **1004** – JSON из тела запроса не соответствует схеме или список идентификаторов услуг пустой;   - **1005** – объявление, к которому вы хотите применить услуги, неактивно;   - **1006** – неправильное количество выбранных значков для объявления. Убедитесь, что в списке идентификаторов услуг есть услуга для покупки значков и она совпадает с количеством выбранных значков.       - stickerpack_x1 – 1 значок       - stickerpack_x2 – 2 значка       - stickerpack_x3 – 3 значка   - **1007** – некоторые из выбранных услуг не могут быть применены;   - **1008** – в объявлении появились обязательные поля, которые нужно заполнить. Отредактируйте объявление и попробуйте применить услугу снова.   - **1009** – в кошельке не хватает средств для покупки услуг;   - **1010** – вы пытались купить больше одной услуги увеличения просмотров;   - **1011** – вы пытались купить значки, недоступные для выбранного объявления.  В случае внутренней ошибки на стороне Авито вернётся код ответа 500 и структура, содержащая поле `code`. Возможные коды ошибок:   - **1000** – ошибка на стороне Авито, попробуйте позже или [напишите в поддержку](https://support.avito.ru/request/659?eventData[contextId]=117);  **Важно:** если ответ пришёл без кода ошибки или его значения нет в списке выше — возможно, услуга всё-таки была куплена. Подождите несколько минут: услуга продвижения появится в списке применённых, а если нет — попробуйте оформить её снова.

### Example
```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

// Configure OAuth2 access token for authorization: AuthorizationCode
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');
// Configure OAuth2 access token for authorization: ClientCredentials
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');

$apiInstance = new Swagger\Client\Api\ItemApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$authorization = "authorization_example"; // string | Токен для авторизации
$item_id = 789; // int | Идентификатор объявления на сайте
$body = new \Swagger\Client\Model\ItemIdVasBody(); // \Swagger\Client\Model\ItemIdVasBody | 

try {
    $result = $apiInstance->applyVas($authorization, $item_id, $body);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ItemApi->applyVas: ', $e->getMessage(), PHP_EOL;
}
?>
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **authorization** | **string**| Токен для авторизации |
 **item_id** | **int**| Идентификатор объявления на сайте |
 **body** | [**\Swagger\Client\Model\ItemIdVasBody**](../Model/ItemIdVasBody.md)|  | [optional]

### Return type

[**map[string,\Swagger\Client\Model\ApplyVasResp]**](../Model/ApplyVasResp.md)

### Authorization

[AuthorizationCode](../../README.md#AuthorizationCode), [ClientCredentials](../../README.md#ClientCredentials)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

# **getItemInfo**
> \Swagger\Client\Model\ItemInfoAvito getItemInfo($user_id, $item_id, $authorization)

Получение информации по объявлению

Возвращает данные об объявлении - его статус, список примененных услуг  **Внимание:** для получения статистики объявления должен использоваться метод: [получение статистики по списку объявлений](#operation/itemStatsShallow)

### Example
```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

// Configure OAuth2 access token for authorization: AuthorizationCode
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');
// Configure OAuth2 access token for authorization: ClientCredentials
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');

$apiInstance = new Swagger\Client\Api\ItemApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$user_id = 789; // int | Номер пользователя в Личном кабинете Авито
$item_id = 789; // int | Идентификатор объявления на сайте
$authorization = "authorization_example"; // string | Токен для авторизации

try {
    $result = $apiInstance->getItemInfo($user_id, $item_id, $authorization);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ItemApi->getItemInfo: ', $e->getMessage(), PHP_EOL;
}
?>
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **user_id** | **int**| Номер пользователя в Личном кабинете Авито |
 **item_id** | **int**| Идентификатор объявления на сайте |
 **authorization** | **string**| Токен для авторизации |

### Return type

[**\Swagger\Client\Model\ItemInfoAvito**](../Model/ItemInfoAvito.md)

### Authorization

[AuthorizationCode](../../README.md#AuthorizationCode), [ClientCredentials](../../README.md#ClientCredentials)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

# **getItemsInfo**
> \Swagger\Client\Model\ItemsInfoWithCategoryAvito getItemsInfo($authorization, $per_page, $page, $status, $updated_at_from, $category)

Получение информации по объявлениям

Возвращает список объявлений авторизованного пользователя - статус, категорию и ссылку на сайте. **Внимание! В настоящий момент этот метод не работает с объявлениями [сотрудников](https://pro.avito.ru/employees).** Он позволяет получить объявления только для пользователя, который указан владельцем этого объявления. В случае сотрудника это будет главный аккаунт компании, для авторизованного сотрудника вернётся пустой список объявлений.

### Example
```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

// Configure OAuth2 access token for authorization: AuthorizationCode
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');
// Configure OAuth2 access token for authorization: ClientCredentials
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');

$apiInstance = new Swagger\Client\Api\ItemApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$authorization = "authorization_example"; // string | Токен для авторизации
$per_page = 25; // int | Количество записей на странице (целое число больше 0 и меньше 100)
$page = 1; // int | Номер страницы (целое число больше 0)
$status = "active"; // string | Статус объявления на сайте (можно указать несколько значений через запятую)
$updated_at_from = "updated_at_from_example"; // string | Фильтр больше либо равно по дате обновления/редактирования объявления в формате YYYY-MM-DD
$category = 56; // int | Идентификатор категории объявления

try {
    $result = $apiInstance->getItemsInfo($authorization, $per_page, $page, $status, $updated_at_from, $category);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ItemApi->getItemsInfo: ', $e->getMessage(), PHP_EOL;
}
?>
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **authorization** | **string**| Токен для авторизации |
 **per_page** | **int**| Количество записей на странице (целое число больше 0 и меньше 100) | [optional] [default to 25]
 **page** | **int**| Номер страницы (целое число больше 0) | [optional] [default to 1]
 **status** | **string**| Статус объявления на сайте (можно указать несколько значений через запятую) | [optional] [default to active]
 **updated_at_from** | **string**| Фильтр больше либо равно по дате обновления/редактирования объявления в формате YYYY-MM-DD | [optional]
 **category** | **int**| Идентификатор категории объявления | [optional]

### Return type

[**\Swagger\Client\Model\ItemsInfoWithCategoryAvito**](../Model/ItemsInfoWithCategoryAvito.md)

### Authorization

[AuthorizationCode](../../README.md#AuthorizationCode), [ClientCredentials](../../README.md#ClientCredentials)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

# **itemStatsShallow**
> \Swagger\Client\Model\StatisticsResponse itemStatsShallow($authorization, $content_type, $user_id, $body)

Получение статистики по списку объявлений

Получение счетчиков по переданному списку объявлений пользователя.  **Внимание:** в запросе может быть передано не более 200 идентификаторов объявлений.  **Внимание:** глубина такого запроса ограничена 270 днями.  ### Счетчики * ~~views - общее число просмотров объявления;~~ __DEPRECATED (будет удалено в апреле 2021 г.).__ Используйте поле uniqViews. * uniqViews - число уникальных пользователей, просмотревших объявление; * ~~contacts - число контактов [1];~~ __DEPRECATED (будет удалено в апреле 2021 г.).__ Используйте поле uniqContacts. * uniqContacts - число уникальных пользователей, совершивших контакты [1]; * ~~favorites - число добавлений объявления в \"избранное\";~~ __DEPRECATED (будет удалено в апреле 2021 г.).__ Используйте поле uniqFavorites. * uniqFavorites - число уникальных пользователей, добавивших объявление в \"избранное\".  ### Группировка счетчиков Счетчики могут быть сгруппированы [2] по: * дням; * неделям - в поле `date` соответствующей структуры будет первый день недели; * месяцам - в поле `date` соответствующей структуры будет первый день месяца.  #### Период группировки Период группировки передается в теле запроса в поле `periodGrouping`. Доступные значения этого поля: * \"day\" (по умолчанию) - без группировки; * \"week\" - суммирование счетчиков за неделю; * \"month\" - суммирование счетчиков за месяц.  ### Примечания * [1]: Под контактом понимаются: запросы телефона продавца, начатый чат с продавцом по конкретному объявлению, отклик на резюме и пр. * [2]: Группировка уникальных пользователей происходит только в рамках одного дня.

### Example
```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

// Configure OAuth2 access token for authorization: AuthorizationCode
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');
// Configure OAuth2 access token for authorization: ClientCredentials
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');

$apiInstance = new Swagger\Client\Api\ItemApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$authorization = "authorization_example"; // string | Токен для авторизации
$content_type = "content_type_example"; // string | Тип данных запроса
$user_id = 789; // int | Идентификатор пользователя (клиента)
$body = new \Swagger\Client\Model\StatisticsShallowRequestBody(); // \Swagger\Client\Model\StatisticsShallowRequestBody | Набор параметров в теле запроса.

try {
    $result = $apiInstance->itemStatsShallow($authorization, $content_type, $user_id, $body);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ItemApi->itemStatsShallow: ', $e->getMessage(), PHP_EOL;
}
?>
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **authorization** | **string**| Токен для авторизации |
 **content_type** | **string**| Тип данных запроса |
 **user_id** | **int**| Идентификатор пользователя (клиента) |
 **body** | [**\Swagger\Client\Model\StatisticsShallowRequestBody**](../Model/StatisticsShallowRequestBody.md)| Набор параметров в теле запроса. | [optional]

### Return type

[**\Swagger\Client\Model\StatisticsResponse**](../Model/StatisticsResponse.md)

### Authorization

[AuthorizationCode](../../README.md#AuthorizationCode), [ClientCredentials](../../README.md#ClientCredentials)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

# **postCallsStats**
> \Swagger\Client\Model\CallsStatsResponse postCallsStats($body, $authorization, $content_type, $user_id)

Получение статистики по звонкам

Получение агрегированной статистики звонков, полученных пользователем

### Example
```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

// Configure OAuth2 access token for authorization: AuthorizationCode
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');
// Configure OAuth2 access token for authorization: ClientCredentials
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');

$apiInstance = new Swagger\Client\Api\ItemApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$body = new \Swagger\Client\Model\CallsStatsRequest(); // \Swagger\Client\Model\CallsStatsRequest | 
$authorization = "authorization_example"; // string | Токен для авторизации
$content_type = "content_type_example"; // string | Тип данных запроса
$user_id = 789; // int | Номер пользователя в Личном кабинете Авито

try {
    $result = $apiInstance->postCallsStats($body, $authorization, $content_type, $user_id);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ItemApi->postCallsStats: ', $e->getMessage(), PHP_EOL;
}
?>
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**\Swagger\Client\Model\CallsStatsRequest**](../Model/CallsStatsRequest.md)|  |
 **authorization** | **string**| Токен для авторизации |
 **content_type** | **string**| Тип данных запроса |
 **user_id** | **int**| Номер пользователя в Личном кабинете Авито |

### Return type

[**\Swagger\Client\Model\CallsStatsResponse**](../Model/CallsStatsResponse.md)

### Authorization

[AuthorizationCode](../../README.md#AuthorizationCode), [ClientCredentials](../../README.md#ClientCredentials)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

# **putItemVas**
> \Swagger\Client\Model\VasApplyAvito putItemVas($authorization, $user_id, $item_id, $body)

Применение дополнительных услуг

**Внимание:** метод объявлен устаревшим и больше не поддерживается. Вместо него используйте метод `/core/v2/items/{itemId}/vas/`  Применение дополнительной услуги к объявлению, в ответе возвращает данные о примененной услуге и сумму списания. [Более подробная информация по дополнительным услугам](https://support.avito.ru/sections/200009758)  **Внимание:** получение ошибки при выполнении этой операции не означает, что услуга точно не была куплена. В этом случае рекомендуется подождать несколько минут и проверить, что услуга отсутствует в списке применённых, а только затем повторить попытку.

### Example
```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

// Configure OAuth2 access token for authorization: AuthorizationCode
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');
// Configure OAuth2 access token for authorization: ClientCredentials
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');

$apiInstance = new Swagger\Client\Api\ItemApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$authorization = "authorization_example"; // string | Токен для авторизации
$user_id = 789; // int | Номер пользователя в Личном кабинете Авито
$item_id = 789; // int | Идентификатор объявления на сайте
$body = new \Swagger\Client\Model\VasIdRequestBody(); // \Swagger\Client\Model\VasIdRequestBody | 

try {
    $result = $apiInstance->putItemVas($authorization, $user_id, $item_id, $body);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ItemApi->putItemVas: ', $e->getMessage(), PHP_EOL;
}
?>
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **authorization** | **string**| Токен для авторизации |
 **user_id** | **int**| Номер пользователя в Личном кабинете Авито |
 **item_id** | **int**| Идентификатор объявления на сайте |
 **body** | [**\Swagger\Client\Model\VasIdRequestBody**](../Model/VasIdRequestBody.md)|  | [optional]

### Return type

[**\Swagger\Client\Model\VasApplyAvito**](../Model/VasApplyAvito.md)

### Authorization

[AuthorizationCode](../../README.md#AuthorizationCode), [ClientCredentials](../../README.md#ClientCredentials)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

# **putItemVasPackageV2**
> \Swagger\Client\Model\VasAmountAvito putItemVasPackageV2($authorization, $user_id, $item_id, $body)

Применение пакета дополнительных услуг

**Внимание:** метод объявлен устаревшим и больше не поддерживается. Вместо него используйте метод `/core/v2/items/{itemId}/vas/`  Применение пакета дополнительных услуг к объявлению, в ответе возвращает сумму списания.  **Внимание:** получение ошибки при выполнении этой операции не означает, что пакет точно не была куплен. В этом случае рекомендуется подождать несколько минут и проверить, что пакет отсутствует в списке применённых, а только затем повторить попытку.

### Example
```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

// Configure OAuth2 access token for authorization: AuthorizationCode
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');
// Configure OAuth2 access token for authorization: ClientCredentials
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');

$apiInstance = new Swagger\Client\Api\ItemApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$authorization = "authorization_example"; // string | Токен для авторизации
$user_id = 789; // int | Номер пользователя в Личном кабинете Авито
$item_id = 789; // int | Идентификатор объявления на сайте
$body = new \Swagger\Client\Model\PackageIdRequestBodyV2(); // \Swagger\Client\Model\PackageIdRequestBodyV2 | 

try {
    $result = $apiInstance->putItemVasPackageV2($authorization, $user_id, $item_id, $body);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ItemApi->putItemVasPackageV2: ', $e->getMessage(), PHP_EOL;
}
?>
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **authorization** | **string**| Токен для авторизации |
 **user_id** | **int**| Номер пользователя в Личном кабинете Авито |
 **item_id** | **int**| Идентификатор объявления на сайте |
 **body** | [**\Swagger\Client\Model\PackageIdRequestBodyV2**](../Model/PackageIdRequestBodyV2.md)|  | [optional]

### Return type

[**\Swagger\Client\Model\VasAmountAvito**](../Model/VasAmountAvito.md)

### Authorization

[AuthorizationCode](../../README.md#AuthorizationCode), [ClientCredentials](../../README.md#ClientCredentials)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

# **vasPrices**
> \Swagger\Client\Model\InlineResponse200 vasPrices($authorization, $user_id, $body)

Получение информации о стоимости услуг продвижения и доступных значках

Возвращает в ответ список объектов со следующей структурой: - `itemId` – идентификатор объявления - `vas` – список объектов, которые содержат информацию о стоимости дополнительных услуг и пакетов дополнительных услуг для каждого объявления. Структура объекта:   - `slug` – идентификатор услуги или пакета услуг:     - `highlight` — [услуга продвижения \"Выделить\"](https://support.avito.ru/articles/200026858)     - `xl` – [услуга продвижения \"XL-объявление\"](https://support.avito.ru/articles/685)     - `stickerpack_x1` – [1 значок на XL-объявлении](https://support.avito.ru/articles/2450)      - `stickerpack_x2` – [2 значка на XL-объявлении](https://support.avito.ru/articles/2450)     - `stickerpack_x3` – [3 значка на XL-объявлении](https://support.avito.ru/articles/2450)      - `x2_1` – [пакет \"до 2 раз больше просмотров на 1 день\"](https://support.avito.ru/articles/1398)     - `x2_7` – [пакет \"до 2 раз больше просмотров на 7 дней\"](https://support.avito.ru/articles/1398)     - `x5_1` – [пакет \"до 5 раз больше просмотров на 1 день\"](https://support.avito.ru/articles/1398)     - `x5_7` – [пакет \"до 5 раз больше просмотров на 7 дней\"](https://support.avito.ru/articles/1398)     - `x10_1` – [пакет \"до 10 раз больше просмотров на 1 день\"](https://support.avito.ru/articles/1398)     - `x10_7` – [пакет \"до 10 раз больше просмотров на 7 дней\"](https://support.avito.ru/articles/1398)     - `x15_1` – [пакет \"до 15 раз больше просмотров на 1 день\"](https://support.avito.ru/articles/1398)     - `x15_7` – [пакет \"до 15 раз больше просмотров на 7 дней\"](https://support.avito.ru/articles/1398)     - `x20_1` – [пакет \"до 20 раз больше просмотров на 1 день\"](https://support.avito.ru/articles/1398)     - `x20_7` – [пакет \"до 20 раз больше просмотров на 7 дней\"](https://support.avito.ru/articles/1398)    - `price` – цена в рублях с учетом скидки    - `priceOld` – цена в рублях до применения скидки  - `stickers` – список объектов которые содержат доступные для объявления  [значки](https://support.avito.ru/articles/2450)   - `id` – идентификатор значка   - `title` – название значка   - `description` – описание значка

### Example
```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

// Configure OAuth2 access token for authorization: AuthorizationCode
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');
// Configure OAuth2 access token for authorization: ClientCredentials
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');

$apiInstance = new Swagger\Client\Api\ItemApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$authorization = "authorization_example"; // string | Токен для авторизации
$user_id = 789; // int | Номер пользователя в Личном кабинете Авито
$body = new \Swagger\Client\Model\PricesItemIdsRequestBody(); // \Swagger\Client\Model\PricesItemIdsRequestBody | Набор идентификаторов объявлений на сайте

try {
    $result = $apiInstance->vasPrices($authorization, $user_id, $body);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ItemApi->vasPrices: ', $e->getMessage(), PHP_EOL;
}
?>
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **authorization** | **string**| Токен для авторизации |
 **user_id** | **int**| Номер пользователя в Личном кабинете Авито |
 **body** | [**\Swagger\Client\Model\PricesItemIdsRequestBody**](../Model/PricesItemIdsRequestBody.md)| Набор идентификаторов объявлений на сайте | [optional]

### Return type

[**\Swagger\Client\Model\InlineResponse200**](../Model/InlineResponse200.md)

### Authorization

[AuthorizationCode](../../README.md#AuthorizationCode), [ClientCredentials](../../README.md#ClientCredentials)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

