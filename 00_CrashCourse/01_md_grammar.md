# Markdown 

## Heading

- `#` 해시태그의 개수만큼 헤딩의 중요도가 결정됨.
- `h1`~`h6` 태그가 있음.

## 순서가 있는 리스트

- 순서가 있는 리스트
- `숫자` + `.` 으로 작성 가능

1. 하나
2. 둘
3. 셋
4. 넷

## 순서가 없는 리스트

- `*/-` + `space bar`

## Code Block

```python
import time

time.sleep(60)
print('Hello, World!')
```

- ` ```(빽킷) ` -> 코드 블럭
- ` ``(빽킷) ` -> 인코드 블럭

## Link

- `[텍스트](링크)` : 링크로 바로 이동할 수 있음.

  [구글](https://www.google.com)

  [네이버](https://www.naver.com)

## Image

- `![텍스트](링크)`
- ![손석구](01_md_grammar-images/102224_129789_1357.jpg)

## Text Emphasis

- `**텍스트**` 또는 `__텍스트__` 또는 `Ctrl`+`b`: Bold **Bold** 
- `*텍스트*` 또는 `_텍스트_` 또는 `Ctrl`+`i`: Italic *Italic*
- `~~텍스트~~`: Strkieout ~~Strikeout~~

## Divider

- `---` 혹은 `___`

- HTML

  - ``<br>``: 한줄 띄어주기

  - ``<hr>``: 한줄 그어주기
  


## Blockquotes

  > `>` 한 개만 작성하면 단락을 생성
  >
  > > depth가 생김.
  > >
  > > > depth가 또 생김.

  ## Table

-  `|` (bar): 선

- `space bar` : 칸

| 품목 | 가격 |
| ---- | ---- |
| 진로 | 5000 |
