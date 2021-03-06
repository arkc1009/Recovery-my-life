## ๐ ๋ค์ด๊ฐ๊ธฐ์ !
์๋ํ์ธ์! ์ค๋์ ์ ๋ ์ฒ์ ์์๋ณด๋ **Thymeleaf** ์ ๊ธฐ๋ณธ์ ์ธ ํํ์๋ค์ ์์๋ณด๊ฒ ์ต๋๋ค! <br />
**Thymeleaf๋** MVC ํจํด์ View๋ฅผ ๋ด๋นํ๋ **View Template Engine** ์ธ๋ฐ์!

spring boot์ ํจ๊ป ์ฌ์ฉํ๋ฉฐ **Controller๊ฐ ์ ๋ฌํด์ฃผ๋ ๊ฐ**์ ์ฌ์ฉํ์ฌ ๋์  ํ์ด์ง๋ฅผ ๋ง๋ค ์ ์์ด์! <br />
์ด๊ฒ ์ด๋ ํ ๋ง์ด๋๋ฉด..

๊ฐ๋จํ๊ฒ ํ์์ ๋ณด๋ฅผ ๊ด๋ฆฌํ๋ Controller๊ฐ ์กด์ฌํ  ๋, <br />
์ฌ์ฉ์๊ฐ `baseURL/auth/me` ๋ผ๋ ์ฃผ์๋ก ์์ฒญ์ ๋ณด๋์ ๋ Controller๊ฐ ํด๋น ์ฌ์ฉ์์ ์ด๋ฆ ๊ฐ์ **๊ฐ**์ view์๊ฒ ์ ๋ฌํ๋๊ฑฐ์์!

์ ๋ React๋ฅผ ์ฌ์ฉํด๋ณด์์ผ๋๊น React์ ๋๋๋๋ก ๋งํ์๋ฉด,, `userName` ์ด๋ผ๋ state์ useEffect์ API๋ฅผ ํตํด์ ๊ฐ์ ์ ์ฅํ ๋ค์ ๋ ๋๋งํ๋ ๊ฒ๊ณผ ๋น์ทํ๋ค๊ณ  ๋ณด๋ฉด ๋๊ฒ ๋ค์!

์์
```java
//UserController.java
...
@Controller
public class UserController() {
  @GetMapping("/user/${id}")
  public getProfile(@PathVariable String id) {
     ModelAndView mav = new ModelAndView("profile"); //template/profile.html
     const username = userService.getName(id);
     
     mav.addObject("userName", username);
     
     return mav;
  } 
}
```
```html
<!--template/profile.html-->
...
<html lang="ko" xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>My Profile(onlyName..)</title>
        <meta charset="UTF-8">
    </head>
    <body>
      <h1 th:text="${userName}"></h1> //controller์์ ์ ๋ฌํ userName ๋์!
    </body>
</html>
```
์ด๋ฐ ์ผ์ด ๊ฐ๋ฅํด์ง๋ต๋๋ค! ์ ๊ธฐํ์ฃ ??
์๋ก ์ด ๋  ์์ฒญ ๊ธธ์๋ค์! ์๋ฌดํผ ์ด๋ฐ Thymeleaf์ ๊ธฐ๋ณธ์ ์ธ ํํ์ 5๊ฐ์ง๋ฅผ ์๋์์ ๋ ์์๋ณผ๊ฒ์!

## ๋ณ์ ํํ์ (Variable expressions) ${...}
์๊น ์์ ์์ ์์๋ ์ ๊น ๋์์ฃ ?? ๊ธฐ๋ณธ์ ์ผ๋ก ๋ณ์๋ฅผ ๊ฐ์ ธ์ฌ ์ ์๋ ํํ์์๋๋ค. <br />
๊ณต์ ์์ ๋ฅผ ๋ณผ๊น์?
```jsp
${session.user.name} 
or
<span th:text="${user.profile.name}">
```
์ด๋ฐ์์ผ๋ก ๊ฐ์ ธ์ฌ ์ ์์ต๋๋ค! <br />
๋, ์ถ๊ฐ์ ์ผ๋ก ์ ๊ธฐํ ๊ฒ์ด ์ฐ๋ฆฌ๊ฐ ํํ ์๊ณ  ์๋ foreach๋ฅผ ์๋์ ๊ฐ์ด ์ฌ์ฉํ  ์ ์๋ต๋๋ค.
```jsp
<ul th:each="item: ${lists}">
  <li th:text="${item.name}" />
</ul>
```

## ์ ํ ํํ์ (Selection expressions) \*{...}
์ด๊ฑด ์ฌ์ค ์์ ๋ณ์ ํํ์๊ณผ ๊ฑฐ์ ๋น์ทํ๋ฐ์! <br />
์กฐ๊ธ ๋ค๋ฅธ ์ ์ ๊ฐ์ฒด ์ํ์ ๋ฐ์ดํฐ๋ฅผ ๋ค๋ฃจ๋๋ฐ ์กฐ๊ธ ์ฐจ์ด๊ฐ ์์ต๋๋ค.

์ด๊ฑด ์์ ๋ฅผ ๋ณด์๋๊ฒ ์ดํด๊ฐ ๋น ๋ฅผ ๊ฒ ๊ฐ์์!
```jsp
<div th:object="${book}"> //ํด๋น ๋ถ๋ถ์์ book ์ด๋ผ๋ object์ ์ ๊ทผ.
...
  <span th:text="*{title}">...</span> //book.title ์ ๊ทธ๋ฅ title๋ก ์ฌ์ฉ๊ฐ๋ฅ.
...
</div>
```
์ดํด๊ฐ ์กฐ๊ธ ๊ฐ์๋์?? ์ฌ์ค ์ ๋ ํ์คํ ์์ง ๋ชปํด ๋๋ธ์ฒดํฌ๊ฐ ํ์ํ ๋ถ๋ถ์ด์ง๋ง.. <br />
ํต์ฌ์ spanํ๊ทธ์์ ๋ณธ๋ book.title ์ด๋ผ๋ ํ์์ ๋จ์ title๋ก ๊ฐ์ ธ์ค๊ฒ ๋๋ ๋ถ๋ถ์๋๋ค!

๋ง์น js๋ก ์๋ฅผ ๋ค์๋ฉด
```javascript
// th:obejct="${book}"
const SelectObject = book;
// th:text="*{title}"
SelectObject.title
```
์ด๋ฐ ๋๋์ด๊ฒ ๋ค์!

## ๋ฉ์ธ์ง ํํ์ (Message expressions) #{...}

(์ถ๊ฐ์์ )
