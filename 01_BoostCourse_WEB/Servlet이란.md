# Servlet이란?

웹 어플리케이션은 정적인 콘텐츠(웹 서버)와 동적인 컨텐츠로 나눌 수 있다.

그렇다면 웹서버는 정적인 컨텐츠를 처리하는데, 어떻게 **동적인 컨텐츠**를 처리할 수 있을까?

=> **서블릿**이 페이지를 동적으로 만들어준다!

## 목차

1. 자바 웹 어플리케이션
2. 서블릿 작성법
   - httpServlet
   - Web.xml

## 자바 웹 어플리케이션 (Java Web Application)

작성된 서블릿은 내부에서 설정한 runtime, 톰캣이라는 WAS를 통해 동작이 된다.

웹 브라우저는 톰캣 서버에 URL 요청을 전송하였고, 서블릿이 실행되었었다.

이런 일련의 과정들로 만들어지는 것이 자바 웹 어플리케이션이다.

> html, css, 이미지, 서블릿....

즉, **WAS(동적+정적)에 설치(배포)되어 동작하는 어플리케이션**이라고 생각하면 된다.

### 디렉토리 구조

디렉토리 구조는 어떤 개발을하던 중요한 것 같다. 

내가 어디서 어떤 작업을 왜 하고있는지 파악하기 좋은 가장 기초적인 지표라고 생각하기 때문이다. ㅎㅎ

- 자바 웹 어플리케이션
  - **WEB-INF 폴더** (!!중요)
    - Web.xml 파일
      - 배포기술자로, 앱 정보를 가지고 있다.
      - 서블릿 3.0 이상에서는 어노테이션이 역할을 대신해준다.
    - lib 폴더 - jar 파일들 (각종 자료 파일들)
    - classes 폴더 - java 패키지, class들
  - 리소스들
    - 각종 이미지, 리소스들..

### 서블릿 정리

`WAS에서 동작하는 JAVA의 클래스`이다. httpServlet 클래스를 상속받아야 하는데.. JSP와 Servlet을 조화롭게 사용하도록하자. 

> html에 표시하고 싶은 내용을 서블릿에 out.print로 전부 찍어내면 너무 하드하다. 그래서 JSP를 함께 사용한다.

## 서블릿 작성법

1. 서블릿 3.0 이상에서 사용하기
   - 자바 annotation을 사용한다.
2. 서블릿 3.0 미만에서 사용하기
   - 서블릿 등록시 web.xml 파일에 직접 등록

### 동적이다?

요청(url)이 들어왔을 때 프로그램(서블릿)이 실행되면서 응답할 코드를 만들어 내고 그 코드로 응답을 하게한다.

### Servlet 살펴보기

- 요청을 받아내는 객체
- 응답을 하기위한 객체

두개가 자동으로 생기며 각 객체안에 추상화 되어 요청에 대한 정보, 응답에 대한 정보를 넣는다.

#### response

얘가 이미지인지 뭔지 브라우저에게 먼저 알려줘야한다. 어떤 것인지 브라우저가 파악하고, 이렇게 해석해서 보여줘야겠다고 결정할 수 있기 때문이다. 

`response.setContentType("text/html;charset=utf-8");`

이제 코드를 보면서 확인해보자.

```java
package exam;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/ten")
public class TenServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException
    {
        response.setContentType("text/html;charset=utf-8");
      // 통로열어주기
        PrintWriter out = response.getWriter();
        out.println("<h1> 1~10까지 출력: <h1>");
        for(int i = 1; i <= 10; i++){
            out.print(i + "<br/>");
        }
        out.close();
    }
}

```

**getWriter()** 메소드

- printWriter 객체를 리턴한다.
- 보낼 내용을 넣어줄 통로를 얻는 것이다! 얻은 통로에 이런 저런 내용을 넣어 브라우저에 응답을 보내보자.

