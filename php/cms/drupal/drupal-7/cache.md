# Cache

## 1. Static variable

```php
function my_module_function() {
    $my_data = &drupal_static(__FUNCTION__);
    if (!isset($my_data)) {
        // Do your expensive calculations here, and populate $my_data
        // with the correct stuff..
    }
    return $my_data;
}
```

drupal\_static\(\)은 처음으로 호출 할 때 빈 값을 반환하지만 함수가 다시 호출 될 때 변수에 대한 변경 사항은 보존된다 즉 변수가 이미 채워 졌는지 여부를 확인할 수 있으며 더 이상 일을 하지 않고 즉시 반환 할 수 있다. 결과 정보는 페이지로드 지속 기간 동안 정적 변수에 보관된다.

## 2. Drupal's cache function

```php
function my_module_function() {
    $my_data = &drupal_static(__FUNCTION__);
    if (!isset($my_data)) {
        if ($cache = cache_get('my_module_data')) {
            $my_data = $cache->data;
        } else {
            // Do your expensive calculations here, and populate $my_data
            // with the correct stuff..
            cache_set('my_module_data', $my_data, 'cache');
        }
    }
    return $my_data;
}
```

정적 변수 기술은 단일 페이지로드 기간 동안 만 데이터를 저장한다 영구적인 방식으로 데이터를 캐시 할 수 있다

정적 변수의 초기 검사가 끝나면이 함수는 Drupal의 캐시에서 특정 키와 함께 저장된 데이터를 찾는다 찾으면 $my\_data가 $cache-&gt; data로 설정되고 완료된다. 정적 변수와 결합하여 이 페이지 요청 동안 향후 호출은 cache\_get\(\)을 호출 할 필요조차 없다.

일반적으로 캐시의 이름은 앞에 모듈의 이름을 붙이는게 좋다.

## 3. Cache delete

```php
cache_clear_all('my_module', 'cache', TRUE);
```

키가 'my\_module'로 시작하는 모든 캐시 값이 지워진다.

## 4. Cache's expiration date

```php
// 60초 * 60분 * 24시간 * 30일
cache_set('my_module_data', $field, 'cache', time() + 60 * 60 * 24 * 30);
```

캐시를 설정할때 위의 코드와 같이 만료일을 설정해 줄 수 있다.

## 5. Cinbtrolling Where cached data is stored

```php
function mymodule_schema() {
    $schema['cache_mymodule'] = drupal_get_schema_unprocessed('system', 'cache');
    return $schema;
}
```

drupal\_get\_schema\_unprocessed\('system', 'cache'\)는 시스템 모듈의 표준 Cache 테이블 정의를 검색하고, $schema에 cache\_mymodule이라는 클론을 만든다.

cache\_ 접두사는 캐시 테이블 정리에 도움이 된다

이렇게 생성된 cache\_mymodule은 아래 코드의 해당 파라미터 대신에 적으면 된다.

```php
cache_get('my_module_data', 'cache')            // 2번째 파라미터
cache_set('my_module_data', $field, 'cache')    // 3번째 파라미터
cache_clear_all('my_module', 'cache', TRUE);    // 2번재 파라미터
```

\*\* Drupal은 대체 캐싱 시스템의 사용도 지원한다 사이트의 settings.php 파일에서 한 줄을 변경하면 표준 cache\_set \(\), cache\_get \(\) 및 cache\_clear\_all \(\) 함수의 다른 구현을 가리킬 수 있다.

## 6. Advanced caching with renderable content

```php
$content['my_content'] = array(
    '#cache' => array(
        'cid' => 'my_module_data',
        'bin' => 'cache',
        'expire' => time() + 360,
    ),
// Other element properties go here...);
```

위의 요소를 추가하면 drupal\_render\(\) 함수가 page 엘리먼트가 생성 될 때 마다 렌더링 된 HTML을 캐시하고 재사용하도록 지시 할 수 있다.

