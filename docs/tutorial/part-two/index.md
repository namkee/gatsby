---
title: Gatsby.js Tutorial Part Two
typora-copy-images-to: ./
---

Welcome to part two of the Gatsby tutorial!

In this part we're going to explore options for styling Gatsby websites and dive
deeper into using React components for building sites.

이 파트에서는 Gatsby 웹사이트를 스타일링하는 방법들을 살펴보고 사이트를 만드는데 사용되는 리액트 컴포넌트에 
대해서 좀더 깊게 알아봅니다.

## 컴포넌트를 이용해서 빌딩 

컴포넌트를 빌드할때 발생하는 가장 큰 어려움중 하나는 CSS, HTML 및 JavaScript가 긴밀하게 결합되어 있으며 종종 동일한 파일 내에서도 존재한다는 것입니다.

겉으로보기에는 단순한 변화이지만, 웹 사이트를 구축하는 방법에 대한 심오한 의미가 있습니다.

검색 버튼을 커스터마이징 하는 과정을 예를 들어보면, 과거에는 맞춤 스타일을 사용하여 CSS 클래스 (아마도 `.primary-button`) 를 만들고, 원하는 곳마다 해당 스타일을 적용했습니다.
예를들어.

```html
<button class="primary-button">
  Click me
</button>
```

대신에, 컴포넌트의 세상에서는 원하는 스타일을 가진 `PrimaryButton` 컴포넌트를 만들고 사이트에서 사용하게됩니다.
다음과 같이요.

<!-- prettier-ignore -->
```jsx
<PrimaryButton>Click me</PrimaryButton>
```

컴포넌트는 사이트를 구축하는 하나의 기본 요소입니다. 
브라우저가 제공(인식)하는 것들(`<button>` 와 같은) 을 사용하지 않고,
프로젝트에서 필요한 것들 우아하게 충족시키는 새로운 요소를 쉽게 만들 수 있습니다.

## 글로벌 스타일을 생성하기

모든 사이트에는 글로벌 스타일이 있습니다. 여기에는 사이트의 문자열 스타일 및 배경색과 같은 것들이 포함됩니다. 
이 스타일은 사이트의 색상과 배경의 질감등의 전반적인 느낌을 설정하는 것과 같이 사이트의 전반적인 스타일을 설정합니다.

종종 사람들은 글로벌 스타일로 쓰려고 Bootstrap 이나 Foundation 같은 UI 프레임워크를 사용할 것입니다. 
그러나 커스터마이징이 어렵고 React 구성 요소와 잘 작동하도록 설계되지 않았다는 문제점이 있습니다.

이 튜토리얼에서는 전역 스타일을 생성하는데 특히 Gatsby 및 React와 잘 작동 하는 [Typography.js](https://github.com/kyleamathews/typography.js) 라는 
자바 스크립트 라이브러리를 살펴보겠습니다. 

### Typography.js

Typography.js는 typographic CSS 를 생성하는 라이브러리 입니다. 

다른 HTML 요소의 `font-size` 를 직접 설정하는 대신 Typography.js에 원하는 baseFontSize 및 baseLineHeight를 지정하고 
이를 기반으로 모든 요소에 대한 기본 CSS를 생성합니다.

따라서 수십 개의 CSS 규칙을 직접 수정하지 않고도 사이트의 모든 요소의 글꼴 크기를 변경하는 것이 쉽습니다.

이것을 사용하면 다음과 같이 보입니다.

```javascript
import Typography from "typography";

const typography = new Typography({
  baseFontSize: "18px",
  baseLineHeight: 1.45,
  headerFontFamily: [
    "Avenir Next",
    "Helvetica Neue",
    "Segoe UI",
    "Helvetica",
    "Arial",
    "sans-serif",
  ],
  bodyFontFamily: ["Georgia", "serif"],
});
```

## Gatsby plugins

그러나 Typography.js를 만들고 다시 테스트해보기 전에 Gatsby 플러그인에 대한 빠른 전환과 토론을 해봅시다.


플러그인 아이디어에 대해 잘 알고있을 것입니다. 
많은 소프트웨어 시스템은 사용자 정의 플러그인을 추가하여 새로운 기능을 추가하거나 소프트웨어의 핵심 기능을 수정할 수 있도록 지원합니다.

Gatsby 플러그인도 같은 방식으로 작동합니다.

커뮤니티 회원은(당신과 같은) 다른 사람들이 사용할 수있는 플러그인을 공헌(소량의 JavaScript 코드) 해서 Gatsby 사이트를 구축 사용 하게 할 수 있습니다.

이미 수십 개의 플러그인이 있습니다! [plugins section of the site](/docs/plugins/)에서 확인하십시오.

Gatsby 플러그인을 사용하는 목적은 쉽게 설치하고 사용할 수있게 만드는 것입니다. 
거의 모든 Gatsby 사이트에서 플러그인을 설치하게됩니다. 
나머지 튜토리얼을 진행하면서 플러그인 설치 및 사용을 연습 할 수있는 많은 기회를 갖게됩니다.


## Installing your first Gatsby plugin

새로운 사이트를 만들어 보겠습니다. 이 시점에서 tutorial-part-one을 만드는 데 사용한 터미널 창을 닫아 잘못된 위치에 tutorial-part-two 를 실수로 만들지 않도록하는 것이 좋습니다. 
tutorial-part-two를 만들기 전에 tutorial-part-one을 닫지 않으면 tutorial-part-two가 localhost : 8000 대신 localhost : 8001에 나타납니다.

첫번째 파트와 마찬가지로 새 터미널 창을 열고 다음을 실행하여 새 사이트를 만듭니다.

```shell
gatsby new tutorial-part-two https://github.com/gatsbyjs/gatsby-starter-hello-world
```

이렇게하면 다음과 같은 구조로 새 사이트가 만들어집니다.

```shell
├── package.json
├── src
│   └── pages
│       └── index.js
```

이것은 Gatsby 사이트의 최소 설정입니다.

플러그인을 설치하려면 두 단계가 있습니다. 첫번째 단계는 플러그인의 NPM 패키지를 설치 합니다.
두 번째 단계는 gatsby-config.js에 플러그인을 추가합니다.

Typography.js 는 Gatsby 플러그인을 제공하고 있으므로 다음을 실행하여 설치하십시오.

```shell
npm install --save gatsby-plugin-typography
```

그런 다음 코드 편집기에서 `gatsby-config.js` 라는 프로젝트 폴더의 루트에 파일을 만듭니다. 
사이트의 다른 설정도 추가하면서 동시에 플러그인 관련 설정도 추가하는 곳입니다.

다음을 `gatsby-config.js`에 복사하십시오.


```javascript
module.exports = {
  plugins: [`gatsby-plugin-typography`],
};
```

Gatsby는 시작할 때 사이트의 설정 파일을 읽습니다. 
여기서 우리는 `gatsby-plugin-typography` 라는 플러그인을 읽어들이도록 했습니다. 
Gatsby는 NPM 패키지 로 되어 있는 플러그인을 찾았으므로, 이미 설치 된 패키지를 찾습니다.

이제 `gatsby develop`를 실행하십시오. 
사이트를 로드하고나서 Chrome 개발자 도구를 사용하여 생성 된 HTML을 검사 해보면 
생성 된 CSS가 있는 `<head>` 요소에 typography 플러그인이 추가한 `<style>` 요소 확인 할 수 있습니다.


![typography-styles](typography-styles.png)

아래 코드를 `src/pages/index.js` 에 복사해서 붙여 넣으면 Typography.js 가 만들어낸 CSS 가 적용된 것을 볼수 있을겁니다. 

```jsx
import React from "react";

export default () => (
  <div>
    <h1>Richard Hamming on Luck</h1>
    <div>
      <p>
        From Richard Hamming’s classic and must-read talk, “<a href="http://www.cs.virginia.edu/~robins/YouAndYourResearch.html">
          You and Your Research
        </a>”.
      </p>
      <blockquote>
        <p>
          There is indeed an element of luck, and no, there isn’t. The prepared
          mind sooner or later finds something important and does it. So yes, it
          is luck.{" "}
          <em>
            The particular thing you do is luck, but that you do something is
            not.
          </em>
        </p>
      </blockquote>
    </div>
    <p>Posted April 09, 2011</p>
  </div>
);
```

사이트는 이제 아래 그림처럼 보일겁니다.

![typography-not-centered](typography-not-centered.png)

빠르게 작업을 진행해 봅시다. 많은 사이트들이 페이지의 중앙부분에 한줄짜리 텍스트를 보여주고 있습니다.
이걸 만들어보기 위해서 `src/pages/index.js` 안에 `<div>` 에 다음과 같이 스타일을 입혀 봅시다.

```jsx{4,23}
import React from "react";

export default () =>
  <div style={{ margin: '3rem auto', maxWidth: 600 }}>
    <h1>Richard Hamming on Luck</h1>
    <div>
      <p>
        From Richard Hamming’s classic and must-read talk, “<a href="http://www.cs.virginia.edu/~robins/YouAndYourResearch.html">
          You and Your Research
        </a>”.
      </p>
      <blockquote>
        <p>
          There is indeed an element of luck, and no, there isn’t. The prepared
          mind sooner or later finds something important and does it. So yes, it
          is luck.{" "}
          <em>
            The particular thing you do is luck, but that you do something is
            not.
          </em>
        </p>
      </blockquote>
    </div>
    <p>Posted April 09, 2011</p>
  </div>
```

![basic-typography-centered](typography-centered.png)

멋집니다. 

여기까지 우리가 확인할수 있는건 Typography.js 가 생성하는 기본 CSS 입니다. 
하지만 손쉽게 커스터마이징 할수 있습니다. 직접 해보도록 하죠

사이트에서 `src/utils` 디렉토리를 만들고 그 디렉토리에 `typography.js` 라는 파일을 만듭니다.
그리고 그 파일에 다음의 코드를 작성합니다.

```javascript
import Typography from "typography";

const typography = new Typography({ baseFontSize: "18px" });

export default typography;
```

그런 다음 `gatsby-config.js` 파일에서 `gatsby-plugin-typography` 가 설정을 읽어들일수 있도록 모듈을 설정하십시오.

```javascript{2..9}
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography.js`,
      },
    },
  ],
};
```

개발 프로세스가 실행되고 있는 터미널 창으로 가서<kbd>Ctrl + c</kbd> 를 눌러 `gatsby develop` 을 멈추게 합니다.

`gatsby develop` 를 다시 실행해서 재시작합니다. 플러그인 설정이 변경된것을 다시 읽어들여 실행하도록 하기 위함입니다.

이제 전체 텍스트 크기가 약간 커졌을 겁니다. `baseFontSize` 를 `24px` 로 바꿔 봅시다. 또 `12px` 로 바꿔 봅시다.
`baseFontSize` 로 설정한 값을 기준으로 모든 요소들의 `font-size` 값이 변경되어 크기가 조절됩니다. 

_만약 기본 스타터 에서 `gatsby-plugin-typography` 를 사용 하는 거라면, 기본으로 생성된 index.css 파일을 삭제해주어야 Typography.js CSS 가 생성된 CSS 가 덮어쓰여지는걸 방지할 수 있습니다._

Typography.js 를 사용한 [수많은 테마들](https://github.com/KyleAMathews/typography.js#published-typographyjs-themes) 이 존재합니다.
그중 몇개를 사용해봅시다. 터미널 상에서 사이트의 루트디렉토리에서 다음을 실행합니다. 

```shell
npm install --save typography-theme-bootstrap typography-theme-lawton
```

Bootstrap 테마를 사용하려면 typography 코드를 다음과 같이 수정해주어야 합니다. 

```javascript{2,4}
import Typography from "typography";
import bootstrapTheme from "typography-theme-bootstrap";

const typography = new Typography(bootstrapTheme);

export default typography;
```

![typography-bootstrap](typography-bootstrap.png)

테마는 Google 글꼴을 추가 할 수도 있습니다. 
우리가 Bootstrap 테마와 함께 설치 한 Lawton 테마가 Google 글꼴을 사용하고 있습니다.

타이포그래피 모듈 코드를 다음과 같이 바꾼 다음 dev 서버를 다시 시작하십시오 (새 Google 글꼴을로드하는 과정이 필요합니다).

```javascript{2-3,5}
import Typography from "typography";
// import bootstrapTheme from "typography-theme-bootstrap"
import lawtonTheme from "typography-theme-lawton";

const typography = new Typography(lawtonTheme);

export default typography;
```

![typography-lawton](typography-lawton.png)

Typography.js 는 30개가 넘는 테마를 가지고 있습니다.
[데모를 통해서 실험](http://kyleamathews.github.io/typography.js) 해보거나 
[전체 목록](https://github.com/KyleAMathews/typography.js#published-typographyjs-themes) 을 확인해보세요.

## Component CSS

Gatsby 는 컴포넌트를 스타일링 할 수 있는 다양한 옵션들이 있습니다.
이 튜토리얼에서는 가장 유명한 방법인 CSS 모듈 을 살펴 보겠습니다. 

### CSS-in-JS

While we won't cover CSS-in-JS in this initial tutorial, we encourage you to explore CSS-in-JS libraries as these solve many of the problems with traditional CSS plus help make your React components even smarter. There are mini-tutorials for two libraries, [Glamor](/docs/glamor/) and [Styled Components](/docs/styled-components/). Check out the following resources for background reading on CSS-in-JS:

[Christopher "vjeux" Chedeau's 2014 presentation that sparked this movement](https://speakerdeck.com/vjeux/react-css-in-js)
as well as
[Mark Dalgleish's more recent post "A Unified Styling Language"](https://medium.com/seek-blog/a-unified-styling-language-d0c208de2660).

### CSS Modules

**CSS Modules** 을 살펴 봅시다. .

[the CSS Module 홈페이지](https://github.com/css-modules/css-modules) 에서 강조했습니다. :

> **CSS Module** 은 모든 클래스 이름과 애니메이션 이름이 기본적으로 로컬로 범위가 지정된 CSS 파일입니다. 

CSS 모듈은 일반적인 CSS처럼 작성할 수 있기 때문에 매우 인기가 있지만 훨씬 더 안전합니다. 
CSS 모듈은 클래스 및 애니메이션 이름을 자동으로 고유한 것으로 생성하기 때문에 셀렉터의 이름 충돌에 대해 걱정할 필요가 없습니다.

CSS 모듈은 Gatsby 를 이용해 새롭게 만들어지는 경우에 매우 권장됩니다.(일반적인 리택트도 마찬가지)



Gatsby 는 CSS 모듈을 즉시 사용할 수 있습니다.

CSS 모듈을 이용해서 페이지를 만들어 봅시다.

먼저, CSS-in-JS 예제들에서 사용하게될 `Container` 컴포넌트를 생성해 봅시다.
`src` 디렉토리 하위에 `components` 디렉토리를 만들고, 데릭토리 안에 `container.js` 라고 파일을 생성합니다.
그리고 다음의 코드를 붙여넣어주세요.

```javascript
import React from "react";

export default ({ children }) => (
  <div style={{ margin: "3rem auto", maxWidth: 600 }}>{children}</div>
);
```

그리고나서 새로운 컴포넌트 페이지를 `src/pages/about-css-modules.js` 파일에 생성해 봅시다.

```javascript
import React from "react";

import Container from "../components/container";

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
  </Container>
);
```

앞서 생성한 `Container` 컴포넌트를 임포트 했습니다.

페이지는 다음과 같이 보여질 겁니다. 

![css-modules-1](css-modules-1.png)

이름, 아바타 및 짧은 라틴어 전기가있는 사람들의 목록을 만들어 보겠습니다.

먼저, `src/pages/about-css-modules.module.css` 경로에 CSS 파일을 생성합니다.
파일의 이름은 `.css` 가 아니라, 반드시 `.module.css` 로 끝나야 함을 기억하세요. Gatsby 가 CSS modules 를 처리할때 읽어들일 파일을 지정하는 규약입니다. 

파일에 다음과 같이 코드를 붙여넣으세요. 

```css
.user {
  display: flex;
  align-items: center;
  margin: 0 auto 12px auto;
}

.user:last-child {
  margin-bottom: 0;
}

.avatar {
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
}

.description {
  flex: 1;
  margin-left: 18px;
  padding: 12px;
}

.username {
  margin: 0 0 12px 0;
  padding: 0;
}

.excerpt {
  margin: 0;
}
```

앞서 생성한 페이지 파일에 `about-css-modules.js` 파일을 임포트 하고 한줄을 더 추가합니다.
(`console.log(styles)` 코드는 임포트한 결과 를 로깅해서 처리되는 파일이 어떤 모습인지 확인 하려는 목적입니다).

```javascript
import styles from "./about-css-modules.module.css";
console.log(styles);
```

브라우저의 개발자 콘솔을 열어보면 다음같이 확인 할수 있습니다.

![css-modules-console](css-modules-console.png)

CSS 파일과 비교하면 각 클래스는 가져온 객체의 키값으로 쓰이는 긴 문자열을 참조하는 것을 볼 수 있습니다. 
예를 들어 `avatar` 는 `about-css-modules-module---avatar----hYcv` 을 가리 킵니다. 
이것이 CSS 모듈이 생성하는 클래스 이름입니다. 사이트 전체에서 고유한 것으로 보장됩니다. 
클래스를 사용하기 위해 임포트를 명시적으로 하기 때문에, CSS가 어디에서 사용되는지에 대해서는 전혀 의문의 여지가 없습니다.

우리의 스타일을 `User` 컴포넌트를 생성하는데 사용해 봅시다.

`about-css-modules.js` 페이지 컴포넌트에 새로운 컴포넌트를 인라인 형태로 생성해 봅시다.
일반적인 경우에 여러 위치에서 컴포넌트를 재사용하는 경우 `components` 디렉토리 안에 자신의 이름을 가진 파일이 존재하는 것을 원칙으로 합니다.
하지만, 사용되는곳이 딱하나만 있는경우 인라인으로 만듭니다. 

`about-css-modules.js` 파일을 다음과 같이 수정합니다. 

```jsx{6-17,23-30}
import React from "react";
import styles from "./about-css-modules.module.css";
console.log(styles);

import Container from "../components/container";

const User = props =>
  <div className={styles.user}>
    <img src={props.avatar} className={styles.avatar} alt="" />
    <div className={styles.description}>
      <h2 className={styles.username}>
        {props.username}
      </h2>
      <p className={styles.excerpt}>
        {props.excerpt}
      </p>
    </div>
  </div>

export default () =>
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
      excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
      excerpt="I'm Bob smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
  </Container>
```

완료된 파일은 다음과 같습니다. 

![css-modules-final](css-modules-final.png)

### Other CSS options

Gatsby 는 가능한 거의 모든 스타일링 옵션을 지원합니다.(당신이 선호하는 CSS 옵션이 아직 플러그인으로 제공되지 않는다면 [한번 공헌해주시죠!](/docs/how-to-contribute/))

* [Sass](/packages/gatsby-plugin-sass/)
* [Emotion](/packages/gatsby-plugin-emotion/)
* [JSS](/packages/gatsby-plugin-jss/)
* [Stylus](/packages/gatsby-plugin-stylus/)
* and more!

Now continue on to [Part Three](/tutorial/part-three/) of the tutorial.
