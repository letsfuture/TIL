# html

## 1. 북마크

- **html에서 북마크 이동**

  ```html
  <h2 id="C4">Chapter 4</h2>
  <a href="#C4">Jump to Chapter 4</a>
  ```

- **다른 페이지의 북마크로 이동**

  ```html
  <a href="html_demo.html#C4">Jump to Chapter 4</a>
  ```

<br>

## 2. 이미지 맵

```html
<img src="workplace.jpg" alt="Workplace" usemap="#workmap">

<map name="workmap">
  <area shape="rect" coords="34,44,270,350" alt="Computer" href="computer.htm">
  <area shape="rect" coords="290,172,333,250" alt="Phone" href="phone.htm">
  <area shape="circle" coords="337,300,44" alt="Coffee" href="coffee.htm">
</map>
```

<br>

## 3. 백그라운드 이미지

```html
<p style="background-image: url('img_girl.jpg');"></p>

<!-- style로 처리하는 이미지 -->
<style>
    p {
      background-image: url('img_girl.jpg');
    }
</style>

<!-- body에 들어가는 이미지 -->
<style>
    body {
      background-image: url('img_girl.jpg');
    }
    </style>

<!-- repeat -->
<style>
    body {
      background-image: url('example_img_girl.jpg');
      background-repeat: no-repeat;
    }
    </style>
    
    <style>
        body {
          background-image: url('img_girl.jpg');
          background-repeat: no-repeat;
          background-attachment: fixed;
          background-size: cover;
        }
        </style>
```

<br>

## 4. 픽처 테크

```html
<picture>
    <source srcset="img_avatar.png">
    <source srcset="img_girl.jpg">
    <img src="img_beatles.gif" alt="Beatles" style="width:auto;">
</picture>   
```

- 몇몇 브라우저나 장치들은 모든 이미지 포맷을 지원하지 않을 수 있음. 그럴 땐 `<picture>` 를 대신 사용하면 해결할 수 있음.

<br>

## 5. 파비콘

```html
<link rel="icon" type="image/x-icon" href="/images/favicon.ico">
```

<br>

## 6. 테이블

- **Tag Description**
  ```html
  <table> Defines a table
  <th>    Defines a header cell in a table
  <tr>    Defines a row in a table
  <td>    Defines a cell in a table
  <caption>   Defines a table caption
  <colgroup>  Specifies a group of one or more columns in a table for formatting
  <col>   Specifies column properties for each column within a <colgroup> element
  <thead> Groups the header content in a table
  <tbody> Groups the body content in a table
  <tfoot> Groups the footer content in a table
  ```
  
- visual code에 `table>tr * 5>td * 3` 를 치면 계층적으로 완성된 table를 불러올 수 있음.

- **테이블 보더**

  ```html
  th, td {
      border: 1px solid black;
      border-radius: 10px;
      border-color: #96D4D4;
    }
  ```

- **테이블 사이즈**

  ```html
  style="width:100%"
  style="height:200px"
  ```

- **테이블 헤더**

  ```html
  <table>
      <tr>
        <th>Firstname</th>
        <td>Jill</td>
        <td>Eve</td>
      </tr>
      <tr>
        <th>Lastname</th>
        <td>Smith</td>
        <td>Jackson</td>
      </tr>
      <tr>
        <th>Age</th>
        <td>94</td>
        <td>50</td>
      </tr>
    </table>
  
  <table>
      <tr>
        <th colspan="2">Name</th>
        <th>Age</th>
      </tr>
      <tr>
        <td>Jill</td>
        <td>Smith</td>
        <td>50</td>
      </tr>
      <tr>
        <td>Eve</td>
        <td>Jackson</td>
        <td>94</td>
      </tr>
  </table>
  ```

<br>

## 7. 리스트

- **Tag Description**

  ```html
  <ul>    Defines an unordered list
  <ol>    Defines an ordered list
  <li>    Defines a list item
  <dl>    Defines a description list
  <dt>    Defines a term in a description list
  <dd>    Describes the term in a description list
  ```

<br>

## 8. 섹션

- `<div>`  : Defines a section in a document (block-level)
- `<span>` : Defines a section in a document (inline)

<br>

## 9. 폼

```html
<input type="text"> Displays a single-line text input field
<input type="radio">    Displays a radio button (for selecting one of many choices)
<input type="checkbox"> Displays a checkbox (for selecting zero or more of many choices)
<input type="submit">   Displays a submit button (for submitting the form)
<input type="button">   Displays a clickable button

<!-- 예시 -->
<form>
  <label for="fname">First name:</label><br>
  <input type="text" id="fname" name="fname"><br>
  <label for="lname">Last name:</label><br>
  <input type="text" id="lname" name="lname">
</form>
```

- **라디오 버튼**

  ```html
  <form>
    <input type="radio" id="html" name="fav_language" value="HTML">
    <label for="html">HTML</label><br>
    <input type="radio" id="css" name="fav_language" value="CSS">
    <label for="css">CSS</label><br>
    <input type="radio" id="javascript" name="fav_language" value="JavaScript">
    <label for="javascript">JavaScript</label>
  </form>
  ```

- **체크박스**

  ```html
  <form>
    <input type="checkbox" id="vehicle1" name="vehicle1" value="Bike">
    <label for="vehicle1"> I have a bike</label><br>
    <input type="checkbox" id="vehicle2" name="vehicle2" value="Car">
    <label for="vehicle2"> I have a car</label><br>
    <input type="checkbox" id="vehicle3" name="vehicle3" value="Boat">
    <label for="vehicle3"> I have a boat</label>
  </form>
  ```

- **form action**

  ```html
  <form action="/action_page.php" method="get">
    <label for="fname">First name:</label><br>
    <input type="text" id="fname" name="fname" value="John"><br>
    <label for="lname">Last name:</label><br>
    <input type="text" id="lname" name="lname" value="Doe"><br><br>
    <input type="submit" value="Submit">
  </form>
  ```

  - method에는 `get`과 `post`가 들어갈 수 있음.
  - `get` : 쿼리스트링으로 처리함. 길이 제한 문제가 있음.
  - `post` : 주소창에 정보를 전달하지 않음. 정보보호나 보안에 유리함.

<br>

## 10. 인풋 타입

  ```html
  <input type="button">
  <input type="checkbox">
  <input type="color">
  <input type="date">
  <input type="datetime-local">
  <input type="email">
  <input type="file">
  <input type="hidden">
  <input type="image">
  <input type="month">
  <input type="number">
  <input type="password">
  <input type="radio">
  <input type="range">
  <input type="reset">
  <input type="search">
  <input type="submit">
  <input type="tel">
  <input type="text">
  <input type="time">
  <input type="url">
  <input type="week">
  ```

<br>

## 11. 콘텐츠 삽입

- **비디오 삽입**

  ```html
  <video width="320" height="240" autoplay muted>
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.ogg" type="video/ogg">
  Your browser does not support the video tag.
  </video>
  ```

- **오디오 삽입**

  ```html
  <audio controls autoplay muted>
    <source src="horse.ogg" type="audio/ogg">
    <source src="horse.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
  </audio>
  ```

- **유튜브 삽입**

  ```html
  <iframe width="420" height="315"
  src="https://www.youtube.com/embed/tgbNymZ7vqY?controls=0">
  </iframe>
  ```


<br>

## 12. 자바스크립트

```html
<html>
    <body>

    <h1>My First JavaScript</h1>

    <button type="button"
    onclick="document.getElementById('demo').innerHTML = Date()">
    Click me to display Date and Time.</button>

    <p id="demo"></p>

    </body>
</html>

<script>
    document.getElementById("demo").innerHTML = "Hello JavaScript!";
</script>
```

<br>

## 13. 헤드

- **Tag Description**

  ```html
  <head>  Defines information about the document
  <title> Defines the title of a document
  <base>  Defines a default address or a default target for all links on a page
  <link>  Defines the relationship between a document and an external resource
  <meta>  Defines metadata about an HTML document
  <script>    Defines a client-side script
  <style> Defines style information for a document
  ```

  