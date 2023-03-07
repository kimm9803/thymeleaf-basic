<h1>스프링 MVC 2편</h1>

> ### 📗 Reference
[스프링 MVC 2편 - 백엔드 웹 개발 활용 기술](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-2/dashboard)

인강 들을 때마다 계속해서 수정중입니다...

### 🟢 프로젝트 생성
![](https://velog.velcdn.com/images/kimm9803/post/852fcdd8-7f7b-4351-86ea-77680ed711e6/image.png)

- [start.spring.io](https://start.spring.io/) <- 여기에 들어가서 스프링부트 프로젝트를 먼저 만들어야함
- Project : Gradle - Groovy
- Language : Java
- Spring Boot : 'SNAPSHOT'이 붙지 않은 버전 중 제일 최신 버전을 선택
(버전 3.0이상을 선택하게 된다면 **Java 17 이상**을 사용하고 **javax 패키지 이름을 jakarta로 변경**)
- Group : hello
- Artifact : thymeleaf-basic
- Name : thymeleaf-basic
- Package name : hello.thymeleaf
- Packaging : Jar
- Java : 11
- Dependencies : Spring Web, Thymeleaf, Lombok
- 메인 클래스 실행 후 **http://localhost:8080**을 호출해서 Whitelabel Error Page가 나오면 정상 동작!

> InteliJ 버전은 Gradle을 통해서 실행하는 것이 기본 설정인데 실행 속도가 느리다.
따라서 다음과 같이 설정을 변경하면 자바로 바로 실행하는 것이라 실행속도가 더 빠르다.
- Settings ▶ Build, Execution, Deployment ▶ Build Tools ▶ Gradle
  - Build and run using : Gradle IntelliJ IDEA
  - Run tests using : Gradle IntelliJ IDEA
  
> Lombok 적용
1. Settings ▶ plugin ▶ lombok 검색 후 실행 (재시작)
2. Settings ▶ Annotation Processors 검색 ▶ Enable annotation processing 체크 (재시작)

<br><br>

### 🟢 텍스트 - text, utext

데이터를 출력할 때는 아래와 같이 th:text 를 사용
```<span th:text="${data}">```
HTML 테그의 속성이 아니라 HTML 콘텐츠 영역안에서 직접 데이터를 출력하고 싶으면 다음과 같이 ```[[...]]``` 를 사용
컨텐츠 안에서 직접 출력하기 = ```[[${data}]]```
<br>

> - BasicController

```java
package hello.thymeleaf.basic;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/basic")
public class BasicController {

    @GetMapping("/text-basic")
    public String textBasic(Model model) {
        model.addAttribute("data", "Hello Spring!");
        return "basic/text-basic";
    }
}
```

> - /resources/templates/basic/text-basic.html

```
<!doctype html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<h1>컨텐츠에 데이터 출력하기</h1>
<ul>
    <li>th:text 사용 <span th:text="${data}"></span></li>
    <li>컨텐츠 안에서 직접 출력하기 = [[${data}]]</li>
</ul>
</body>
</html>
```
![](https://velog.velcdn.com/images/kimm9803/post/871c2f02-c487-4e8e-b085-456a1a795db1/image.png)

<br>

- 타임리프가 제공하는 ```th:text``` , ```[[...]]``` 는 기본적으로 이스케이프(escape)를 제공
- 이스케이프 기능을 사용하지 않으려면?
- ```th:text``` ▶ ```th:utext```
- ```[[...]]``` ▶ ```[(...)]```

> BasicController에 추가

```java
@GetMapping("/text-unescaped")
public String textUnescaped(Model model) {
 model.addAttribute("data", "Hello <b>Spring!</b>");
 return "basic/text-unescaped";
}
```
> /resources/templates/basic/text-unescape.html

```
<!doctype html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<h1>text vs utext</h1>
<ul>
    <li>th:text = <span th:text="${data}"></span></li>
    <li>th:utext = <span th:utext="${data}"></span></li>
</ul>

<h1><span th:inline="none">[[...]] vs [(...)]</span></h1>
<ul>
    <li><span th:inline="none">[[...]] = </span>[[${data}]]</li>
    <li><span th:inline="none">[(...)] = </span>[(${data})]</li>
</ul>
</body>
</html>
```

![](https://velog.velcdn.com/images/kimm9803/post/2dd0995c-1629-4572-8ed5-28d374263cdd/image.png)


https://velog.io/@kimm9803/%ED%83%80%EC%9E%84%EB%A6%AC%ED%94%84-%EA%B8%B0%EB%B3%B8-%EA%B8%B0%EB%8A%A5
