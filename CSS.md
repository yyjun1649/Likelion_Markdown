# CSS

p{
font-family:'맑은 고딕';
font-size : 18px
color:blue;
}

- 선택자
  스타일을 적용하고자 하는 HTML 요소를 선택하는 역할
- 속성
  지정한 스타일의 속석명에 해당 속성: 값
- 값
  키워드나 특정 단위를 이용하여 원하는 스타일을 적 속성과 쌍을 이룸



- Link style, Enbedding style, lnline style



Link style

\<link rel = "stylesheet" herf="test.css">



Enbedding style

\<style>
    h1{color : red;}
\</style>



lnline style

\<h1 style = "color : red;">Hello</h1>



---

### 선택자

---

스타일을 적용하고자 하는 HTML 요소를 선택하는 역할

h1, h2 {

}
여러개의  스타일을 한번에 지정



단순 선택자

- 타입 선택자

  <style>
      p{}
      h1{}
  </style>

  

- 아이디 선택자

  <style>
      #snow {background: yellow;}
  </style>

  

- 클래스 선택자

  <style>
      .contents{}
  </style>

  

- 전제 선택자

  <style>
      *{}
  </style>

  

- 속성 선택자

  <style>
      a[target="_blank"] {color : red;}
  </style>

  

- pseudo 클래스

  - link : 방문x
  - visited : 방문o
  - hover : mouseEntered

  <style>
      a:link{}
      a:visted{}
      a:hober{}
  </style>



복합 선택자

- 자식 선택자

  <style>
      article > p {}
  </style>

  

- 후손 선택자

  <style>
      article p {}
  </style>

  

#### 텍스트와 관련된 프로퍼티

- font-size
- font-family
- font-style
- font-weight



##### 정렬

- text-align
  자기 자신을 기준으로 정렬
- line-height
  줄간격

- letter-spacing
  자간
- text-indent 
  들여쓰기

---

### 박스모델

---

HTML 모든 요소는 상태 형태

```css
<style>
  #inner{
    border-style: dashed solid dotted double;
    boder-width: 6px;
    border-color: red;
    border: 4px solid lemonchiffon;
    
    border-radius: 12px;
    box-sizing: content-box; // width(height) = content size
    box-sizing: border-box; // width(height) = content size + padding + border
  }
</style>
```

- 패딩

padding : 20px

가장자리의 선의 값



---

### 프로퍼티

---

- display

  요소가 보여지는 방식을 지정

  - block 요소 : 항상 새로운줄, width 기본 100
  - inline : 새로운 줄에서 시작하지 않고, 필요한 만큼의 크기를 가짐
  - display : inline-block : inline 에 사용하면 block과 같은 모양이됨
  - display : none : 사라짐

- position

  - static
    기본값
    

  - relative
    상대위치

  - absoulte
    부모나 조상 중 relativ,absolute,fixed가 선언된 곳을 기준으로 좌표 프로퍼티 적용

  - fixed

    드래그를해도 고정가능

- Z-index
  우선순위를 상대적으로 비교하여 위로 보냄



#### flexbox

- flex container (부모요소) < - display: flex; 추가

  - flex-direction
    flex 컨테이너 안의 item들의 방향을 정함
    - row, row-reverse, column, column-reverse

  

  - flex-wrap
    flex 아이템이 flex 컨테이너를 벗어났을 때 줄을 바꾸는 속성

    - nowrap, wrap

    

  - justify-content
    flex-direction으로 정해진 방향을 기준으로 수평으로 item을 정렬하는 방법을 정함

    - flex-start,f lex-end, space-around, space-between

    

  - align-items
    flex-direction으로 정해진 방향을 기준으로 수직으로 item을 정렬하는 방법을 정함

    - flex-direction : row;
    - flex-direction:column;
    - stretch : 기본
    - flex-start , flex-end, center
    - baseline : 안에있는 글꼴에 기준선으로 정렬

    

  - align-content
    flex-direction으로 정해진 방향을 기준으로 수직으로 여러 줄인 item을 정렬하는 방법을 정함

    - stretch, flex-start, flex-end, center
    - space-between, space-around

    

- flex item(자식요소)

  - flex-grow
    flex 아이템의 확장과 관련된 속성, 기본 0

  

  - flex-shrink
    flex 아이템의 축소와 관련된 속성, 기본1

  

  - flex-basis
    flex 아이템의 기본 크기를 결정함, 기본 auto

  

  - flex
    축약형
    - flex : grow shrink basis













