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

