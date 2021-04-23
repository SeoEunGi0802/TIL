# PHP
------------
## 2021-04-21(졸작으로 인해 늦어진 TIL 작성)
------------
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
    ```
    <?php
    $id = $_GET['GET_TEST'];
    echo $id;
    ?>
    ```
    이런 식으로 가능하다.<br/>
    GET 방식 이므로 입력한 값이 '123' 이라면 URL에 "http://localhost/~~~?GET_TEST=123"으로 나타난다.<br/>
    여기서 'echo'는 글자를 HTML 으로 변환하여 출력해준다. 비슷한 코드로 print가 있다.<br/>

    #### $_POST<br/>
    HTML form이 method="POST"으로 제출되었을 때 form 데이터를 수집하는 데 사용하고 또한 변수를 전달할 때도 사용한다.
    ```
    <form action="<?php echo $_SERVER['PHP_SELF'];?>" method="POST">
        ID : <input type="text" name="POST_TEST">
        <input type="submit">
    </form>
    ```
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
    ```
    <?php
    $name = $_REQUEST['fname'];
    echo $name;
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
    쿠키(cookie)란 웹 사이트에 접속할 때 서버에 의해 사용자의 컴퓨터에 저장되는 정보를 의미한다.<br/>
    쿠키는 사용자를 식별하는데 종종 사용된다.<br/>
    쿠키는 서버가 사용자 컴퓨터에 내장하는 작은 파일이다.<br/>
    같은 컴퓨터가 브라우져로 페이지를 요청할 때마다, 쿠키도 함께 보낸다.<br/>
    웹 사이트는 이렇게 저장된 사용자의 정보를 클라이언트(client) 측의 컴퓨터에 남겨서 필요할 때마다 재사용한다.<br/>
    현재 이러한 쿠키는 로그인 정보나 장바구니 정보를 저장하는 용도로 많이 활용되고 있다.<br/>
    하지만 사용자의 정보가 컴퓨터에 고스란히 남기 때문에 사생활 침해의 우려가 있으며, 보안과 관련된 이슈를 가지고 있다.<br/>

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
    setcookie() 함수의 매개변수 중에서 쿠키 명을 제외한 매개변수는 모두 옵션이다.<br/>
    쿠키는 명시된 지속 시간이 지나면 무효가 되며, 지속 시간을 전달하지 않으면 브라우저가 닫히기 전까지 계속 유효하다.<br/>
    또한, 사용자가 직접 삭제하지 않는 한 브라우저에 계속 남아 있을 것이다.<br/>
    쿠키를 생성할 때 유효한 주소와 경로를 매개변수로 전달할 수 있다.<br/>
    만약 HTTPS 프로토콜에서 사용하려면 secure 값을 true로 설정해야 한다.
    또한, HTTP 프로토콜에서만 사용하도록 하려면 httponly 값을 true로 설정하면 된다.<br/>
    ```
    <body>
        <?php
        $cookie = $_COOKIE['COOKIE'];
        echo "쿠키 정보：{$cookie}";
        ?>
        <form method="POST" action="./test.php">
            <input type="text" name="COOKIE_TEST">
            <input type="submit" value="전송">
        </form>
    </body>
    ```
    PHP에서 unset() 함수나 setcookie() 함수를 사용하면, 생성된 쿠키를 삭제할 수 있다.<br/>
    ```
    unset($_COOKIE["COOKIE"]);
    or
    setcookie($cookieName, $POST_COOKIE, time()-60, "/");
    ```

    #### $_SESSION<br/>
    $_SESSION는 쿠키에 대한 코드 입니다.<br/>
    세션(session)이란 웹 사이트의 여러 페이지에 걸쳐 사용되는 사용자 정보를 저장하는 방법을 의미한다.<br/>
    사용자가 브라우저를 닫아 서버와의 연결을 끝내는 시점까지를 세션이라고 한다.<br/>
    쿠키는 클라이언트 측의 컴퓨터에 모든 데이터를 저장합니다. 하지만 세션은 서비스가 돌아가는 서버 측에 데이터를 저장하고, 세션의 키값만을 클라이언트 측에 남겨둔다.<br/>
    브라우저는 필요할 때마다 이 키값을 이용하여 서버에 저장된 데이터를 사용하게 된다.<br/>
    이러한 세션은 보안에 취약한 쿠키를 보완해주는 역할을 하고 있다.<br/><br/>

    PHP에서는 session_start() 함수를 이용하여 새로운 세션을 시작하거나, 기존의 세션을 다시 시작할 수 있다.<br/>
    session_start() 함수는 세션 아이디가 이미 존재하는지를 확인하고, 존재하지 않으면 새로운 아이디를 만든다.<br/>
    만약 이미 존재하는 세션 아이디가 있을 때는 원래 있던 세션 변수를 다시 불러와서 사용할 수 있도록 한다.<br/>
    세션 아이디는 웹 서버에 의해 무작위로 만들어진 숫자이다.<br/>
    이 세션 아이디는 세션이 유지되는 동안 클라이언트 측에 저장되며, 세션 변수를 등록하는 키로 사용된다.<br/>
    웹 서버에서는 클라이언트로부터 받아온 세션 아이디를 가지고, 해당 아이디에 대응되는 세션 변수에 접근할 수 있다.<br/>
    쿠키와 마찬가지로 세션도 어떤 헤더보다도 먼저 생성해야만 한다.<br/>
    세션의 지속 시간은 쿠키와 달리 php.ini 파일에 설정되어 있으므로, 따로 명시해주지 않아도 된다.<br/>
    ```
    session_start();
    ```
    세션이 생성되고 나면 세션 변수를 수퍼 글로벌인 $_SESSION 배열에 등록할 수 있다.<br/>
    이때 세션 변수의 이름이 키값이 되며, 이 내용은 서버 측에 저장된다.<br/>
    등록된 세션 변수는 등록을 해지하지 않는 한 세션이 끝날 때까지 유지된다.<br/>
    ```
    $_SESSION["name"] = "김씨";
    $_SESSION["age"] = 21;
    ```

    생성된 세션 변수는 $_SESSION["~"]으로 접근할 수 있다.<br/>
    ```
    <?php
    session_start();
    session = "session_test";
    $_SESSION['SESSION'] = $session;
    ?>
    ```
    ```
    <body>
        <?php
        echo "세션 정보：{$_SESSION['SESSION']}";
        ?>
    </body>
    ```
    세션 변수의 사용이 모두 끝나면, 세션 변수의 등록을 해지할 수 있다.<br/>
    unset() 함수를 사용하면, 특정 이름의 세션 변수만을 해지할 수 있다.<br/>
    현재 등록된 모든 세션 변수를 해지하고자 할 때에는 session_unset() 함수를 사용하면 된다.<br/>
    또한, 세션을 자체를 완전히 종료하려면 session_destroy() 함수를 사용하여 세션 아이디를 삭제하면 된다.<br/>
    ```
    unset($_SESSION["session"]); //해당 세션 등록 해지
    session_unset(); //모든 세션 등록 해지
    session_destroy(); //세션 자체를 종료
    ```

    + 정적 변수<br/>
    정적 변수(static variable)란 함수 내부에서 static 키워드로 선언한 변수를 의미한다.<br/>
    함수 내부에서 선언된 정적 변수는 함수의 호출이 종료되더라도 메모리상에서 사라지지 않다.<br/>
    하지만 지역 변수처럼 해당 함수 내부에서만 접근할 수 있습니다.<br/>
    ```
    <?php
    function staticfun() {
        static $cnt = 0;
        echo "static count의 값 : {$cnt}<br>";
        $cnt++;
    }
    staticfun();
    staticfun();
    staticfun();
    ?>
    ```
------------
## 2021-04-22
#### 중간고사
------------
## 2021-04-24
------------
## 상수
상수란 변수와 마찬가지로 데이터를 저장할 수 있는 메모리 공간을 의미한다.
하지만 상수가 변수와 다른 점은 한 번 선언되면, 스크립트가 실행되는 동안 그 데이터를 변경하거나 해제할 수 없다는 점이다.
PHP에서는 define() 함수를 사용하여 상수를 선언할 수 있다.
 + define()<br/>
    ```
    define(상수이름, 상수 값, 대소문자구분여부)
    //대소문자구분여부의 디폴트(false, 빈칸 가능)는 구분하고, true가 들어가면 구분을 하지 않는다.
    ```
    ```
    <?php
    function definefunc(){
        echo def; // 에러발생
        define("def", "define() 테스트");
        echo def; // 정상출력
        }
        
        definefunc();
        echo "<br>".def; // 정상출력(이해를 돕기위한 <br>태그 삽입)
    ?>
    ```

## 마법 상수
PHP는 어떤 스크립트에서도 사용할 수 있는 미리 정의된 다양한 상수를 제공한다.

    <?php
    echo "<pre>";
    print_r(get_defined_constants(true));
    echo "</pre>";
    ?>

// 위 코드는 '```' 로 감싸면 제대로 보여지지 않아서 평문으로 작성 //