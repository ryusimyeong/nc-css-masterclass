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
  align-content: center;
  justify-content: center;
  place-content: center center;
}
```

### 2.10 Auto Columns and Rows

align-self는 자식 요소에게 설정한다.

justify-self도 마찬가지다.
```css
.header {
  align-self: end;
  justify-self: end;
  /* 수직, 수평 */
  place-self: end center;
}
```

auto-rows, auto-column
```css
.grid {
  display: grid;
  gap: 5px;
  grid-template-columns: repeat(4, 100px);
  grid-template-rows: repeat(4, 100px);
}
```

위처럼 설정하면 4개의 행, 열만 커버 가능하다.

grid-auto-columns 혹은 grid-auto-rows를 사용하면 데이터베이스에서 가져오는 요소에 맞춰서 행과 열을 생성

```css
.grid {
  display: grid;
  gap: 5px;
  grid-template-columns: repeat(4, 100px);
  grid-auto-rows: 100px;
}
```

```css
.grid {
  display: grid;
  gap: 5px;
  grid-template-columns: repeat(4, 100px);
  grid-template-rows: repeat(4, 100px);
  grid-auto-flow: column;
}
```

그리드가 자동생성되는 방향을 바꾸고 싶다면 

grid-auto-flow를 사용한다. default는 row이다.

### 2.11 minmax

요소가 가능한 커지길 바라지만 최소 크기를 갖길 원할 때 사용

```css
.grid {
  display: grid;
  gap: 5px;
  grid-template-columns: repeat(10, 1fr);
  grid-template-rows: repeat(4, 100px);
  grid-auto-columns: 100px;
}
```

위의 코드에서 1fr은 화면의 크기에 따라 크기가 달라진다.

화면이 작아져도 박스의 크기를 일정이상 유지하고 싶을 때 minmax()를 사용한다.

```css
.grid {
  display: grid;
  gap: 5px;
  /* minmax(최소, 최대) */
  grid-template-columns: repeat(10, minmax(100px, 1fr));
  grid-template-rows: repeat(4, 100px);
  grid-auto-columns: 100px;
}
```

### 2.12 auto-fit auto-fill

반응형 웹을 만들 떄 필요하다.

```css
.grid:first-child {
  grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
}

.grid:last-child {
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
}
```

auto-fill

우리가 준 사이즈 안에서 최대한 많은 column을 생성한다.

auto-fit

현재 row에 있는 요소들을 화면에 맞춰 크기를 조절한다. 

화면을 키우면 auto-fill을 한 요소는 빈 컬럼이 늘어나고

auto-fit한 요소는 빈 컬럼이 아니라 요소들의 크기가 화면에 맞춰 늘어난다.

### 2.13 min-content max-content

max-content

박스가 content 크기만큼 커진다.

min-content

박스가 작아질 수 있을만큼 작아진다.

```css
.grid {
  grid-template-columns: max-content min-content;
}
```

minmax와 활용해서 최소값을 max-content, 최대값을 원하는 값으로 하면 좋다.

### 3.0 CSS Preprocessors and Set Up

SCSS 

CSS 전처리기. 

SCSS를 compile 해서 CSS 파일로 만든다.

CSS를 프로그래밍 언어처럼 사용할 수 있다. 변수나 함수 등을 사용할 수 있다.

compile과 build가 필요하다. 

### 3.1 Variables and Nesting

gulp는 src 내 styles.scss 파일을 보고 있다.

이 scss 파일이 complile 되면 dist 폴더 내의 css 파일로 변환된다.

variables

SCSS 는 변수를 사용하여 CSS를 제어할 수 있다.

가장 중요하거나 반복되는 요소를 저장해서 사용한다. 

scss 파일을 `_variables.scss` 처럼 언더바를 앞에 붙이면 css로 컴파일 되지 않는다. 

변수를 저장해둘 파일을 따로 만든다. 

**_variables.scss**

```scss
// $를 이용해서 변수 생성
$bg: #e74c3c;
```

해당 파일을 import 한다.

**styles.scss**

```scss
// 변수 파일 import
@import "_variables";

body {
  background: $bg;
}
```

**nesting**

```scss
.box {
  margin-top: 20px;
}

.box h2 {
  color: blue;
}

.box:hover {
  background-color: green;
}
```

이런 식의 코드를

```scss
.box {
  margin-top: 20px;

  h2 {
    color: blue;
  }

  &:hover {
    background-color: green;
  }
}
```

이렇게 작성할 수 있다.

**&**은 자기 자신을 뜻한다.

### 3.2 Mixins

상황에 따라 다르게 코딩을 하고 싶으면 사용한다.

scss 구문 덩어리를 재사용하는 것

**_mixins.scss** 파일을 만들고 아래 구문을 작성한다. 

```scss
@mixin sexyTitle {
  color: blue;
  font-size: 30px;
  margin-bottom: 10px;
}
```

**styles.scss**

```scss
@import "_mixins";

h2 {
  @include sexyTitle();
}
```

mixins 파일을 import. mixin을 사용할 때 @include 어노테이션 사용. 함수를 실행하듯 ()로 로드.

변수 또한 사용 가능하다.

mixin을 만들 때는 **@mixin** 사용할 때는 **@include**

#### mixins.scss

```scss
@mixin link($color) {
  text-decoration: none;
  display: block;
  color: $color;
}
```

#### styles.scss

```scss
a {
  margin-bottom: 10px;
  &:nth-child(odd) {
    @include link(blue);
  }

  &:nth-child(even) {
    @include link(red);
  }
}
```

**if - else** 문도 가능하다.

#### mixins.scss

```scss
@mixin link($word) {
  text-decoration: none;
  display: block;
  @if $word == "odd" {
    color: purple;
  } @else {
    color: yellow;
  }
}
```

#### styles.scss

```scss
a {
  margin-bottom: 10px;
  &:nth-child(odd) {
    @include link("odd");
  }

  &:nth-child(even) {
    @include link("even");
  }
}
```

### 3.3 Extends

같은 코드를 중복해서 사용하고 싶지 않을 때 사용한다.

페이지에서 분리해야 하는 요소들이 많을 때 유용하다. 버튼, 타이틀, 카드, 네비게이션 등

익스텐드로 사용할 것을 선언할 때는 **%**를 사용하고, 그 설정을 사용할 때는 **@extend** 어노테이션을 사용한다.

#### _button.scss

```scss
// extend 사용하기 "%"
%button {
  font-family: inherit;
  border-radius: 7px;
  font-size: 12px;
  text-transform: uppercase;
  padding: 5px 10px;
  background: peru;
  color: white;
  font-weight: 500;
}
```

#### styles.scss

```scss
@import "_button";

a {
  // extend 요소 사용하기.
  @extend %button;
  // 공통된 프로퍼티는 extend로 처리하고 별도로 처리해줄 건 따로 작성해준다.
  text-decoration: none;
}

button {
  @extend %button;
  border: none;
}
```

### 3.4 Awesome Mixins and Conclusions

**content** 어노테이션

#### _mixins.scss

```scss
@mixin responsive {
  @content;
}
```

위와 같이 mixin 안에 `@content`를 선언하면

#### styles.scss

```scss
@import "_mixins";

a {
  @include responsive {
    text-decoration: none;
    color: red;
  }
}
```

include로 사용해서 선언한 것들의 프로퍼티가 적용된다.

반응형을 만들 때 유용하다.

#### _mixins.scss

```scss
$minIphone: 500px;
$maxIphone: 690px;
$minTablet: 501px;
$maxTablet: 1120px;

@mixin responsive($device) {
  @if $device == "iphone" {
    @media screen and (min-width: $minIphone) and (max-width: $maxIphone) {
      @content;
    }
  } @else if $device == "tablet" {
    @media screen and (min-width: $minTablet) and (max-width: $maxTablet) {
      @content;
    }
  } @else if $device == "iphone-l" {
    @media screen and (min-width: $minIphone) and (max-width: $maxIphone) and (orientation: landscape) {
      @content;
    }
  } @else if $device == "ipad-l" {
    @media screen and (min-width: $minIphone) and (max-width: $maxIphone) and (orientation: landscape) {
      @content;
    }
  }

```

#### styles.scss

```scss
@import "_mixins";

h1 {
  color: red;
  @include responsive("iphone") {
    color: yellow;
  }
  @include responsive("iphone-l") {
    font-size: 60px;
  }
  @include responsive("tablet") {
    color: green;
  }
}
```

### 4.2 Best Horror Scenes Comment

사이드바 고정하기 -> main 콘텐츠에 사이드바 크기만큼 margin left 혹은 right를 준다. 

그리고 사이드바를 position fixed 한다.

#### styles.scss

```scss
@import "_variables";

* {
  box-sizing: border-box;
}

body {
  height: 100vh;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  background-color: $white;
}

header {
  position: fixed;
  top: 0;
  left: 0;
  width: $fixedWidth;
  height: 100%;
  padding: 5vh 0 100px 72px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  color: $red;
  h1 {
    font-size: 85px;
    width: 50%;
    // 영어를 실수 없이 반드시 대문자로 바꾸고 싶을 때 사용
    text-transform: uppercase;
    // 자간
    // 단어 간격은 word-spacing
    letter-spacing: 5px;
    margin-bottom: 40px;
  }
  h3 {
    font-size: 30px;
    font-weight: 300;
    margin-bottom: 40px;
  }
}

h3,
p {
  width: 70%;
  line-height: 1.2;
  // 문단 설정. 좌로, 중앙, 우로 정렬 등
  text-align: justify;
}

p {
  font-weight: 300;
  font-size: 22px;
  margin-bottom: 40px;
}

nav {
  width: 80%;
  ul {
    display: flex;
    flex-wrap: wrap;
    li {
      cursor: pointer;
      margin-right: 12px;
      font-size: 20px;
      color: black;
      opacity: 0.5;
      padding-bottom: 5px;
      border-bottom: 2px solid rgba(0, 0, 0, 1);
      margin-bottom: 20px;
      &:hover {
        opacity: 1;
      }
    }
  }
}

main {
  margin-left: $fixedWidth;
  .movie {
    // 위에서 아래로 음영
    background: linear-gradient(
        to bottom,
        rgba(0, 0, 0, 0.1) 2%,
        transparent,
        transparent,
        transparent,
        transparent
      )
      $red;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    .wrapper {
      width: 80%;
      display: flex;
      flex-direction: column;
      .movie__header {
        display: flex;
        justify-content: space-between;
        align-items: flex-end;
        margin-bottom: 25px;
      }
      h4 {
        font-size: 32px;
        text-transform: uppercase;
      }
      h5 {
        letter-spacing: 2px;
      }
    }
  }
  img {
    width: 100%;
    box-shadow: 0 80px 80px -80px #000, 0 0 12px rgba(0, 0, 0, 0.06),
      inset 0 0 0 1px rgba(0, 0, 0, 0.2);
  }
}

```

#### _variables.scss

```scss
$red: #e7473c;
$white: #f0eff0;
$fixedWidth: 33%;
```

#### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="dist/css/reset.css" />
    <link rel="stylesheet" href="dist/css/styles.css" />
    <title>(S)CSS Masterclass</title>
  </head>
  <body>
    <header>
      <h1>Best Horror Scenes</h1>
      <div class="bottom">
        <h3>
          An ever growing collection featuring some of the best scenes in
          horror.
        </h3>
        <p>
          “Best Horror Scenes” is a collection of scenes I feel are some of the
          most affecting in horror. Some may be simple black cat scares, others
          may be more subdued or nuanced. Many come from films that aren't
          necessarily “horror” but have elements or threads of horror, and all
          have the same general effect: unease, dread, fear, shock, disgust.
        </p>
        <nav>
          <ul>
            <li>Watch on YouTube</li>
            <li>Suggest a Scene</li>
            <li>Get Episode Notices</li>
            <li>Contact</li>
            <li>RSS</li>
          </ul>
        </nav>
      </div>
    </header>
    <main>
      <section class="movie">
        <div class="wrapper">
          <div class="movie__header">
            <h4>38. Hereditary (2018)</h4>
            <h5>Directed by Me</h5>
          </div>
          <img src="./assets/sample.png" alt="sample" />
        </div>
      </section>
      <section class="movie">
        <div class="wrapper">
          <div class="movie__header">
            <h4>38. Hereditary (2018)</h4>
            <h5>Directed by Me</h5>
          </div>
          <img src="./assets/sample.png" alt="sample" />
        </div>
      </section>
      <section class="movie">
        <div class="wrapper">
          <div class="movie__header">
            <h4>38. Hereditary (2018)</h4>
            <h5>Directed by Me</h5>
          </div>
          <img src="./assets/sample.png" alt="sample" />
        </div>
      </section>
      <section class="movie">
        <div class="wrapper">
          <div class="movie__header">
            <h4>38. Hereditary (2018)</h4>
            <h5>Directed by Me</h5>
          </div>
          <img src="./assets/sample.png" alt="sample" />
        </div>
      </section>
    </main>
  </body>
</html>

```

### 4.4 Paint Box

#### styles.scss

```scss
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,500&display=swap");
@import url("https://fonts.googleapis.com/css?family=Caladea:400&display=swap");
@import "_titles";
@import "_variables";

* {
  box-sizing: border-box;
}

a {
  text-decoration: none;
  color: inherit;
  @extend %miniTitle;
}

body {
  font-family: "Caladea";
  padding-top: 70px;
}

// body 내 .footer를 제외한 모든 요소
// > 없이 하면 모든 요소가 되니까 직계 자손인 것들만 선택
body > *:not(.footer) {
  padding: 0px 140px;
}

header {
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
  width: 100%;
  padding: 0 140px;
  background-color: white;
  height: 70px;
  display: flex;
  align-items: center;
  nav {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    ul {
      display: flex;
      text-transform: uppercase;
      font-size: 10px;
      @extend %miniTitle;
      &:first-child {
        li {
          margin-right: 60px;
        }
      }
    }
  }
}

.hero {
  height: 100vh;
  background-image: linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)),
    url("https://images.unsplash.com/photo-1583248369069-9d91f1640fe6?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1352&q=80");
  background-size: cover;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: white;
  h4 {
    @extend %miniTitle;
    margin-bottom: 30px;
  }

  h3 {
    font-size: 48px;
    width: 35%;
    text-align: center;
    margin-bottom: 50px;
  }

  a {
    width: 10%;
    background-color: white;
    padding: 20px 0;
    border-radius: 5px;
    text-align: center;
    text-decoration: none;
    color: black;
    @extend %miniTitle;
    font-size: 10px;
    // 버튼 애니메이션
    transition: color 0.3s linear, background-color 0.3s linear;
    &:hover {
      background-color: black;
      color: white;
    }
  }
}

.under-hero {
  height: 80vh;
  display: flex;
  width: 100%;
  margin-bottom: 80px;

  img,
  div {
    width: 50%;
  }

  .under-hero__content {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: $bg;
    .wrapper {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      h4 {
        @extend %miniTitle;
        margin-bottom: 30px;
      }
      h3 {
        font-size: 32px;
        text-align: center;
        margin-bottom: 50px;
      }
      a {
        border: 1px solid black;
        padding: 20px;
      }
    }
  }
}

.blog {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: repeat(3, 60vh);
  margin-bottom: 80px;
  .blog__post {
    background-color: $bg;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    // order를 활용해서 엇갈리는 grid
    &:nth-child(even) {
      img {
        order: 1;
      }
    }
    img {
      width: 100%;
      height: 100%;
    }
    .post__content {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      .post__date {
        @extend %miniTitle;
        margin-bottom: 70px;
      }
      h4 {
        font-size: 32px;
        margin-bottom: 40px;
      }
    }
  }
}

.gallery {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(2, 1fr);
  .gallery__poster {
    cursor: pointer;
    height: 100%;
    img {
      max-width: 100%;
      height: 100%;
      transition: opacity 0.3s linear;
      &:hover {
        opacity: 0.5;
      }
    }
  }
}

.footer {
  margin-top: 100px;
  background-color: $bg;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  padding: 65px 0;
  .footer__column {
    display: flex;
    flex-direction: column;
    align-items: center;
    @extend %miniTitle;
    .column__title {
      margin-bottom: 50px;
      opacity: 0.5;
    }
    ul {
      text-align: center;
      li {
        margin-bottom: 15px;
      }
    }

    &:nth-child(2) {
      border-right: 1px solid black;
      border-left: 1px solid black;
    }
  }
}

```

#### _variables.scss

```scss
$bg: #f3ede8;
$sideSpace: 140px;

```

#### _titles.scss

```scss
%miniTitle {
  font-family: "Montserrat";
  font-weight: 500;
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 2px;
}

```

#### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="dist/css/reset.css" />
    <link rel="stylesheet" href="dist/css/styles.css" />
    <title>(S)CSS Masterclass</title>
  </head>
  <body>
    <header>
      <nav>
        <ul>
          <li>Nail Studios</li>
          <li>Shop Polish</li>
        </ul>
        <ul>
          <li>Journal</li>
        </ul>
      </nav>
    </header>
    <div class="hero">
      <h4>The Uptown Collection</h4>
      <h3>
        Meet our newest nails, designed in collaboration with our friends on the
        Upper East Side.
      </h3>
      <a href="#">Read More</a>
    </div>
    <section class="under-hero">
      <img src="./assets/sample.png" alt="sample" />
      <div class="under-hero__content">
        <div class="wrapper">
          <h4>The Studio</h4>
          <h3>
            Book a manicure at our Soho flagship studio or our new Uptown
            studio, 20 East 69th Street at Madison Avenue.
          </h3>
          <a href="#">Book a Manicure</a>
        </div>
      </div>
    </section>
    <section class="blog">
      <article class="blog__post">
        <img src="./assets/sample.png" />
        <div class="post__content">
          <span class="post__date">Feb 25, 2020</span>
          <h4>New and Now: The Uptown Collection</h4>
          <a href="#">Read Story</a>
        </div>
      </article>
      <article class="blog__post">
        <img src="./assets/sample.png" />
        <div class="post__content">
          <span class="post__date">Feb 25, 2020</span>
          <h4>New and Now: The Uptown Collection</h4>
          <a href="#">Read Story</a>
        </div>
      </article>
      <article class="blog__post">
        <img src="./assets/sample.png" />
        <div class="post__content">
          <span class="post__date">Feb 25, 2020</span>
          <h4>New and Now: The Uptown Collection</h4>
          <a href="#">Read Story</a>
        </div>
      </article>
    </section>
    <section class="gallery">
      <div class="gallery__poster">
        <img src="./assets/sample.png" alt="" />
      </div>
      <div class="gallery__poster">
        <img src="./assets/sample.png" alt="" />
      </div>
      <div class="gallery__poster">
        <img src="./assets/sample.png" alt="" />
      </div>
      <div class="gallery__poster">
        <img src="./assets/sample.png" alt="" />
      </div>
      <div class="gallery__poster">
        <img src="./assets/sample.png" alt="" />
      </div>
      <div class="gallery__poster">
        <img src="./assets/sample.png" alt="" />
      </div>
      <div class="gallery__poster">
        <img src="./assets/sample.png" alt="" />
      </div>
      <div class="gallery__poster">
        <img src="./assets/sample.png" alt="" />
      </div>
    </section>
    <footer class="footer">
      <div class="footer__column">
        <span class="column__title">Support</span>
        <ul>
          <li>F.A.Q.</li>
          <li>Privacy Policu</li>
          <li>Terms and Conditions</li>
          <li>Accessibility</li>
        </ul>
      </div>
      <div class="footer__column">
        <span class="column__title">Follow Us</span>
        <ul>
          <li>Instagram</li>
          <li>Twitter</li>
        </ul>
      </div>
      <div class="footer__column">
        <span class="column__title">Support</span>
        <ul>
          <li>F.A.Q.</li>
          <li>Privacy Policu</li>
          <li>Terms and Conditions</li>
          <li>Accessibility</li>
        </ul>
      </div>
    </footer>
  </body>
</html>

```

### 4.6 10x19 Comment

body background-color 와 grid gap 을 이용해서 화면 전체에 border를 줄 수 있다.

#### styles.scss

````scss
@import "_variables";

* {
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  height: 100vh;
  background-color: $bg;
  display: grid;
  gap: 1px;
  grid-template-columns: 1.5fr 1.9fr 1.5fr;
  grid-template-rows: 1fr 5fr 1fr;
  & > * {
    background-color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    color: $bg;
    font-size: 22px;
    text-transform: uppercase;
  }
  .menu {
    grid-column-start: -2;
  }
  .center-image {
    grid-column: 2 / -2;
    grid-row: 2 / -2;
    background-image: url("https://images.unsplash.com/photo-1583309219338-a582f1f9ca6b?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1364&q=80");
    background-size: cover;
    background-position: center;
  }
  .number__row {
    background-color: $bg;
    display: grid;
    grid-template-columns: 1fr;
    gap: 1px;
    height: 100%;
    align-items: stretch;
    .number {
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: white;
      cursor: pointer;
      transition: color 0.3s linear, background-color 0.3s linear;
      &:hover {
        background-color: $bg;
        color: white;
      }
    }
  }
  .scrolling__text {
    grid-column-start: 2;
    white-space: nowrap;
    overflow: hidden;
    // 애니메이션
    span {
      animation: scrollText 3s linear infinite forwards;
    }
  }
}

@keyframes scrollText {
  0% {
    transform: translateX(-150px);
  }
  50% {
    transform: translateX(150px);
  }
  100% {
    transform: translateX(-150px);
  }
}
````

#### _variables.scss

````scss
$bg: #af7732;
````

#### index.html

````html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="dist/css/reset.css" />
    <link rel="stylesheet" href="dist/css/styles.css" />
    <title>(S)CSS Masterclass</title>
  </head>
  <body>
    <span></span>
    <span></span>
    <span class="menu">Menu</span>
    <div class="number__row">
      <div class="number">#10</div>
      <div class="number">#9</div>
      <div class="number">#8</div>
      <div class="number">#7</div>
      <div class="number">#6</div>
    </div>

    <div class="number__row">
      <div class="number">#5</div>
      <div class="number">#4</div>
      <div class="number">#3</div>
      <div class="number">#2</div>
      <div class="number">#1</div>
    </div>
    <div class="center-image"></div>
    <span></span>
    <div class="scrolling__text">
      <span>
        This is a very long text that should scroll using CSS3 Animations and
        not JS
      </span>
    </div>
    <span></span>
  </body>
</html>
````

### 4.7 Zoo

CSS는 같은 속성에 다른 값을 지정하면 나중에 입력한 값을 적용한다.

!important 키워드를 붙이면 이런 현상을 막고, 키워드가 적용된 속성을 적용한다.

#### styles.scss

```scss
@import "_variables";

* {
  box-sizing: border-box;
}

body {
  padding: 20px 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}

header {
  width: 100%;
  position: fixed;
  top: 0;
  height: 50px;
  background-color: white;
  display: flex;
  align-items: center;
  nav {
    width: 100%;
    height: 100%;
    display: grid;
    grid-template-columns: 2fr 1fr;
    font-size: 32px;
    text-transform: lowercase;
    ul {
      display: flex;
      align-items: center;
      padding: 0px 15px;
      &:hover {
        background-color: gainsboro;
      }
      li {
        cursor: pointer;
        margin-right: 50px;
      }
      &:first-child {
        &:hover {
          li:not(:first-child) {
            // 나중에 다른 값이 작성되더라도 white로 유지
            color: white !important;
          }
        }
        li {
          &:first-child {
            margin-right: 120px;
          }
          &:not(:first-child) {
            color: gainsboro;
            margin-right: 50px;
          }
        }
      }
    }
  }
}

main {
  margin-top: 50px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 45vh;
  article {
    cursor: pointer;
    height: 100%;
    display: grid;
    grid-template-rows: 10fr 0.8fr;
    img {
      min-width: 100%;
      height: 100%;
    }
    div {
      display: flex;
      align-items: center;
      text-transform: uppercase;
      padding-left: 10px;
      h3 {
        font-size: 14px;
      }
    }
  }
}

```

#### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="dist/css/reset.css" />
    <link rel="stylesheet" href="dist/css/styles.css" />
    <title>(S)CSS Masterclass</title>
  </head>
  <body>
    <header>
      <nav>
        <ul>
          <li>Zoo</li>
          <li>Contact</li>
          <li>Team</li>
          <li>Clients</li>
        </ul>
        <ul>
          <li>Projects</li>
          <li>Tours</li>
        </ul>
      </nav>
    </header>
    <main>
      <article>
        <img src="https://source.unsplash.com/random/450x450" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x451" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x452" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x453" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x454" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x455" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x456" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x457" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x458" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x459" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x460" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x461" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x462" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x463" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
      <article>
        <img src="https://source.unsplash.com/random/450x464" />
        <div>
          <h3>Moco Montpellier Contemporain</h3>
        </div>
      </article>
    </main>
  </body>
</html>

```

### 4.9 Schwartz Coding

px로 사칙연산을 할 수 있다.

```scss
$fontMedium: 30px - 5px;
```

#### _elements.scss

```scss
@import "_variables";

%categoryTitle {
  font-weight: 600;
  font-size: 22px;
  margin-bottom: 50px;
}

%btn {
  text-decoration: none;
  color: inherit;
  border: $border;
  padding: 10px 40px;
  font-weight: 500;
  border-radius: 99px;
  transition: background-color 0.2s linear;
  &:hover {
    background-color: black;
    color: white;
  }
}

```

#### _variables.scss

```scss
$fontMedium: 30px;
$border: 0.5px solid rgba(0, 0, 0, 0.3);

```

#### styles.scss

```scss
@import "_variables";
@import "_elements";

* {
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}

main {
  line-height: 1.6;
  width: 55%;
  margin: 0 auto;
}

p {
  font-size: $fontMedium;
}

.hero {
  width: 100%;
  margin-top: 150px;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 150px;
  .hero__photo {
    height: 70vh;
    width: 100%;
    background-image: url("https://source.unsplash.com/random/");
    background-size: cover;
    background-position: center center;
  }
  h2 {
    font-weight: 500;
    font-size: 32px;
    margin-top: 80px;
    margin-bottom: 120px;
  }
  p {
    font-size: $fontMedium;
    span {
      // 변수를 이용한 사칙 연산이 가능하다.
      font-size: $fontMedium - 5px;
      margin-right: 50px;
      font-weight: 500;
    }
  }
}

.products {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  .product {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
    padding: 20px 0;
    border-top: $border;
    grid-column-start: span 2;
    &:nth-child(even) {
      div {
        order: 1;
      }
    }
    p {
      margin-bottom: 50px;
    }
    .product__category {
      @extend %categoryTitle;
    }
  }
  .line {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-column-start: span 2;
    gap: 10px;
    .product {
      grid-template-columns: 1fr;
      grid-column-start: span 1;
      p {
        font-size: 22px;
        margin-top: 30px;
      }
    }
  }
}

.links {
  margin-top: 100px;
  display: grid;
  border-top: $border;
  padding-top: 20px;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-bottom: 200px;
  .link {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    h4 {
      @extend %categoryTitle;
      margin-bottom: 30px;
    }
    span {
      font-size: 22px;
      margin-bottom: 20px;
    }
  }
}

a.btn {
  @extend %btn;
}

footer {
  background-color: #4d4c4c;
  width: 100%;
  padding: 100px 0;
  .footer__top {
    width: 55%;
    margin: auto;
    color: white;
    display: grid;
    grid-template-columns: 1.5fr 1fr;
    span {
      font-size: 38px;
    }
    ul {
      width: 100%;
      display: flex;
      li {
        margin-right: 10px;
      }
    }
  }
}

```

#### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="dist/css/reset.css" />
    <link rel="stylesheet" href="dist/css/styles.css" />
    <title>(S)CSS Masterclass</title>
  </head>
  <body>
    <main>
      <div class="hero">
        <div class="hero__photo"></div>
        <h2>News that lasts.</h2>
        <p>
          <span>About</span> Schwartz Media publishes intelligent news and
          current affairs that breaks the 24-hour news cycle. We offer a nuanced
          examination of Australia and the world, focused on fresh insight and
          literary expression. Our audience reads to know, not just to agree. We
          invest in long-form journalism where the issues demand it, providing
          writing of a quality that makes difficult topics clear. Schwartz Media
          publishes Australia’s most respected writers across The Saturday
          Paper, The Monthly magazine and the daily podcast 7am, alongside our
          sister publications, Quarterly Essay and Australian Foreign Affairs.
        </p>
      </div>
      <section class="products">
        <article class="product">
          <div>
            <h4 class="product__category">Journalism</h4>
            <p class="product__description">
              Our journalists create in-depth, independent, original public
              interest reporting, focusing on storytelling and insight.
            </p>
            <a href="#" class="btn">Learn more</a>
          </div>
          <img src="https://source.unsplash.com/random/500x360" />
        </article>
        <article class="product">
          <div>
            <h4 class="product__category">Journalism</h4>
            <p class="product__description">
              Our journalists create in-depth, independent, original public
              interest reporting, focusing on storytelling and insight.
            </p>
            <a href="#" class="btn">Learn more</a>
          </div>
          <img src="https://source.unsplash.com/random/500x360" />
        </article>
        <article class="product">
          <div>
            <h4 class="product__category">Journalism</h4>
            <p class="product__description">
              Our journalists create in-depth, independent, original public
              interest reporting, focusing on storytelling and insight.
            </p>
            <a href="#" class="btn">Learn more</a>
          </div>
          <img src="https://source.unsplash.com/random/500x360" />
        </article>
        <article class="product">
          <div>
            <h4 class="product__category">Journalism</h4>
            <p class="product__description">
              Our journalists create in-depth, independent, original public
              interest reporting, focusing on storytelling and insight.
            </p>
            <a href="#" class="btn">Learn more</a>
          </div>
          <img src="https://source.unsplash.com/random/500x360" />
        </article>
        <div class="line">
          <article class="product">
            <div>
              <h4 class="product__category">Journalism</h4>
              <img src="https://source.unsplash.com/random/500x360" />
              <p class="product__description">
                Our journalists create in-depth, independent, original public
                interest reporting, focusing on storytelling and insight.
              </p>
              <a href="#" class="btn">Learn more</a>
            </div>
          </article>
          <article class="product">
            <div>
              <h4 class="product__category">Journalism</h4>
              <img src="https://source.unsplash.com/random/500x360" />
              <p class="product__description">
                Our journalists create in-depth, independent, original public
                interest reporting, focusing on storytelling and insight.
              </p>
              <a href="#" class="btn">Learn more</a>
            </div>
          </article>
        </div>
      </section>
      <div class="links">
        <div class="link">
          <h4>Careers</h4>
          <span>Work at the country’s leading independent publisher. </span>
          <a href="#" class="btn">Learn more</a>
        </div>
        <div class="link">
          <h4>Careers</h4>
          <span>Work at the country’s leading independent publisher. </span>
          <a href="#" class="btn">Learn more</a>
        </div>
        <div class="link">
          <h4>Careers</h4>
          <span>Work at the country’s leading independent publisher. </span>
          <a href="#" class="btn">Learn more</a>
        </div>
      </div>
    </main>
    <footer>
      <div class="footer__top">
        <span>Schwartz</span>
        <ul>
          <li>Schwartz</li>
          <li>Schwartz</li>
          <li>Schwartz</li>
        </ul>
      </div>
    </footer>
  </body>
</html>

```

### 4.11 Tolv

글자 중 가운데 글자만 transform 하는 것

#### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="dist/css/reset.css" />
    <link rel="stylesheet" href="dist/css/styles.css" />
    <title>(S)CSS Masterclass</title>
  </head>
  <body>
    <header>
      <nav>
        <ul>
          <li>Products</li>
          <li>Stockists</li>
          <li>About us</li>
        </ul>
      </nav>
      <!-- 글자 중간만 스타일링 하기 -->
      <h1 class="logo">
        T
        <div>o</div>
        lv
      </h1>
      <span>👀</span>
    </header>
    <main>
      <div class="hero">
        <div class="hero__img"></div>
        <div class="hero__text">
          <h2>
            Lift the blind to let in the light. A moment of calm before the day
            begins.
          </h2>
          <span>
            Featuring
            <a href="#">Cherry Sofa</a>
            and
            <a href="#">Kile Coffee Table</a>
          </span>
        </div>
      </div>
      <div class="banner">
        <h3 class="banner__title">Time for Living</h3>
        <p>
          Take time for life’s little moments. Browsing the news as you eat
          breakfast. Setting the table for hungry guests. Sinking in to your
          favourite armchair. At Tolv, your daily rituals are at the heart of
          our design. We make furniture to give you your best day, every day.
        </p>
        <span>
          Find out more
          <a href="#">About us</a>
        </span>
      </div>
      <section class="gallery">
        <div class="gallery__item"></div>
        <div class="gallery__item"></div>
        <div class="gallery__item"></div>
        <div class="gallery__item"></div>
        <div class="gallery__item"></div>
        <div class="gallery__item"></div>
        <div class="gallery__item"></div>
        <div class="gallery__item"></div>
        <div class="gallery__item"></div>
        <div class="gallery__item"></div>
        <div class="gallery__item"></div>
        <div class="gallery__item"></div>
      </section>
    </main>
  </body>
</html>

```

#### _variables.scss

```scss
$orange: #ff6429;
$bg: #efcb56;
```

#### _styles.scss

```scss
@import url("https://fonts.googleapis.com/css?family=Yrsa:400,500&display=swap");
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,600&display=swap");
@import "_variables";

* {
  box-sizing: border-box;
}

body {
  font-family: "Montserrat", -apple-system, BlinkMacSystemFont, "Segoe UI",
    Roboto, Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  margin-top: 60px;
}

header {
  position: fixed;
  top: 0;
  left: 0;
  height: 60px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  align-items: center;
  width: 100%;
  padding: 0px 10%;

  h1 {
    place-self: center center;
    font-family: "Yrsa";
  }
  > span {
    justify-self: end;
  }
  nav {
    ul {
      display: flex;
      font-family: "Montserrat", sans-serif;
      // li 요소 중 마지막 요소를 제외하고
      li:not(:last-chlid) {
        margin-right: 10px;
      }
    }
  }
  .logo {
    font-size: 48px;
    font-weight: 500;
    display: flex;
    // 네 개의 글자 중 하나만 방향 틀기
    div {
      transform: rotateZ(-15deg);
      margin: 0px -3px;
    }
  }
}

.hero {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: calc(100vh - 60px);
  .hero__img {
    background-image: url("https://source.unsplash.com/random/");
    background-size: cover;
    background-position: center center;
  }
  .hero__text {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    h2 {
      font-family: "Yrsa";
      font-size: 52px;
      text-align: center;
      width: 60%;
      font-weight: 500;
      margin-bottom: 40px;
    }
    span {
      font-size: 12px;
    }
  }
}

a {
  font-weight: 600;
  color: $orange;
}

.banner {
  background-color: $bg;
  height: 50vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  h3 {
    font-family: "Yrsa";
    font-size: 56px;
    margin-bottom: 30px;
  }
  p {
    width: 50%;
    text-align: center;
    font-family: "Yrsa";
    font-size: 32px;
    margin-bottom: 30px;
  }
  span {
    font-size: 12px;
  }
}

.gallery {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 50vh;
  .gallery__item {
    background-image: url("https://source.unsplash.com/random/");
    background-size: cover;
    background-position: center;
    transition: all 0.2s linear;
    cursor: pointer;
    overflow: hidden;
    &:first-child,
    &:nth-child(5),
    &:nth-child(7),
    &:nth-child(10) {
      grid-column-start: span 2;
    }
    &:hover {
      filter: blur(50px);
    }
  }
}

```

### 4.13 Rodic Davidson

#### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="dist/css/reset.css" />
    <link rel="stylesheet" href="dist/css/styles.css" />
    <title>(S)CSS Masterclass</title>
  </head>
  <body>
    <h1>Rodic Davison</h1>
    <main>
      <nav>
        <ul>
          <li>Projects</li>
          <li>Practice</li>
          <li>News</li>
          <li>Exhibition</li>
          <li>Contact</li>
        </ul>
      </nav>
      <div class="photo">
        <img src="https://source.unsplash.com/random/1" />
        <h4>Suffolk Farmstead</h4>
      </div>
      <div class="photo">
        <img src="https://source.unsplash.com/random/2" />
        <h4>Suffolk Farmstead</h4>
      </div>
      <div class="photo">
        <img src="https://source.unsplash.com/random/3" />
        <h4>Suffolk Farmstead</h4>
      </div>
      <div class="photo">
        <img src="https://source.unsplash.com/random/4" />
        <h4>Suffolk Farmstead</h4>
      </div>
      <div class="photo">
        <img src="https://source.unsplash.com/random/5" />
        <h4>Suffolk Farmstead</h4>
      </div>
      <div class="photo">
        <img src="https://source.unsplash.com/random/6" />
        <h4>Suffolk Farmstead</h4>
      </div>
      <div class="photo">
        <img src="https://source.unsplash.com/random/6" />
        <h4>Suffolk Farmstead</h4>
      </div>
    </main>
  </body>
</html>

```

#### styles.scss

```scss
@import "_variables";

* {
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  display: grid;
  grid-template-columns: 1.3fr 4fr;
  padding: 20px;
  font-size: 13px;
  align-items: start;
  h1 {
    cursor: pointer;
    font-weight: 500;
    &:hover {
      color: blue;
    }
  }
}

main {
  display: grid;
  // gap을 따로따로 넣기
  column-gap: 20px;
  row-gap: 80px;
  grid-template-columns: repeat(2, 1fr);
  nav {
    grid-column-start: span 2;
    ul {
      display: flex;
      li:not(:last-child) {
        margin-right: 10px;
      }
    }
  }
  .photo {
    &:hover {
      h4 {
        color: blue;
      }
    }
    img {
      max-width: 100%;
      margin-bottom: 10px;
    }
    h4 {
      font-size: 14px;
    }
  }
}
```

### 4.15 Beige Coding

#### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="dist/css/reset.css" />
    <link rel="stylesheet" href="dist/css/styles.css" />
    <title>(S)CSS Masterclass</title>
  </head>
  <body>
    <header class="header">
      <h1>Beigr</h1>
      <nav>
        <ul>
          <!-- 빈 span 혹은 div를 이용하여 원을 만든다. -->
          <li><span></span><a href="#">Kultur</a></li>
          <li><span></span><a href="#">Menschen</a></li>
          <li><span></span><a href="#">Reisen</a></li>
          <li><span></span><a href="#">Design</a></li>
          <li><span></span><a href="#">Mode</a></li>
          <li><span></span><a href="#">Pflege</a></li>
          <li><span></span><a href="#">Fair</a></li>
        </ul>
      </nav>
      <span>👀</span>
    </header>
    <main class="posts">
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
      <section class="post">
        <header class="post__header">
          <span class="post__date">2020.02.24</span>
          <span class="post__author">Marie Jaster</span>
        </header>
        <div class="post__content">
          <div class="visible">
            <h3>Hol dir Farbe in deine Inbox</h3>
          </div>
          <div class="invisible"></div>
        </div>
        <footer>
          <span class="category">Newsletter</span>
          <span class="comments">1개의 댓글</span>
        </footer>
      </section>
    </main>
  </body>
</html>

```

#### styles.scss

```scss
@import "_variables";

* {
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  margin-top: 40px;
}

.header {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1;
  width: 100%;
  height: 40px;
  padding: 0px 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  h1 {
    font-size: 22px;
    text-transform: uppercase;
  }
  nav {
    ul {
      display: flex;
      li {
        font-size: 20px;
        display: flex;
        align-items: center;
        &:nth-child(3n + 1) {
          span {
            background-color: #e4c464;
          }
        }
        &:nth-child(3n + 2) {
          span {
            background-color: #56854a;
          }
        }
        &:nth-child(3n + 3) {
          span {
            background-color: #97c2de;
          }
        }
        // 빈 span에 높이와 너비를 주고 border-radius: 50%; 로 동그라미를 만든다.
        span {
          margin-right: 5px;
          height: 15px;
          width: 15px;
          background-color: red;
          border-radius: 50%;
        }
        a {
          color: inherit;
          text-decoration: none;
          text-transform: uppercase;
        }
        &:not(:last-child) {
          margin-right: 20px;
        }
      }
    }
  }
}

.posts {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-auto-rows: 55vh;
  .post {
    cursor: pointer;
    padding: 20px;
    font-size: 12px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    position: relative;
    .post__header,
    footer {
      display: flex;
      justify-content: space-between;
      letter-spacing: 1px;
    }
    // 규칙성이 있게 색상 배치
    &:nth-child(5n + 1) {
      background-color: #dd433e;
    }
    &:nth-child(5n + 2) {
      background-color: #e4c874;
    }
    &:nth-child(5n + 3) {
      background-color: #198ca1;
    }
    &:nth-child(5n + 4) {
      background-color: #ec9860;
    }
    &:nth-child(5n + 5) {
      background-color: #ccb2a2;
    }
    // 마우스 올리면 이미지 출력
    .post__content {
      position: absolute;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      h3 {
        letter-spacing: 2px;
        line-height: 1.3;
        font-size: 26px;
        text-align: center;
      }
      .invisible {
        display: none;
        width: 100%;
        height: 100%;
        background-image: url("https://images.prismic.io/beige/3479dcfd-17b4-4391-8b1c-506801d60786_Beige-Mode-Fashion-Menswear-Trends-2020-Gucci-Cruise-5.jpg?auto=compress,format?auto=format,compress&q=60&fit=crop&w=1200&h=1920");
        background-position: center center;
        background-size: cover;
      }
    }
    &:hover {
      .post__content {
        .visible {
          display: none;
        }
        .invisible {
          display: block;
        }
      }
    }
  }
}

```

### 4.17 Donica Coding

#### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="dist/css/reset.css" />
    <link rel="stylesheet" href="dist/css/styles.css" />
    <title>(S)CSS Masterclass</title>
  </head>
  <body>
    <header>
      <h1>
        Donica Ida is an art director and designer working in editorial,
        identity, and digital design.
      </h1>
    </header>
    <div class="works">
      <div class="works__header">
        <span>Year</span>
        <span>Client</span>
        <span>Info</span>
      </div>
      <ul class="works__list">
        <li class="works__work">
          <span>2019</span>
          <span>Huffpost Highline</span>
          <span>Investigative journalism meets digital storytelling.</span>
        </li>
        <li class="works__work">
          <span>2019</span>
          <span>Huffpost Highline</span>
          <span>Investigative journalism meets digital storytelling.</span>
        </li>
        <li class="works__work">
          <span>2019</span>
          <span>Huffpost Highline</span>
          <span>Investigative journalism meets digital storytelling.</span>
        </li>
        <li class="works__work">
          <span>2019</span>
          <span>Huffpost Highline</span>
          <span>Investigative journalism meets digital storytelling.</span>
        </li>
        <li class="works__work">
          <span>2019</span>
          <span>Huffpost Highline</span>
          <span>Investigative journalism meets digital storytelling.</span>
        </li>
        <li class="works__work">
          <span>2019</span>
          <span>Huffpost Highline</span>
          <span>Investigative journalism meets digital storytelling.</span>
        </li>
        <li class="works__work">
          <span>2019</span>
          <span>Huffpost Highline</span>
          <span>Investigative journalism meets digital storytelling.</span>
        </li>
        <li class="works__work">
          <span>2019</span>
          <span>Huffpost Highline</span>
          <span>Investigative journalism meets digital storytelling.</span>
        </li>
        <li class="works__work">
          <span>2019</span>
          <span>Huffpost Highline</span>
          <span>Investigative journalism meets digital storytelling.</span>
        </li>
      </ul>
    </div>
    <div class="cv">
      <span>Education</span>
      MFA Design Entrepreneurship, School of Visual Arts; BFA Visual
      Communication Design, University of Washington.
      <span>Formerly at</span>
      HuffPost Highline, Mary Review, Critical Mass, Pentagram.
      <span>Select clients</span>
      Airbnb, Condé Nast Traveler, Google, Planned Parenthood.
    </div>
    <div class="about">
      <span>About</span>
      Donica Ida is a Hawaii-born designer who loves beautiful typography and a
      well-told story. She is the former Creative Director of HuffPost Highline
      and Design Director of Mary Review. Donica lives in Brooklyn with her
      <a href="#">husband</a> and splits her time between freelance work,
      traveling, hikes, and ramen. She is currently available for new
      opportunities.
      <span>Connect</span>
      <a href="#">Email</a>, <a href="#">Instagram</a>,
      <a href="#">LinkedIn</a>, <a href="#">WorkingNotWorking</a>.
    </div>
  </body>
</html>

```

#### _elements_.scss

```scss
@import "_variables";

%tinyText {
  color: $red;
  font-size: 12px;
  font-family: "Nunito";
}

%grid {
  display: grid;
  grid-template-columns: 1fr 3fr 5fr;
}

```

#### _variables_.scss

```scss
$red: #fc3f33;
$black: #444444;

```

#### styles.scss

```scss
@import url("https://fonts.googleapis.com/css?family=Nunito|PT+Serif:400,400i&display=swap");
@import "_elements";
@import "_variables";

* {
  box-sizing: border-box;
}

body {
  font-family: "PT Serif", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  background-color: #f0efeb;
  color: $black;
  padding: 30px 40px;
  line-height: 2;
}

header {
  font-size: 46px;
  letter-spacing: 1px;
  margin-bottom: 175px;
}

.works {
  margin-bottom: 80px;
  .works__header {
    @extend %grid;
    padding-bottom: 10px;
    span {
      @extend %tinyText;
    }
  }
  .works__list {
    .works__work {
      cursor: pointer;
      font-size: 20px;
      border-top: 1px solid $black;
      @extend %grid;
      &:hover {
        font-style: italic;
      }
    }
  }
}

.cv,
.about {
  font-size: 30px;
  span {
    @extend %tinyText;
  }
}

a {
  color: $red;
  &:hover {
    font-style: italic;
  }
}

.about {
  padding-bottom: 80px;
}

```

### 4.19 Canal Street

#### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="dist/css/reset.css" />
    <link rel="stylesheet" href="dist/css/styles.css" />
    <title>(S)CSS Masterclass</title>
  </head>
  <body>
    <main>
      <header>
        <h1>
          Canal Street Market is a carefully curated retail market, food hall &
          community space open year-round at 265 Canal Street.
        </h1>
        <div class="header__photo"></div>
      </header>
      <section class="about">
        <h2>A New Kind of Market</h2>
        <div class="about__columns">
          <div class="about__column">
            <div class="img__wrapper">
              <img src="https://source.unsplash.com/random/1" />
            </div>
            <span>
              Merging retail, food, art, and culture, Canal Street Market
              highlights top retail and design concepts, restaurants, and
              up-and-coming players in the downtown New York City community.
            </span>
          </div>
          <div class="about__column">
            <div class="img__wrapper">
              <img src="https://source.unsplash.com/random/2" />
            </div>
            <span
              >Merging retail, food, art, and culture, Canal Street Market
              highlights top retail and design concepts, restaurants, and
              up-and-coming players in the downtown New York City
              community.</span
            >
          </div>
          <div class="about__column">
            <div class="img__wrapper">
              <img src="https://source.unsplash.com/random/3" />
            </div>
            <span
              >Merging retail, food, art, and culture, Canal Street Market
              highlights top retail and design concepts, restaurants, and
              up-and-coming players in the downtown New York City
              community.</span
            >
          </div>
        </div>
      </section>
      <section class="events">
        <div class="events__header">
          <span>nomad</span>
          <h4>Market Events</h4>
          <span>coder</span>
        </div>
        <div class="events__list">
          <div class="events__event">
            <span class="event__date">12/11</span>
            Korean Wave
          </div>
          <div class="events__event">
            <span class="event__date">12/11</span>
            Korean Wave
          </div>
          <div class="events__event">
            <span class="event__date">12/11</span>
            Korean Wave
          </div>
        </div>
        <a href="#" class="btn">See All</a>
      </section>
      <section class="location">
        <div class="location__address">
          <h3>265 Canal St. <span>New York, NY</span></h3>
        </div>
        <div class="location__address"></div>
      </section>
      <section class="contact">
        <h4>Interested in becoming a vendor?</h4>
        <a href="#" class="btn">Click Here</a>
      </section>
    </main>
    <nav>
      <ul>
        <li><span>Food</span></li>
        <li><span>Retail</span></li>
        <li><span>Community</span></li>
      </ul>
    </nav>
  </body>
</html>

```

#### _variables.scss

```scss
$paddingLeft: 65px;

```

#### styles.scss

```scss
@import url("https://fonts.googleapis.com/css2?family=B612+Mono&family=DM+Serif+Display:ital@1&display=swap");
@import "_elements";
@import "_variables";

* {
  box-sizing: border-box;
}

body {
  font-family: "B612 Mono", monospace;
  margin-right: 180px;
  nav {
    position: fixed;
    right: 0;
    top: 0;
    width: 180px;
    ul {
      display: grid;
      grid-template-columns: repeat(3, 60px);
      grid-template-rows: 100vh;
      li {
        background-color: #f64344;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 18px;
        span {
          transform: rotateZ(-90deg);
        }
        &:first-child {
          background-color: #5da3ec;
        }
        &:last-child {
          background-color: #ffb301;
        }
      }
    }
  }
}

h1,
h2,
h3,
h4 {
  font-family: "DM Serif Display", serif;
}

main {
  header {
    margin-top: 250px;
    h1 {
      padding-left: $paddingLeft;
      font-size: 80px;
      width: 60%;
      line-height: 1.2;
      margin-bottom: 100px;
    }
    .header__photo {
      width: 100%;
      height: 120vh;
      background-image: url("https://source.unsplash.com/random/12");
      background-position: center center;
      background-size: cover;
    }
  }
}

.about {
  margin-top: 120px;
  margin-bottom: 240px;
  padding: 0px $paddingLeft;
  h2 {
    font-size: 120px;
    width: 50%;
    margin-bottom: 120px;
  }
  .about__columns {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 60px;
    .about__column {
      height: 100%;
      display: grid;
      grid-template-rows: 650px 20%;
      gap: 30px;
      .img__wrapper {
        overflow: hidden;
        img {
          max-width: 100%;
        }
      }
      span {
        font-size: 12px;
        line-height: 1.5;
      }
    }
  }
}

.events {
  padding: 0px $paddingLeft;
  display: grid;
  justify-items: center;
  margin-bottom: 120px;
  .events__header {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    place-items: center center;
    font-size: 64px;
    h4 {
      font-size: 94px;
      text-align: center;
    }
  }
  .events__list {
    margin-top: 150px;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    place-items: center center;
    width: 100%;
    .events__event {
      display: flex;
      flex-direction: column;
      align-items: center;
      .event__date {
        margin-bottom: 30px;
        font-size: 12px;
      }
    }
  }
  .btn {
    margin-top: 120px;
  }
}

.btn {
  text-transform: lowercase;
  text-decoration: none;
  color: black;
  border: 1px solid black;
  padding: 17px 60px;
  transition: background-color 0.2s linear;
  &:hover {
    color: white;
    background-color: black;
  }
}

.location {
  padding: $paddingLeft;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: 33vh;
  gap: 60px;
  .location__address {
    font-size: 68px;
    display: flex;
    justify-content: center;
    align-items: center;
    h3 {
      width: 100%;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
    border: 1px solid black;
  }
}

.contact {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin: 200px 0px;
  h4 {
    font-size: 56px;
    margin-bottom: 30px;
  }
}
```

### 4.21 One hundred

#### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="dist/css/reset.css" />
    <link rel="stylesheet" href="dist/css/styles.css" />
    <title>(S)CSS Masterclass</title>
  </head>
  <body>
    <header>
      <nav>
        <ul>
          <li>Search</li>
          <li>Won Hundred</li>
          <li>Shopping Bag (0)</li>
          <li>Journal</li>
          <li>Women</li>
          <li>Men</li>
          <li>Currency</li>
        </ul>
      </nav>
    </header>
    <main>
      <h1>Spring Summer – Volume 2</h1>
      <h6>
        Get your wardrobe ready for those upcoming warm spring days with our
        second delivery of Spring Summer 20.
      </h6>
      <div class="hero">
        <div class="hero__img"></div>
        <div class="hero__img"></div>
        <div class="hero__img"></div>
        <div class="hero__img"></div>
      </div>
      <section class="arrivals">
        <h4 class="arrivals__title">Selected New Arrivals</h4>
        <div class="wrapper">
          <article class="product">
            <div class="product__photo"></div>
            <div class="product__data">
              <span class="name">Jonah Shirt - Zen Blue</span>
              <span class="price">900 DKK</span>
            </div>
          </article>
          <article class="product">
            <div class="product__photo"></div>
            <div class="product__data">
              <span class="name">Jonah Shirt - Zen Blue</span>
              <span class="price">900 DKK</span>
            </div>
          </article>
          <article class="product">
            <div class="product__photo"></div>
            <div class="product__data">
              <span class="name">Jonah Shirt - Zen Blue</span>
              <span class="price">900 DKK</span>
            </div>
          </article>
          <article class="product">
            <div class="product__photo"></div>
            <div class="product__data">
              <span class="name">Jonah Shirt - Zen Blue</span>
              <span class="price">900 DKK</span>
            </div>
          </article>
          <span class="arrivals__category">Shop Women's New Arrivals</span>
          <span class="arrivals__category">Shop Men's New Arrivals</span>
        </div>
      </section>
    </main>
    <footer>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </footer>
  </body>
</html>

```

#### styles.scss

grid 내부에 border를 주고 싶다면 background-color를 주고 gap을 이용한다.

```scss
@import url("https://fonts.googleapis.com/css2?family=B612+Mono&family=DM+Serif+Display:ital@0;1&display=swap");
@import "_elements";
@import "_variables";

* {
  box-sizing: border-box;
}

body {
  font-family: "DM Serif Display", monospace;
  padding: 45px;
}

header {
  background-color: black;
  border: 1px solid black;
  margin-bottom: 100px;
  nav {
    ul {
      display: grid;
      gap: 1px;
      grid-template-columns: repeat(4, 1fr);
      grid-template-rows: repeat(2, 60px);
      li {
        background-color: white;
        display: flex;
        justify-content: center;
        align-items: center;
        &:nth-child(2) {
          grid-column-start: span 2;
          font-size: 32px;
          text-transform: uppercase;
        }
      }
    }
  }
}

main {
  h1,
  h6 {
    text-align: center;
  }
  h1 {
    font-size: 58px;
    margin-bottom: 20px;
  }
  h6 {
    font-family: "B612 Mono";
    font-size: 12px;
    margin-bottom: 50px;
  }
}

.hero {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: 80vh;
  margin-bottom: 150px;
  .hero__img {
    background-image: url("https://source.unsplash.com/random/");
    background-position: center center;
    background-size: cover;
    &:first-child {
      background-image: url("https://source.unsplash.com/random/1");
    }
    &:last-child {
      background-image: url("https://source.unsplash.com/random/2");
    }
    &:nth-last-child(2) {
      background-image: url("https://source.unsplash.com/random/3");
    }
  }
}

.arrivals {
  h4 {
    font-size: 36px;
    margin-bottom: 70px;
    text-align: center;
  }
  .wrapper {
    border: 1px solid black;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: 80vh auto;
    // grid에 border color가 없기 때문에 배경색을 설정하고 gap을 준다.
    background-color: black;
    gap: 1px;
    .product,
    .arrivals__category {
      background-color: white;
    }
    .arrivals__category {
      grid-column-start: span 2;
      text-align: center;
      font-size: 20px;
      padding: 20px 0px;
    }
    .product {
      padding: 40px;
      display: grid;
      gap: 20px;
      grid-template-rows: 80% auto;
      .product__photo {
        background-image: url("https://source.unsplash.com/random/4");
        background-position: center center;
        background-size: cover;
      }
      .product__data {
        display: flex;
        flex-direction: column;
        .price {
          margin-top: 10px;
        }
      }
    }
  }
}

footer {
  margin: 100px 0px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: 10fr 2fr;
  background-color: black;
  gap: 1px;
  height: 200px;
  border: 1px solid black;
  div {
    background-color: white;
    &:first-child {
      grid-column: span 2;
    }
    &:last-child {
      grid-column: 1 / -1;
    }
  }
}

```