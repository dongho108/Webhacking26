# Webhacking26
워게임 26번문제 풀이입니다.

#  26번 문제

## 문제풀기전에 알아야 했던 점
주소의 끝에 [?id=admin]을 입력하면 id값을 줄 수 있다.



## 문제소스코드
```
<?php
  include "../../config.php";
  if($_GET['view_source']) view_source();
?><html>
<head>
<title>Challenge 26</title>
<style type="text/css">
body { background:black; color:white; font-size:10pt; }    
a { color:lightgreen; }
</style>
</head>
<body>
<?php
  if(preg_match("/admin/",$_GET['id'])) { echo"no!"; exit(); }
  $_GET['id'] = urldecode($_GET['id']);
  if($_GET['id'] == "admin"){
    solve(26);
  }
?>
<br><br>
<a href=?view_source=1>view-source</a>
</body>
</html>
```

1. preg_match는 문자열을 매칭되는 값을 찾게되면 그 시점에서 검색이 종료된다. 소스코드를 분석해보면 admin이 매칭되면 no!를 반환한다.
2. 그 다음줄을 살펴보면 입력되는 id의 값이 urldecode되어서 들어간다. 그리고 그 값이 해답이 된다.
3. 그렇다면 “인코딩된 admin의 값”이 해답이다.

그러나 여기서 간과하지 말아야 할 점은 주소창 자체에서 디코딩을 한다는 것이다.
그래서 admin을 인코딩하고 그 값을 또 인코딩을 해야 한다.

[>>그림설명 보려면 클릭<<](https://user-images.githubusercontent.com/54317630/73593320-27718600-4546-11ea-8e09-01a9ac74d5f6.jpeg)
