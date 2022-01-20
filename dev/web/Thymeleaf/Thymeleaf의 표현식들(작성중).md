## 🎈 들어가기전!
안녕하세요! 오늘은 저도 처음 알아보는 **Thymeleaf** 의 기본적인 표현식들을 알아보겠습니다! <br />
**Thymeleaf는** MVC 패턴의 View를 담당하는 **View Template Engine** 인데요!

spring boot와 함께 사용하며 **Controller가 전달해주는 값**을 사용하여 동적 페이지를 만들 수 있어요! <br />
이게 어떠한 말이냐면..

간단하게 회원정보를 관리하는 Controller가 존재할 때, <br />
사용자가 `baseURL/auth/me` 라는 주소로 요청을 보냈을 때 Controller가 해당 사용자의 이름 같은 **값**을 view에게 전달하는거에요!

저는 React를 사용해보았으니까 React의 느낌대로 말하자면,, `userName` 이라는 state에 useEffect와 API를 통해서 값을 저장한 다음 렌더링하는 것과 비슷하다고 보면 되겠네요!

예시
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
      <h1 th:text="${userName}"></h1> //controller에서 전달한 userName 대입!
    </body>
</html>
```
이런 일이 가능해진답니다! 신기하죠??
서론이 떠 엄청 길었네요! 아무튼 이런 Thymeleaf의 기본적인 표현식 5가지를 아래에서 더 알아볼게요!

## 변수 표현식 (Variable expressions) ${...}
아까 위에 예제에서도 잠깐 나왔죠?? 기본적으로 변수를 가져올 수 있는 표현식입니다. <br />
공식 예제를 볼까요?
```jsp
${session.user.name} 
or
<span th:text="${user.profile.name}">
```
이런식으로 가져올 수 있습니다! <br />
또, 추가적으로 신기한 것이 우리가 흔히 알고 있는 foreach를 아래와 같이 사용할 수 있답니다.
```jsp
<ul th:each="item: ${lists}">
  <li th:text="${item.name}" />
</ul>
```

## 선택 표현식 (Selection expressions) \*{...}
이건 사실 위에 변수 표현식과 거의 비슷한데요! <br />
조금 다른 점은 객체 상태의 데이터를 다루는데 조금 차이가 있습니다.

이건 예제를 보시는게 이해가 빠를 것 같아요!
```jsp
<div th:object="${book}"> //해당 부분에서 book 이라는 object에 접근.
...
  <span th:text="*{title}">...</span> //book.title 을 그냥 title로 사용가능.
...
</div>
```
이해가 조금 가시나요?? 사실 저도 확실히 알지 못해 더블체크가 필요한 부분이지만.. <br />
핵심은 span태그에서 본래 book.title 이라는 형식을 단순 title로 가져오게 되는 부분입니다!

마치 js로 예를 들자면
```javascript
// th:obejct="${book}"
const SelectObject = book;
// th:text="*{title}"
SelectObject.title
```
이런 느낌이겠네요!

## 메세지 표현식 (Message expressions) #{...}

(추가예정)
