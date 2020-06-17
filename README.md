# nc-css-masterclass
노마드 코더 SCSS, CSS Flexbox, CSS Grid 강의 노트 

## CSS flexbox

flexbox 이전에는 반응형 웹사이트를 만들기 어렵다. 사용하는 기기의 화면 크기가 달라지면 디자인이 망가졌기 때문이다.

### 1. flexbox

플렉스박스에서는 children보다는 부모 요소가 중요하다. (직계)부모 요소에 display: flex; 를 지정해놓는다. 

그러면 그 안의 자식 요소들은 정렬된다.

### 2. flex-direction

flex-direction는 main axis를 결정한다. 

row(기본값)와 column이 있다.

row는 가로 정렬 , column 세로 정렬이다.

세로로 정렬하고 싶다면 

#### justify-content

main axis(기준축, row 혹은 column)을 기준으로 요소의 위치 결정

`center`: 가운데 정렬

`space-between`: 요소를 양 끝점에 정렬한 뒤 그 사이 요소들을 동일한 간격으로 정렬

`space-around`: 요소들의 양 옆 공간을 동일하게 하여 정렬

`space-evenly`: 요소들을 동일한 간격으로 정렬



```css
justify-content: center;
```

#### align-items

cross axis(main axis에 수직으로 연하는 축)를 기준으로 요소의 위치 결정

`center`: 가운데 정렬

`stretch`: 전체 높이까지 쭉 뻗는다.

`flex-start`: 아이템을 맨 앞에. 기본값.

`flex-end`: 아이템을 맨 끝에.

등등.

#### flex-direction: column;

```css
flex-direction : column;
```

으로 지정하면 main axis는 수직, 세로가 되고, cross axis는 수평, 가로가 된다.

요소는 main axis를 따라 세로로 정렬된다.

### 1.5 align-self and order

flexbox에서 자식에게 줄 수 있는 요소는 두 가지 뿐이다. align-self와 order

#### align-self

flexbox의 자식요소에 지정

align-items와 비슷하지만 자식요소 개별로 지정 가능

```css
.children:nth-child(2) {
  align-self: center;
}
```

flex-direction: row에서 align을 정상적으로 작동하게 하고 싶으면 parent에 height를 줘야 한다.

#### order

HTML을 건드리지 않고 요소의 순서 변경.

모든 요소의 order의 기본값은 0이다.

```css
.children:nth-child(2) {
  order: 1;
}
```

이런식으로 지정하면 1, 3의 order는 0이기 때문에 두 번째 요소는 마지막에 배치된다.

### 1.6 wrap, nowrap, reverse, align-content

기본적으로 flexbox는 너비가 바뀌는 한이 있더라도 한 줄에 정렬된다.

`flex-wrap` 의 기본값은 `nowrap`

wrap으로 바꾸면 너비는 유지되고 요소들이 다음줄로 넘어간다.

줄과 줄 사이의 간격을 조절하는 방법은 `align-content` 

`align-content`를 flex-start로 하면 줄 간격이 사라진다. `center`는 화면의 가운데

```css
.parent {
  display: flex;
  /* main axis */
  justify-content: space-evenly;
  /* cross axis */
  align-items: flex-start;
  /* flex-wrap */
  flex-wrap: wrap;
  align-content: space-between;
  height: 150vh;
}
```

`flex-flow` 속성은 row wrap, column wrap 과 같이 direction과 한 번에 적용 가능하다.

### 1.7 flex-grow, flex-shrink

flex-grow, flex-shrink은 자식에게 주는 속성

#### flex-shrink

기본값 1. 화면의 크기가 줄어들어 너비가 줄어들을 때, 요소별로 그 너비가 줄어드는 정도를 조절해줄 수 있다.

숫자가 클수록 더 많이 줄어든다.

#### flex-grow

shrink와 비슷하지만 반대의 기능이다.

요소 사이의 빈 공간을 채운다.

기본값은 0.

요소별로 숫자를 지정하면 더 큰 숫자를 지닌 요소가 주변 공간을 더 많이 가져간다.

둘다 반응형 사이트를 만들 때 유용하다.

### 1.8 flex-basis

자식요소에 적용.

어떤 공간이 찌그러지거나 늘어나기전의 크기.

메인축을 기준으로 작동한다. row면 width, column이면 height

많이 쓰이진 않는다.

## CSS grid

### 2.0 Life Before Grid

flexbox 만으로극 격자 무늬를 만들기 어렵다.

### 2.1 CSS Grid Basic Concepts

grid도 기본적으로 부모 요소에서 시작한다.

```css
.parent {
  display: grid;
  /* column의 개수 및 크기 */
  grid-template-columns: 250px 250px 250px;
  /* row의 개수 및 크기 */
  grid-template-rows: 250px 250px 250px;
  /* column의 간격 */
  column-gap: 10px;
  /* row의 간격 */
  row-gap: 10px;
}
```

### 2.2 Grid Template Areas

repeat(개수, 크기) 함수

위와 아래는 같다.
```css
.grid {
  display: grid;
  grid-template-columns: 200px 200px 200px 200px;
}
```

```css
.grid {
  display: grid;
  grid-template-columns: repeat(4, 200px);
}
```

```css
.grid {
  display: grid;
  grid-template-columns: repeat(4, 200px);
  grid-template-rows: repeat(4, 200px);
  /* 콤마를 쓰지 않는다. */
  grid-template-areas:
    "header header header header"
    "content content content nav"
    "content content content nav"
    "footer footer footer footer";
}

.header {
  background: green;
  /* string으로 적지 않는다. */
  grid-area: header;
}

.content {
  background: yellow;
  grid-area: content;
}

.nav {
  background: red;
  grid-area: nav;
}

.footer {
  background: blue;
  grid-area: footer;
}
```

지정한 영역대로 css가 적용된다.

### 2.3 Rows and Columns

<img src="./assets/grid-example.png" />

숫자는 컬럼이나 로우가 아니라 grid의 선이다.

즉, 1칸을 선택하려면 start는 1, end는 2가 되어야 한다.

```css
.grid {
  display: grid;
  gap: 10px;
  grid-template-columns: repeat(4, 100px);
  grid-template-rows: repeat(4, 100px);
}

.header {
  background: green;
  /* 컬럼이 아니라 line */
  /* grid에 그어진 줄을 1번부터 센다. 아래 코드는 네 칸을 차지한다. */
  grid-column-start: 1;
  grid-column-end: 5;
}
.content {
  background: yellow;
  grid-column-start: 1;
  grid-column-end: 4;
  grid-row-start: 2;
  grid-row-end: 4;
}

.nav {
  background: red;
  grid-row-start: 2;
  grid-row-end: 4;
}

.footer {
  background: blue;
  grid-column-start: 1;
  grid-column-end: 5;
}

```

### 2.4 Shortcuts

grid start, end를 한 번에 처리할 수 있다.

```css
.grid {
  display: grid;
  gap: 10px;
  grid-template-columns: repeat(4, 100px);
  grid-template-rows: repeat(4, 100px);
}

.header {
  background: green;
  /* 컬럼이 아니라 line */
  /* start 1, end 5 */
  grid-column: 1 / 5;
}
.content {
  background: yellow;
  grid-column: 1 / 4;
  grid-row: 2 / 4;
}

.nav {
  background: red;
  grid-row: 2 / 4;
}

.footer {
  background: blue;
  grid-column: 1 / 5;
}
```

line수를 직접 세는 것보다 시작, 마지막 이런 식으로 적는 게 낫다.

즉, line이 몇 개가 생길지는 모르지만, 마지막, 혹은 마지막 전까지 생성하고 싶다. 그러면 -1, -2 등으로 쓴다.

```css
.grid {
  display: grid;
  gap: 10px;
  grid-template-columns: repeat(4, 100px);
  grid-template-rows: repeat(4, 100px);
}

.header {
  background: green;
  /* 컬럼이 아니라 line */
  /* grid에 그어진 줄을 1번부터 센다. 아래 코드는 네 칸을 차지한다. */
  /* -1은 마지막 줄, -2는 마지막 그 다음 */
  grid-column: 1 / -1;
}
.content {
  background: yellow;
  grid-column: 1 / -2;
  grid-row: 2 / -2;
}

.nav {
  background: red;
  grid-row: 2 / 4;
}

.footer {
  background: blue;
  grid-column: 1 / 5;
}
```

line이 아니라 칸 숫자로 하고 싶으면 span을 사용한다.
```css
.header {
  background: green;
  /* 컬럼이 아니라 line */
  /* span은 줄이 아니라 칸 수. 음수는 안 된다. */
  grid-column: span 4;
}
/* span을 사용할 때 시작점이 필요하면 지정할 수 있다. */
.content {
  background: yellow;
  grid-column: span 3;
  grid-row: 2 / span 2;
}
```

### 2.5 Line Naming

line에 이름을 붙여서 사용할 수도 있다.

```css
.grid {
  grid-template-columns:
    [first] 100px [second] 100px [third] 100px
    [fourth] 100px [fifth];
  grid-column: first / fourth;
}
```

### 2.6 Grid Template

fraction은 사용 가능한 공간. 

repeat(4, 1fr) 

이라고 하면 내가 설정한 grid의 width 내에서 4번 반복할 수 있는 크기고 나뉜다.

fr은 비율이다. 

화면 크기에 맞춰 자동 조절되기 때문에 반응형 웹페이지를 만들 때 유용하다.

```css
.grid {
  display: grid;
  gap: 10px;
  width: 80vw;
  height: 50vh;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(4, 1fr);
}
```

grid-template 사용하기

```css
.grid {
  display: grid;
  gap: 5px;
  height: 50vh;
  grid-template:
    /* "area" row의 길이 / 각 column의 길이  */
    "header header header header" 1fr
    "content content content nav" 2fr
    "footer footer footer footer" 1fr / 1fr 1fr 1fr 1fr;
}
```

### 2.7 Place Items

grid 컨테이너가 grid를 갖고 있고

justify-items의 기본 값은 stretch

justify-items은 수평

align-items는 수직. 기본값은 역시 stretch

stretch면 해당 grid를 가닥 채운다ㅏ.
```css
.grid {
  display: grid;
  gap: 5px;
  height: 50vh;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(4, 1fr);
  justify-items: stretch;
}
```

start, center, end 등으로 위치를 이동시킬 수 있다.

place-items: 수직 수평

을 사용하면 한 번에 할 수 있다.

```css
.grid {
  display: grid;
  justify-items: center;
  align-items: center;
}
```

```css
.grid {
  display: grid;
  place-items: center center;
}
```
### 2.9 Place content

items: grid의 cell 하나하나

content: grid 전체

justify-content의 기본값은 start

```css
.grid {
  justify-content: start;
}
```

space-around 등도 가능하다

align-content도 그렇다.

justify-content는 수평, align-content는 수직. 

```css
.grid {
  align-content: space-around;
}
```

place-content도 가능하다. 수직 수평 순

```css
.grid {
  place-content: end center;
}
```

