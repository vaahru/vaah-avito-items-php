# Swagger\Client\DefaultApi

All URIs are relative to *https://api.avito.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**updatePrice**](DefaultApi.md#updateprice) | **POST** /core/v1/items/{item_id}/update_price | Обновление цены объявления

# **updatePrice**
> \Swagger\Client\Model\UpdatePriceResponse updatePrice($item_id, $body)

Обновление цены объявления

Обновляет цену товара по id.  Максимальное количество запросов в минуту - 150. **Внимание! Доступно для категорий Товары, Запчасти, Авто, Недвижимость (кроме краткосрочной)**

### Example
```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

// Configure OAuth2 access token for authorization: AuthorizationCode
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');
// Configure OAuth2 access token for authorization: ClientCredentials
$config = Swagger\Client\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');

$apiInstance = new Swagger\Client\Api\DefaultApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$item_id = 789; // int | Идентификатор объявления на сайте
$body = new \Swagger\Client\Model\UpdatePriceRequest(); // \Swagger\Client\Model\UpdatePriceRequest | Набор параметров в теле запроса.

try {
    $result = $apiInstance->updatePrice($item_id, $body);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling DefaultApi->updatePrice: ', $e->getMessage(), PHP_EOL;
}
?>
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **item_id** | **int**| Идентификатор объявления на сайте |
 **body** | [**\Swagger\Client\Model\UpdatePriceRequest**](../Model/UpdatePriceRequest.md)| Набор параметров в теле запроса. | [optional]

### Return type

[**\Swagger\Client\Model\UpdatePriceResponse**](../Model/UpdatePriceResponse.md)

### Authorization

[AuthorizationCode](../../README.md#AuthorizationCode), [ClientCredentials](../../README.md#ClientCredentials)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

