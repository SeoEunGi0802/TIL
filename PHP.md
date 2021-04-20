# PHP
------------
## 2021-04-21(졸작으로 인해 늦어진 TIL 작성)
PHP는 C언어를 기반으로 만들어진 서버 측에서 실행되는 '서버 사이드 스크립트' 언어이다.<br/>
서버 사이드 스크립트란 서버 측에서 수행하는 처리를 의미한다.<br/>
브라우저에서 요청한 HTML 문서에 서버 사이드 스크립트 언어의 코드가 포함되어 있으면, 서버는 이 부분을 자신이 처리하고 그 결과를 브라우저에 보내 주고
이러한 서버 사이드에서 자주 사용하는 스크립트 언어가 바로 PHP입니다.<br/>
PHP로 작성된 코드를 HTML 코드 안에 추가하면, 웹 서버는 해당 코드를 해석하여 자동으로 HTML 문서를 생성하여서 PHP를 사용하면 동적으로 빠르게 HTML 문서를 만들 수 있다.<br/>
+ 서버에 미리 저장된 파일이 아닌 서버에 있는 데이터들을 서버 사이드 스크립트 언어로 가공하여 생성되는 페이지를 동적 웹 페이지(dynamic web page)라고 한다.<br/>
+ [인용 TCP-SCHOOL](http://www.tcpschool.com/php/intro)

------------
## 변수 선언
PHP에서 변수를 선언할 때는 변수의 이름 앞에 달러($) 기호를 사용하여 선언하고 따로 타입을 명시하지 않는다.<br/>
예시)<br/>

+ 정수<br/>
```
$a = 10;
$b = 20;
$c = $a + $b; //$c == 30;
```

+ 실수<br/>
```
$a2 = 0.1;
$b2 = 0.2;
$c2 = $a2 + $b2; //$c2 == 0.3;
```

+ 문자열<br/>
```
$str = "PHP";
$str2 = "HI";
(잘못된 방법)$str3 = $str + $str2; //$str == 0; PHP에서는 문자열에 '+'기호를 넣어줄 경우 숫자로 인식되어 값이 0으로 나온다.
$str3 = $str.$str2 //$str3 == "PHPHI";
```

+ 배열<br/>
```
$arr = [1, 2, 3, 4, 5];
$arr2 = [1, '2', "3", '4', 5];
$arr3 = $arr.$arr2 //당연히 오류 발생. C언어를 기반으로 하였으므로 반복문으로 출력이 가능하다.
```

+ 알아둬서 나쁘지 않은 것<br/>
실수의 값을 연결하여 보여주고 싶을때 아래와 같이<br/>
$str4 = $a.$b로 선언할 경우 -> $str4 == 0.10.2 이렇게 나온다. 이는<br/>
$str3 = "$a"."$b"로 해결이 가능하다.<br/>
배열을 합치고 싶으면 array_merge라는 함수를 이용하여 가능하다. -> $arr3 = array_merge($arr, $arr2) -> $arr3 == [1, 2, 3, 4, 5, 1, '2', "3", '4', 5];<br/><br/>

## 변수 이름의 생성 규칙
변수의 이름은 그 변수가 가지는 데이터의 의미를 잘 나타내도록 작성하는 것이 좋다.<br/>
PHP에서는 이러한 변수의 이름을 작성할 때 반드시 지켜야 하는 다음과 같은 규칙이 있다.<br/>

1. 변수의 이름은 영문 대소문자, 숫자, 언더스코어(_)로만 구성됩니다.
2. 변수의 이름은 숫자와의 구분을 빠르게 하기 위해 숫자로는 시작할 수 없습니다.
3. 변수의 이름에는 공백이 포함될 수 없습니다.
4. 변수의 이름으로 PHP에서 미리 정의한 $this는 사용할 수 없습니다.
5. 변수의 이름은 대소문자를 구분합니다.<br/><br/>

## 변수의 종류<br/>
PHP에서 변수는 스크립트 내 어느 곳에서나 선언할 수 있다.<br/>
변수의 유효 범위(variable scope)란 특정 변수를 참조되거나 사용할 수 있는 스크립트 내의 범위를 의미한다.<br/>
PHP에서는 이러한 변수의 유효 범위에 따라 변수의 종류를 다음과 같이 구분한다.<br/><br/>

1. 지역 변수(local variable)
2. 전역 변수(global variable)
3. 정적 변수(static variable)

     + 지역 변수<br/>
     함수 내부에서 선언된 변수는 오직 함수 내부에서만 접근할 수 있다.<br/>
     또한, 함수 내부에서 선언된 변수는 함수의 호출이 종료되면 메모리에서 제거된다.<br/>
     이렇게 함수 내부에서 선언된 변수를 지역 변수(local variable)라고 합니다.<br/><br/>

    + 전역 변수<br/>
    함수 밖에서 선언된 변수는 함수 밖에서만 바로 접근할 수 있다.<br/>
    함수 밖에서 선언된 변수를 함수 내부에서 접근하고자 할 때는 global 키워드를 함께 사용해야 한다.<br/>
    이렇게 함수 밖에서 선언된 변수를 전역 변수(global variable)라고 합니다.<br/><br/>
    
    + 슈퍼 글로벌, 슈퍼전역변수, 초전역변수<br/>
    PHP는 미리 정의된 전역 변수인 슈퍼 글로벌(superglobal)을 제공한다.<br/>
    이러한 슈퍼 글로벌은 특별한 선언 없이 스크립트 내의 어디에서라도 바로 사용할 수 있다.<br/>
    PHP에서 제공하는 슈퍼 글로벌은 다음과 같다.<br/>

    #### $GLOBALS<br/>
    변수 앞에 global을 붙여 사용한다.<br/>
    ```
        $x = 1;
        function globalfun() {
            global $x;
        }
    ```
    이렇게 하면 함수globalfun() 내부에서 $x의 값을 사용할 수 있지만 다른 함수에서는 불가능 하므로 다시 선언 해주어야 한다.<br/>

    #### $_SERVER<br/>
    사용시 서버에 대한 정보를 찾아올 수 있다.<br/>
    그뿐만 아니라 $_SERVER 변수를 통해 사용자가 PC에서 접속했는지 서버에서 접속했는지 알 수 있다.<br/>
    $_SERVER['PHP_SELF'] 현재 실행중인 파일 이름<br/>
    $_SERVER[´SERVER_NAME´] 호스트 서버 이름 등등<br/>

    #### $_GET<br>
    HTML form이 method="GET"으로 제출되었을 때 form 데이터를 수집하는 데 사용하고 또한 변수를 전달할 때도 사용한다.
    ```
    <form action="<?php echo $_SERVER['PHP_SELF'];?>" method="GET">
        ID : <input type="text" name="GET_TEST">
        <input type="submit">
    </form>
    ```
    <br/>
    ```
    <?
    $id = $_GET['GET_TEST'];
    echo $id;
    ?>
    ```
    이런 식으로 가능하다.<br/>
    GET 방식 이므로 입력한 값이 '123' 이라면 URL에 "http://localhost/~~~?GET_TEST=123"으로 나타난다.<br/>
    여기서 'echo'는 "~" 안에 있는 글자(~)를 HTML 으로 변환하여 출력해준다. 비슷한 코드로 print가 있다.<br/>

    #### $_POST<br/>
    HTML form이 method="POST"으로 제출되었을 때 form 데이터를 수집하는 데 사용하고 또한 변수를 전달할 때도 사용한다.
    ```
    <form action="<?php echo $_SERVER['PHP_SELF'];?>" method="POST">
        ID : <input type="text" name="POST_TEST">
        <input type="submit">
    </form>
    ```
    <br/>
    ```
    <?php
    $id = $_POST['POST_TEST'];
    echo $id;
    ?>
    ```
    위 GET방식과 매우 비슷하지만 둘의 차이는 크게 URL에 나타나지 않는다.<br/>

    #### $_REQUEST<br/>
    HTML form이 method="POST" 또는 method="GET"으로 제출되었을 때 form 데이터를 수집하는 데 사용하고 또한 변수를 전달할 때도 사용한다.<br/>
    ```
    <form action="<?php echo $_SERVER['PHP_SELF'];?>" method="POST or GET">
        ID : <input type="text" name="REQUEST_TEST">
        <input type="submit">
    </form>
    ```
    <br/>
    ```
    <?php
    $id = $_REQUEST['REQUEST_TEST'];
    echo $id;
    ?>
    ```
    GET, POST 둘다 상관 없이 HTML form이 제출한 데이터를 받아올 수 있다.

    #### $_FILES<br/>
    HTML form안 input type="file"일때 업로드된 파일 데이터를 수집하는 데 사용한다.<br/>
    ```
    <form enctype="multipart/form-data" action="<?php echo $_SERVER['PHP_SELF']; ?>" method="POST">
        FILE : <input type="file" name="FILE_TEST">
        <input type="submit">
    </form>
    ```
    ```
    <?php
    if (count($_FILES)) {
        echo '<pre>';
        echo "업로드된 파일의 대한 정보\n";
        print_r($_FILES);
        print "</pre>";
    }
    ?>
    ```
    위 코드는 결과물이 예상이 잘 안될것이다. 만약 파일을 선택한 후 전송 버튼을 누르게 되면
    ```
    업로드된 파일의 대한 정보
    Array
    (
    [FILE_TEST] => Array
        (
            [name] => 파일이름
            [type] => 파일의 타입
            [tmp_name] => 파일의 위치경로
            [error] => 에러 검출 횟수
            [size] => 파일의 크기(byte)
        )
    )
    ```

    #### $_COOKIE<br/>
    $_COOKIE는 쿠키에 대한 코드 입니다.<br/>
    먼저 쿠키란?<br/>
    쿠키(cookie)란 웹 사이트에 접속할 때 서버에 의해 사용자의 컴퓨터에 저장되는 정보를 의미한다..<br/>
    쿠키는 사용자를 식별하는데 종종 사용된다.<br/>
    쿠키는 서버가 사용자 컴퓨터에 내장하는 작은 파일이다.<br/>
    같은 컴퓨터가 브라우져로 페이지를 요청할 때마다, 쿠키도 함께 보낸다.<br/>
    //setcookie (이름, 값, 폐기 일자);<br/>
    //더 자세한 속성 : setcookie ( $name [, $value [, $expire [, $path [, $domain [, $secure [, $httponly ]]]]]] )<br/>
    ```
    <?php
    if ($_POST != null) {
        $POST_COOKIE = $_POST['COOKIE_TEST'];
        setcookie("COOKIE", $POST_COOKIE, time() + 60 * 1);
        header("Location: ./test.php");
        }
    ?>
    ```
    ```
    
    ```

    #### $_SESSION<br/>



    + 정적 변수<br/>
    정적 변수(static variable)란 함수 내부에서 static 키워드로 선언한 변수를 의미한다.<br/>
    함수 내부에서 선언된 정적 변수는 함수의 호출이 종료되더라도 메모리상에서 사라지지 않다.<br/>
    하지만 지역 변수처럼 해당 함수 내부에서만 접근할 수 있습니다.<br/>