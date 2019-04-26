# Magic function

## 1. \_\_sleep\(\), \_\_wakeup\(\)

클래스를 serializable\(\) 할 때 sleep\(\) 호출

unserializable\(\)할 때 wakeup\(\) 호출

```php
public __sleep ( void ) : array
public __wakeup ( void ) : void

<?php
class Connection
{
    protected $link;
    private $dsn, $username, $password;
    
    public function __construct($dsn, $username, $password)
    {
        $this->dsn = $dsn;
        $this->username = $username;
        $this->password = $password;
        $this->connect();
    }
    
    private function connect()
    {
        $this->link = new PDO($this->dsn, $this->username, $this->password);
    }
    
    public function __sleep()
    {
        return array('dsn', 'username', 'password');
    }
    
    public function __wakeup()
    {
        $this->connect();
    }
}
?>
```

## 2. \_\_toString\(\)

클래스를 문자열로 반환하거나 출력 시에 실행

```php
public __toString ( void ) : string

<?php
// Declare a simple class
class TestClass
{
    public $foo;


    public function __construct($foo)
    {
        $this->foo = $foo;
    }


    public function __toString()
    {
        return $this->foo;
    }
}


$class = new TestClass('Hello');
echo $class;
?>

Outpus : 
Hello
```

## 3. \_\_invoke\(\)

스크립트가 객체를 함수로 호출하려고 할 때 호출된다.

```php
__invoke ([ $... ] ) : mixed

<?php
class CallableClass
{
    public function __invoke($x)
    {
        var_dump($x);
    }
}
$obj = new CallableClass;
$obj(5);
var_dump(is_callable($obj));
?>

Output : 
int(5)
bool(true)
```

## 4. \_\_set\_state\(\)

var\_export\(\)가 내보낸 클래스에 대해 호출된다

```php
static __set_state ( array $properties ) : object

<?php
class A
{
    public $var1;
    public $var2;


    public static function __set_state($an_array) // As of PHP 5.1.0
    {
        $obj = new A;
        $obj->var1 = $an_array['var1'];
        $obj->var2 = $an_array['var2'];
        return $obj;
    }
}

$a = new A;
$a->var1 = 5;
$a->var2 = 'foo';

eval('$b = ' . var_export($a, true) . ';'); // $b = A::__set_state(array(
                                            //    'var1' => 5,
                                            //    'var2' => 'foo',
                                            // ));
var_dump($b);
?>

Output :
object(A)#2 (2) {
  ["var1"]=>
  int(5)
  ["var2"]=>
  string(3) "foo"
}
```

## 5. \_\_debuginfo\(\)

이 메소드는 객체를 덤프 할 때 표시되어야 하는 특성을 얻기 위해 var\_dump\(\), print\_r\(\)에 의해 호출된다.

var\_export\(\)가 내보낸 클래스에 대해 호출된.메서드가 객체에 정의되어 있지 않으면 모든 public, protected 및 private 속성이 표시된다.

```php
__debugInfo ( void ) : array

<?php
class C {
    private $prop;

    public function __construct($val) {
        $this->prop = $val;
    }

    public function __debugInfo() {
        return [
            'propSquared' => $this->prop ** 2,
        ];
    }
}

var_dump(new C(42));
?>

Output :
object(C)#1 (1) {
  ["propSquared"]=>
  int(1764)
}
```

