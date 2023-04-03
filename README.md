<vue 시작하기> 20230403

1. node.js 설치와 코드에디터 설치
2. 터미널 명령어
- npm install -g @vue/cli 
   vue 설치
- vue create project_name 
   vue 프로젝트 명 입력, 프로젝트 생성 => 프로젝트가 생성된 폴더로 다시 open folder!
- npm run serve
    라이브 서버로 미리보기.
- 코딩은 App.vue에 하기

3. 확장프로그램
Vetur, Vue 3 snippets, HTML CSS Support

4. app.vue
<template>안에는 html, script 안에는 js, style안에는 css 작성

5. 라이브 서버
new terminal => npm run serve => 터미널에 있는 주소 ctrl + click!


6. npm은 각종 웹개발 라이브러리 설치 도우미.
node.js 설치는 npm을 사용하기 위해 설치한 것.

7. node_modules: 프로젝트 라이브러리들
src: 소스코드 파일
package.json 라이브러리 버전, 프로젝트 설정 기록

<데이터 바인딩>
- 자주 바뀌는 데이터는 바인딩 해 놓는다. {{}}
- 데이터는 object 형식으로 보관한다.
- html 속성도 바인딩 가능
- :style = "style_c"  
:속성 = "데이터 이름" 으로 사용.

<반복문 v-for>
<a v-for="atag in 3" :key = "atag" href="#">HOME</a>

태그를 반복할 수 있다.

<a v-for="data in menu" :key = "data" href="#">{{data}}</a>
<a v-for="(data,i) in menu" :key = "i" href="#">{{i}}</a>  0, 1, 2로 출력
i는 인덱스. data는 데이터 내용.

menu : ['HOME', 'ABOUT', 'PRODUCTS'],

key 반복문 쓸 때 반드시 써야 함.
반복문 돌린 요소를 컴퓨터가 구분하기 위해 쓴다.

<이벤트 v-on:click="function이름">
@click ="" 축약형.

<button @click="countNum++">허위매물신고</button> <span>신고수 : {{countNum}}</span>
data
countNum : 0,


@mouseover,@drag, @focus..

<vue에서 함수 만들기>
methods: {함수(){}}

  methods : {
    increase(){
      this.countNum++;
    }
  },


-이미지 파일은 주로 assets 파일에 넣어 관리.


<v-if 조건식>
v-if=""

<div class="black-bg" v-if="modalIsOpen">
    <div class="white-bg">
      <h4>상세페이지이다.</h4>
      <p>상세페이지 내용</p>
    </div>
  </div>

modalIsOpen이 참일 때만 UI를 보여준다.


<import/export>

var apple = 10;
export default apple

------

import apple from './assets/oneroom.js';


_________________________________________

v-if="조건식"
조건식 참일 때만 UI는 보여진다.
v-else
v-if가 참이 아닐 때 이 UI를 보여주세요.


<Component>
HTML을 간단하게 쓰고 싶을 때 사용.
- NEW 파일을 만든다.(컴포넌트이름.vue)
- app.vue와 같은 형식으로 작성.
-컴포넌트 사용법
1) import
- import Discount from './Discount.vue';
2)등록
components: {
    Discount : Discount,
  }
Discount를 Discount 컴포넌트로 갖다 쓰겠다는 내용.
3) 사용
<Discount></Discount>

* 컴포넌트 사용은 multi-word로. (대문자 두번 사용해서 구분)


<Component 사용 시 데이터 바인딩  Props로 해결>
부모 컴포넌트의 데이터를 자식 컴포넌트가 사용하고 싶을 때.
props를 사용하세요!~~

1. 데이터 전송
v-bind 혹은 :

app.vue <자식컴포넌트 :데이터(작명) = "데이터(실제데이터)">
2. 데이터 등록

modal.vue 

props: {
        oneroom : Array,
    }

props: {데이터이름 : 자료형 이름}

3. 사용

***props는 read-only이다. 받아온 자료를 수정할 수 없다.

app.vue
components에 등록


v-bind="오브젝트"


<자식 컴포넌트에서 props를 수정하고 싶다!!!>
custom event 
자식은 부모가 가진 데이터를 원래 수정할 수가 없기 때문에
자식컴포넌트가 데이터를 수정해달라는 요청을 보내야 한다.
@click="$emit('작명', '데이터')"


card.vue
<h4 @click="$emit('openModal')">{{oneroom[i].title}}</h4>

app.vue
<CardUi :oneroom = "oneroom" @openModal="modalIsOpen = true"></CardUi>

자식이 보낸 '데이터'는 $event로 꺼내 볼 수 있다.

<CardUi :oneroom = "oneroom" @openModal="modalIsOpen = true; clIdx = $event"></CardUi>

<h4 @click="$emit('openModal', oneroom.id);">{{oneroom[i].title}}</h4>


** 데이터를 함수안에서 사용할 때
this.를 함께 사용한다.


<v-model: 입력시 데이터 저장>

input @input="month = $event.target.value"
<input v-model="month">

사용자가 input에 입력한 것은 전부 문자 자료형이 된다.
자바스크립트는 숫자계산도 괜춘하다.


<watcher>
데이터 감시하는 기능.

watch: {
        감시할 데이터(value, before){
            //감시할 데이터가 변화할 데이터는 value
//before 변경 전 데이터
        }
    }


---
클래스 탈부착
<div class="start" :class="{end : true조건}">

<div class="start" :class="{end : modalIsOpen}">

-----
<transition> 태그 
<transition name="fade">
    <ModalUi :oneroom = "oneroom" :clIdx = "clIdx" :modalIsOpen = "modalIsOpen" @closeModal="modalIsOpen = false"></ModalUi>
  </transition>

.fade(작명)-enter-from{
  /* 시작 */
  opacity:0;
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
  /* 끝 */
  opacity:1;
}


퇴장시 => enter를 leave로 작성

