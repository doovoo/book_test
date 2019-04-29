---
description: 이것저것
---

# Memo

## 1. Composer

{% code-tabs %}
{% code-tabs-item title="composer.json" %}
```javascript
{
    "name": "[vender name]/[dir]",
    "description": "[설명]",
    "require": {
        "monolog/monolog": "1.0.*"
    },
    "autoloader": {
        "psr-4": {"": ""}
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="test.php" %}
```php
<?php
    require 'vendor/autoload.php';
    ...
?>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 1. Commands

{% code-tabs %}
{% code-tabs-item title="Bash Shell" %}
```bash
$ cd [composer.json 파일이 있는 directory]
$ composer install
```
{% endcode-tabs-item %}
{% endcode-tabs %}

해당 위치에 `vendor` 폴더 및 `composer.lock` 자동 생성

> #### `./vendor/composer`
>
> autoloding에 실행 코드 파일들이 위치하고 있음

> #### `./composer.lock`
>
> 의존성 패키지들을 설치한 뒤에 컴포저는 `composer.lock`파일에 설치한 패키지들의 정확한 버전 목록을 저장합니다. 이 잠금설정들이 프로젝트가 필요로 하는 특정 버전들을 의미합니다.
>
> `install`명령어는 이 잠금파일이 디렉토리에 존재하는지 확인하고 만약 그렇다면 \(`composer.json`에 관계없이\) 잠금설정된 버전의 패키지들을 다운받습니다.



