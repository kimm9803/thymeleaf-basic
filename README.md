<h1>์คํ๋ง MVC 2ํธ</h1>

> ### ๐ Reference
[์คํ๋ง MVC 2ํธ - ๋ฐฑ์๋ ์น ๊ฐ๋ฐ ํ์ฉ ๊ธฐ์ ](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-2/dashboard)

์ธ๊ฐ ๋ค์ ๋๋ง๋ค ๊ณ์ํด์ ์์ ์ค์๋๋ค...

### ๐ข ํ๋ก์ ํธ ์์ฑ
![](https://velog.velcdn.com/images/kimm9803/post/852fcdd8-7f7b-4351-86ea-77680ed711e6/image.png)

- [start.spring.io](https://start.spring.io/) <- ์ฌ๊ธฐ์ ๋ค์ด๊ฐ์ ์คํ๋ง๋ถํธ ํ๋ก์ ํธ๋ฅผ ๋จผ์  ๋ง๋ค์ด์ผํจ
- Project : Gradle - Groovy
- Language : Java
- Spring Boot : 'SNAPSHOT'์ด ๋ถ์ง ์์ ๋ฒ์  ์ค ์ ์ผ ์ต์  ๋ฒ์ ์ ์ ํ
(๋ฒ์  3.0์ด์์ ์ ํํ๊ฒ ๋๋ค๋ฉด **Java 17 ์ด์**์ ์ฌ์ฉํ๊ณ  **javax ํจํค์ง ์ด๋ฆ์ jakarta๋ก ๋ณ๊ฒฝ**)
- Group : hello
- Artifact : thymeleaf-basic
- Name : thymeleaf-basic
- Package name : hello.thymeleaf
- Packaging : Jar
- Java : 11
- Dependencies : Spring Web, Thymeleaf, Lombok
- ๋ฉ์ธ ํด๋์ค ์คํ ํ **http://localhost:8080**์ ํธ์ถํด์ Whitelabel Error Page๊ฐ ๋์ค๋ฉด ์ ์ ๋์!

> InteliJ ๋ฒ์ ์ Gradle์ ํตํด์ ์คํํ๋ ๊ฒ์ด ๊ธฐ๋ณธ ์ค์ ์ธ๋ฐ ์คํ ์๋๊ฐ ๋๋ฆฌ๋ค.
๋ฐ๋ผ์ ๋ค์๊ณผ ๊ฐ์ด ์ค์ ์ ๋ณ๊ฒฝํ๋ฉด ์๋ฐ๋ก ๋ฐ๋ก ์คํํ๋ ๊ฒ์ด๋ผ ์คํ์๋๊ฐ ๋ ๋น ๋ฅด๋ค.
- Settings โถ Build, Execution, Deployment โถ Build Tools โถ Gradle
  - Build and run using : Gradle IntelliJ IDEA
  - Run tests using : Gradle IntelliJ IDEA
  
> Lombok ์ ์ฉ
1. Settings โถ plugin โถ lombok ๊ฒ์ ํ ์คํ (์ฌ์์)
2. Settings โถ Annotation Processors ๊ฒ์ โถ Enable annotation processing ์ฒดํฌ (์ฌ์์)

<br><br>

### ๐ข ํ์คํธ - text, utext

๋ฐ์ดํฐ๋ฅผ ์ถ๋ ฅํ  ๋๋ ์๋์ ๊ฐ์ด th:text ๋ฅผ ์ฌ์ฉ
```<span th:text="${data}">```
HTML ํ๊ทธ์ ์์ฑ์ด ์๋๋ผ HTML ์ฝํ์ธ  ์์ญ์์์ ์ง์  ๋ฐ์ดํฐ๋ฅผ ์ถ๋ ฅํ๊ณ  ์ถ์ผ๋ฉด ๋ค์๊ณผ ๊ฐ์ด ```[[...]]``` ๋ฅผ ์ฌ์ฉ
์ปจํ์ธ  ์์์ ์ง์  ์ถ๋ ฅํ๊ธฐ = ```[[${data}]]```
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
<h1>์ปจํ์ธ ์ ๋ฐ์ดํฐ ์ถ๋ ฅํ๊ธฐ</h1>
<ul>
    <li>th:text ์ฌ์ฉ <span th:text="${data}"></span></li>
    <li>์ปจํ์ธ  ์์์ ์ง์  ์ถ๋ ฅํ๊ธฐ = [[${data}]]</li>
</ul>
</body>
</html>
```
![](https://velog.velcdn.com/images/kimm9803/post/871c2f02-c487-4e8e-b085-456a1a795db1/image.png)

<br>

- ํ์๋ฆฌํ๊ฐ ์ ๊ณตํ๋ ```th:text``` , ```[[...]]``` ๋ ๊ธฐ๋ณธ์ ์ผ๋ก ์ด์ค์ผ์ดํ(escape)๋ฅผ ์ ๊ณต
- ์ด์ค์ผ์ดํ ๊ธฐ๋ฅ์ ์ฌ์ฉํ์ง ์์ผ๋ ค๋ฉด?
- ```th:text``` โถ ```th:utext```
- ```[[...]]``` โถ ```[(...)]```

> BasicController์ ์ถ๊ฐ

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
