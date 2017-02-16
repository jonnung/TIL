# Sass 첫걸음
Sass는 CSS를 만들어주는 언어로 자바스크립트처럼 특정 속성의 값을 변수로 선언하여 필요한 곳에 적용할 수 있고, 재사용이 가능하여 반복되는 코드를 줄여준다.  
Sass의 궁극적인 목적은 CSS의 결함을 보정하고, 부족한 부분을 돕는다.  
Sass 파일의 확장자는 .scss 이며, 변환되어 .css 파일이 된다.  

## 비슷한 전처리기들
- [LESS](http://lesscss.org/)
- [Stylus](http://learnboost.github.io/stylus/)

## 문법
### 변수
- 선언: ``` $variable: value;```

### 중첩
- Sass
```
.contentArea {
    background: #fff;

    &:before {  // 복합선택자 속성값이 적용
        color: red;
    }

    .btnSubmit {  // 하위 자식선택자로 속성값이 적용
        text-align: center;
    }

    body.container & {
        margin: 0 auto;
    }
}
```

- CSS
```
.contentArea {
    background: #fff;
}

.contentArea:before {
     color: red;
}

.contentArea .btnSubmit {
     text-align: center
}

body.container .contentArea {
    margin: 0 auto;
}
```
*◎ 부모참조선택자(Referencing Parent Selectors) & 기호로 부모 선택자를 참조할 수 있음*  
*◎ 연관된 스타일들을 여러줄에 중복되게 하지 않지 않고, 그룹핑할 수 있다는 장점*

### 불러오기(Import)
- 작성법: ``` @import "파일명.scss" ``` 또는 ``` @import "파일명" ```
```
// main.scss

@import "custom.scss";

@button-bright: #fff;

.btnSubmit {
    color: @button-bright;
}

.btnCancel {
    color: $button-dark;
}
```
```
// custom.scss

$button-dark: #dcdcdc;
```

### Mixin
- 같은 스타일을 갖는 클래스에 반복 코드를 줄여준다.
  - 선언: @mixin Mixin이름 {}
  - 사용: @include Mixin이름;
```
@mixin background-gray {
    background-color: #dcdcdc;
    border: solid 1px black;
}

@footer {
    @include background-color;
}
```
- Mixin 을 함수 호출하듯 인자를 넘길 수 있으며, 구현 내부에서 사용할 수 있다.
- 선언한 인자보다 적은 개수로도 호출할 수 있으며 선언시 인자값 뒤에 ':기본값' 을 붙여서 기본값을 지정할 수 있다.
```
@mixin background-dark($color, $size:10px) {
    background-color: #787878;
    color: $color;
    font-size: $size;
}

$footer {
    @include background-dark(#ffc300, 15px);
}
```

### 확장
- Mixin 과 비슷하다. 일부 중복되는 속성값을 다른 클래스로부터 적용할 수 있다.
  - 사용: @extend .클래스이름;
```
.icon {
    display: block;
}

.icon_new {
    @extend .ico;
    background-color: #dcdcdc;
}
```

## 참고
- [https://sass-guidelin.es/ko/](https://sass-guidelin.es/ko/)
- [http://wit.nts-corp.com/2015/01/09/2936](http://wit.nts-corp.com/2015/01/09/2936)
