# html

## 1. 스타일

- **텍스트 컬러**

  `<style="color:blue;">`

- **폰트 패밀리**

  `<h1 style="font-family:Verdana, Geneva, Tahoma, sans-serif">I'm so tired.</h1>`

- **폰트 사이즈**

   `<style="font-size:300%;">`

- **텍스트 정렬**

   `<style="text-align:center;">`

- **텍스트 포맷팅**

  ```html
  <b> Defines bold text
  <em>    Defines emphasized text 
  <i> Defines a part of text in an alternate voice or mood
  <small> Defines smaller text
  <strong>    Defines important text
  <sub>   Defines subscripted text
  <sup>   Defines superscripted text
  <ins>   Defines inserted text
  <del>   Defines deleted text
  <mark>  Defines marked/highlighted text
  ```

<br>

## 2. 인라인

- **내부 import**

  ```html
  <head>
      <style>
      body {background-color: powderblue;}
      h1   {color: blue;}
      p    {color: red;}
      </style>
  </head>
  ```

- **외부 import**

  ```html
  <head>
      <link rel="stylesheet" href="styles.css">
      <link rel="stylesheet" href="https://외부경로/html/styles.css">
  </head>
  ```

<br>

## 3. 이미지

- `<img src="이미지 주소", alt="설명", width="500px", height="500px">`

<br>

## 4. 링크

- `<a href="링크", target="_blank">링크 이름</a>`

  `_self` : Default. Opens the document in the same window/tab as it was clicked
  `_blank` : Opens the document in a new window or tab
  `_parent` : Opens the document in the parent frame
  `_top` : Opens the document in the full body of the window

- **기타 링크**

  - **버튼 링크**

    `<button onclick="document.location='default.a'">버튼 이름</button>`

  - **이메일 링크**

    `<a href="mailto:someone@example.com">Send emial</a>`

  - **전화 링크**

    `<a href="tel:010-1234-5678">전화</a>`

- **링크 컬러**

  ```html
  <style>
      a:link {
        color: green;
        background-color: transparent;
        text-decoration: none;
      }
      
      a:visited {
        color: pink;
        background-color: transparent;
        text-decoration: none;
      }
      
      a:hover {
        color: red;
        background-color: transparent;
        text-decoration: underline;
      }
      
      a:active {
        color: yellow;
        background-color: transparent;
        text-decoration: underline;
      }
      </style>
  
  <style>
      a:link, a:visited {
        background-color: #f44336;
        color: white;
        padding: 15px 25px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
      }
      
      a:hover, a:active {
        background-color: red;
      }
      </style>
  ```

<br>

## 5. 예시

  ```html
  <!-- head 안에 style을 지정해줄 수 있음 -->
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
      <style>
          body {background-color: powderblue;}
          h1   {color: blue}
          p    {color: red}
          #title {color: white}
          .content {color: purple}
      </style>
      <link rel="stylesheet" href="styles.css">
  </head>
  <body>
      <!-- 컬러와 정렬 등을 한꺼번에 할 수 있음 -->
      <p style="background-color: aquamarine; text-align: center;">예시예용</p>
  ```

  - class: `.`
  - id: `#`