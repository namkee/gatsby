---
title: Building nested layouts in Gatsby
typora-copy-images-to: ./
---

Welcome to part three!

## What's in this tutorial?

이 파트에서는 Gatsby가 "레이아웃 컴포넌트"를 만드는 방법에 대해 배우게됩니다. 
레이아웃 컴포넌트는 여러 페이지에 걸쳐 공유하려는 사이트 섹션입니다. 
예를 들어, Gatsby 사이트에는 공통적으로 공유하여 사용하는 머리글과 바닥글 컴포넌트가 있습니다. 
레이아웃에 추가 할 수있는 다른 공통적인 것들은 사이드 바 및 메뉴입니다.

이 페이지에서 왼쪽에있는 사이드 바 (더 큰 사이즈의 디바이스를 사용한다고 가정)와 
맨 위의 머리글은 gatsbyjs.org의 레이아웃 컴포넌트의 일부입니다.

Gatsby 레이아웃을 살펴봅시다.

## Install a starter

먼저 튜토리얼의이 부분을위한 새로운 사이트를 생성 하십시오. 
(그리고 2 부에서 언급했듯이 이 시점에서 터미널 창의 창을 닫고 이전  튜토리얼의 프로젝트 파일을 닫아서 혼돈이 생기지 않도록 하세요). 
"hello world"스타터를 다시 사용합니다.


```shell
gatsby new tutorial-part-three https://github.com/gatsbyjs/gatsby-starter-hello-world
```

사이트 생성이 끝나면 `gatsby-plugin-typography` 를 설치하십시오. 
이를 수행하는 방법에 대한 내용은 튜토리얼 제 2 부를 참조하십시오. 
Typography.js 테마의 경우 이번에는 "Fairy Gates" typography 테마를 사용해 봅시다.

```shell
npm install --save gatsby-plugin-typography typography-theme-fairy-gates
```

`src/utils` 디렉토리를 생성하고, `src/utils/typography.js` typography 설정 파일을 생성 합니다.

```javascript
import Typography from "typography";
import fairyGateTheme from "typography-theme-fairy-gates";

const typography = new Typography(fairyGateTheme);

export default typography;
```

사이트의 루트 디렉토리에 우리 사이트에서 사용할 `gatsby-config.js` 파일을 생성하고 다음 코드를 붙여넣으세요.

```javascript
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

이제, 몇개의 페이지를 추가 합시다. front 페이지, about 페이지, contact 페이지 

`src/pages/index.js`

```jsx
import React from "react";

export default () => (
  <div>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </div>
);
```

`src/pages/about.js`

```jsx
import React from "react";

export default () => (
  <div>
    <h1>About me</h1>
    <p>I’m good enough, I’m smart enough, and gosh darn it, people like me!</p>
  </div>
);
```

`src/pages/contact.js`

```jsx
import React from "react";

export default () => (
  <div>
    <h1>I'd love to talk! Email me at the address below</h1>
    <p>
      <a href="mailto:me@example.com">me@example.com</a>
    </p>
  </div>
);
```

![no-layout](no-layout.png)

이제 멋진 개인 사이트가 시작되었습니다!

그러나 몇 가지 문제가 있습니다. 
첫째, 페이지 내용이 튜토리얼의 파트 2에서와 같이 화면 중앙에 있으면 좋을 것입니다. 
두 번째로, 일종의 글로벌 네비게이션이 있어야 방문자가 각 하위 페이지를 찾고 쉽게 방문 할 수 있습니다.

첫 번째 레이아웃 컴포넌트를 만들어 이러한 문제를 해결해 보겠습니다.

## Our first layout component

먼저, `src/layouts` 디렉토리를 생성합니다. 모든 레이아웃 컴포넌트들이 여기에 위치할 겁니다.

가장 기초적인 레이아웃 컴포넌트를 `src/layouts/index.js` 에 생성합니다.

```jsx
import React from "react";

export default ({ children }) => (
  <div style={{ margin: `0 auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children()}
  </div>
);
```
_다른 대부분의 `children` 속성과는 다르게, 레이아웃 컴포넌트에 전달된 `children` 속성은 function 이므로, 함수를 실행해야 합니다._

`gatsby develop` 를 중지하고, 재시작해서 새로운 레이아웃이 적용된 것으로 다시 띄워 봅시다.

![with-layout2](with-layout2.png)

레이아웃이 잘 동작 합니다! 이제 텍스트가 가운데에 배치되고 지정했던 650 픽셀의 너비로 확인할 수 있습니다.

이제 동일한 파일에 사이트 제목을 추가하겠습니다.

```jsx{5}
import React from "react";

export default ({ children }) =>
  <div style={{ margin: `0 auto`, maxWidth: 650, padding: `0 1rem` }}>
    <h3>MySweetSite</h3>
    {children()}
  </div>
```

세 페이지 중 어디를 가더라도 동일한 제목이 추가됩니다. 예를들어 `/about/` 페이지는 다음과 같이 적용됩니다. 

![with-title](with-title.png)

3개의 페이지로의 링크를 추가해 봅시다.

```jsx{2-9,12-22}
import React from "react";
import Link from "gatsby-link";

const ListLink = props =>
  <li style={{ display: `inline-block`, marginRight: `1rem` }}>
    <Link to={props.to}>
      {props.children}
    </Link>
  </li>

export default ({ children }) =>
  <div style={{ margin: `0 auto`, maxWidth: 650, padding: `1.25rem 1rem` }}>
    <header style={{ marginBottom: `1.5rem` }}>
      <Link to="/" style={{ textShadow: `none`, backgroundImage: `none` }}>
        <h3 style={{ display: `inline` }}>MySweetSite</h3>
      </Link>
      <ul style={{ listStyle: `none`, float: `right` }}>
        <ListLink to="/">Home</ListLink>
        <ListLink to="/about/">About</ListLink>
        <ListLink to="/contact/">Contact</ListLink>
      </ul>
    </header>
    {children()}
  </div>
```

![with-navigation](with-navigation.png)

이제 세 페이지가 기본적인 글로벌 네비게이션으로 잘 나타나고 있습니다.

_Challenge:_ 생성한 "레이아웃 컴포넌트" 를 조금더 강력하게 해봅시다. 헤더와 푸터, 글로벌 네비게이션, 사이드 바 등을 를 추가해봅시다. 

## What's coming next?

Continue on to
[part four of the tutorial where we'll start learning about Gatsby's data layer and programmatic pages!](/tutorial/part-four/)
