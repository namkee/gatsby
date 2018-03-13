---
title: Introduction to Gatsby basics
typora-copy-images-to: ./
---

Gatsby.js 튜토리얼의 제 1 부에 오신 것을 환영합니다.

## 이 튜토리얼에서 다루는 것

이 튜토리얼에서는 Gatsby 개발 환경, 구성 요소 페이지 작성 방법 및 Gatsby 사이트 구축 및 배포 방법에 대해 간략하게 소개합니다.

시작해보죠!

## 개발 환경이 갖춰졌는지 확인해 봅시다

먼저 Gatsby 로 생성 을 시작하기 위한 준비가 되었는지 확인해 봅시다.
최신 버전의 Node.js가 설치되어 있어야합니다.

Node.js는 서버와 컴퓨터의 터미널에서 JavaScript를 실행하기위한 프로그래밍 도구입니다. Gatsby는 Node.js로 만들어졌습니다.


터미널 창을 엽니다. ([terminal instructions for Mac users](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/) 와 
[terminal instructions for Windows users](https://www.quora.com/How-do-I-open-terminal-in-windows)를 참고하세요) 

터미널 창에서 `node --version` 를 입력 하고 엔터키를 눌러봅니다, 그리고 나서  `npm --version` 를 입력하고 엔터를 눌러봅시다.(팁: 특정 명령을 실행하기 위해서는 명령을 입력하고 엔터를 눌러야 합니다. 그러면 명령이 실행될 거에요.)

다음과 같은 결과를 확인 할 수 있습니다.

![Check if node.js/npm is installed](check-versions.png)

Gatsby 는 Node v6 이상, npm v3 이상을 지원합니다.

Node.js 가 설치 되어 있지 않다면, https://nodejs.org/ 로 가서 사용하고 있는 운영체제에 맞는 버전으로 설치 해주세요.

## "Hello World" starters 설치 

Gatsby 는 "starters"를 새로운 프로젝트를 생성하는 방법으로 제공합니다. Starters 는 보다 빠르게 진행 할수 있도록 Gatsby 사이트의 기본 설정등이 작성되어 부분적으로 빌드 되어 있습니다.
공식적으로 제공하는 Starter 뿐만아니라 Gatsby 커뮤니티에서 제공하고 있는 수많은 Starter 들이 있습니다.
[See the Starters page for the full list](/docs/gatsby-starters/).

Starter 를 설치하려면, 먼저 다음과 같이  Gatsby's command line 프로그램을 설치해야합니다. 

```sh
npm install --global gatsby-cli
```

설치되었다면, 다음의 명령을 입력하고 엔터를 눌러주세요.

```sh
gatsby new tutorial-part-one https://github.com/gatsbyjs/gatsby-starter-hello-world
```

이 명령은 Starter 파일들을 다운로드하고, 필수 npm 패키지들을 설치 합니다. 이과정은 아마도 1.5~3분 내에 완료 될 것입니다. 처음에는 아무것도 일어나지 않은것처럼 보이지만, 조그만 참으세요!

이제 Gatsby를 실행 해 봅시다.

Gatsby 내장된 개발 서버를 가지고 있습니다. 앞서 진행했던 터미널 창에서 다음의 명령을 입력해 봅시다. 

```sh
cd tutorial-part-one
gatsby develop
```

몇개의 짧은 내용들이 보여지고나서 마지막에 다음과 같은 메시지를 볼 수 있습니다.
`The development server is listening at:` [http://localhost:8000](http://localhost:8000). 

그 주소를 브라우저여서 확인해보면...

![Gatsby.js hello world](hello-world.png)

잘 동작하네요!!!

멋지네요 😎

Gatsby 의 개발서버는 "hot reloading" 서버입니다. React.js 페이지 컴포넌트들(데이터 파일들을 의미하는데, 뒤에 살펴볼 겁니다) 에 변경이 있다면 즉시 브라우저에 로드되어 보여지거나 사라질겁니다.

개발을 정말 빠르고 흥미있게 해주는 엄청난 기능이에요.

한번 직접 해보죠.


다음 부분을 진행하기 위해서는 아마도 코드편집기가 필요할 것입니다. [VS Code](https://code.visualstudio.com/) 를 추천합니다.
바로 위에서 진행한 터미널에서 `gatsby new` 명령 입력했으니 결과로 "tutorial-part-one" 폴더가 생성되었을 겁니다. 
코드 편집기로 위 폴더를 열어 봅시다.

"tutorial-part-one" 폴더를 코드편집기로 열었다면 이제 본격적으로 웹사이트를 만들어봅시다. 
몇개의 디렉토리와 파일들을 확인할 수 있습니다. `src/pages/index.js` 위치의 파일을 찾아서 열어봅니다.
그리고 페이지 컴포넌트 안에 있는 "Hello world!" 로 되어 있는 부분을  "Hello Gatsby!" 로 변경해봅시다.
변경하고 저장을 하는 순간 브라우저의 문구가 변경될 겁니다.(팁: 브라우저에 변경사항이 나타나려면 항상 저장을 해야 합니다.)

아래와 같이 몇가지 트릭들을 해봅시다.

1. Gatsby 은 자바스크립트의 스타일 prop 를 통해서 스타일을 지정하는 "inline styles" 기능을 제공합니다. (다른 스타일 지정 방법은 뒤에 배우게 됩니다.).

   페이지 컴포넌트를 다음과 같이 교체해봅시다.

```jsx
import React from "react";

export default () => <div style={{ color: `blue` }}>Hello Gatsby!</div>;
```

color 를 pink 로 변경하고, 또 tomato 로 변경 합니다.

2. 몇개의 문장을 추가합니다.

```jsx{5-6}
import React from "react";

export default () =>
 <div style={{ color: `tomato` }}>
   <h1>Hello Gatsby!</h1>
   <p>What a world.</p>
 </div>
```

3. 이미지를 추가합니다. (이 예제 경우 Unsplash에서 랜덤 이미지를 출력합니다.)

```jsx{7}
import React from "react";

export default () =>
 <div style={{ color: `tomato` }}>
   <h1>Hello Gatsby!</h1>
   <p>What a world.</p>
   <img src="https://source.unsplash.com/random/400x200" alt="" />
 </div>
```

이제 화면이 다음과 같이 나올겁니다.

![Screen Shot 2017-06-03 at 11.57.10 AM](moving-along.png)

## 페이지 간의 링크

웹사이트는 페이지들과 페이지들간의 링크로 이루어 집니다. 지금 아주 이쁜 첫번째 page-on 이라는 페이지를 만들었지만 링크가 없으니 유기적으로 연결된 느낌이 없습니다.
그러니 새로운 페이지를 생성해봅시다.

먼저 새로운 페이지와 연결할 링크를 생성합니다.

그러기 위해서는 Starter 를 설치할때 같이 설치되었던 `gatsby-link` 패키지에서 제공하는 `<Link>` 컴포넌트를 임포트 합니다.

일반적인 형태의 HTML 의 `<a>` 와는 다르게 Gatsby 의 `Link` 컴포넌트는 링크에 연결할 페이지를 `to` 로 지정합니다.
링크할 페이지 경로를 `/page-2/` 로 기입합니다. 추가해봅시다. 추가가 완료 되었다면 페이지 컴포넌트는 다음과 같을겁니다.

```jsx{2,9-12}
import React from "react";
import Link from "gatsby-link";

export default () =>
  <div style={{ color: `tomato` }}>
    <h1>Hello Gatsby!</h1>
    <p>What a world.</p>
    <img src="https://source.unsplash.com/random/400x200" alt="" />
    <br />
    <div>
      <Link to="/page-2/">Link</Link>
    </div>
  </div>
```

링크를 클릭해보면 브라우저는 다음과 같은 화면이 나올겁니다.

![Gatsby.js development 404 page](dev-404.png)


Gatsby.js 개발 404 페이지가 보입니다. 404 페이지가 이야기해준 대로
`src/pages/page-2.js` 에 React.js 페이지 컴포넌트를 만듭니다.

두번째 페이지 컴포넌트를 다음과 같이 생성합니다.

```jsx
import React from "react";
import Link from "gatsby-link";

export default () => (
  <div>
    <p>Hello world from my second Gatsby page</p>
    <Link to="/">back home</Link>
  </div>
);
```

저장하면 이제 두 페이지 사이를 앞뒤로 클릭 할 수 있습니다.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="/images/clicking-2.mp4"></source>
  <p>Your browser does not support the video element.</p>
</video>

_Challenge_: 위의 방법을 힌트로 사용하여 세 번째 페이지를 만들고 홈 페이지에서 세 번째 페이지로 연결해 봅시다.

## Interactive page

Gatsby를 웹 사이트 구축하는 것과 다른 도구를 통해 구축하는 것과 비교해 좋은 점 중 하나는 페이지에 대화형 기능을 추가하는 것이 더 쉽다는 것입니다. 
React.js는 Facebook.com 을 위해 설계되었으며 다른 많은 세계적인 웹 프로그램에서 사용됩니다.

페이지에 상호 작용 요소를 추가하는 방법을 살펴 보겠습니다. 카운터부터 시작하겠습니다.

우리가 만들었던 `index.js` 페이지 컴포넌트 에서 인 `<Link to="/counter/">Counter</Link>` 로 `/counter` 의 페이지로의 새 링크를 만드는 것으로 시작하겠습니다 .


```jsx{13-15}
import React from "react";
import Link from "gatsby-link";

export default () =>
  <div style={{ color: `tomato` }}>
    <h1>Hello Gatsby!</h1>
    <p>What a world.</p>
    <img src="https://source.unsplash.com/random/400x200" alt="" />
    <br />
    <div>
      <Link to="/page-2/">Link</Link>
    </div>
    <div>
      <Link to="/counter/">Counter</Link>
    </div>
  </div>
```

해당 링크를 추가하고 클릭 한 다음 `/counter/`에서 보여질 "Hello World" 페이지 컴포넌트를 앞서 진행했던것과 같이 작성합니다. 
그러나 이전처럼 "functional component" 양식을 사용하는 것이 아니라,  "class" 컴포넌트를 만들 것입니다.


```jsx
import React from "react";

class Counter extends React.Component {
  render() {
    return <div>Hello Class Component</div>;
  }
}

export default Counter;
```

React의 클래스 형식을 사용하면 컴포넌트의 상태를 사용 할 수 있습니다. 상태는 카운터를 만드는데 필요합니다.

우리 카운터를 살피면서 계속합시다. 두 개의 버튼을 추가합시다. 하나는 증가, 하나는 감소 시키는 버튼입니다.

```jsx{5-12}
import React from "react";

class Counter extends React.Component {
  render() {
    return (
      <div>
        <h1>Counter</h1>
        <p>current count: 0</p>
        <button>plus</button>
        <button>minus</button>
      </div>
    )
  }
}

export default Counter
```

이제 우리는 멋진 카운터를 만드는 데 필요한 모든 것을 갖추었으니, 실제 동작하도록 해봅시다.

먼저 컴포넌트 상태를 설정합니다.

```jsx{4-7,13}
import React from "react";

class Counter extends React.Component {
  constructor() {
    super()
    this.state = { count: 0 }
  }

  render() {
    return (
      <div>
        <h1>Counter</h1>
        <p>current count: {this.state.count}</p>
        <button>plus</button>
        <button>minus</button>
      </div>
    )
  }
}

export default Counter
```

이제 현재 카운트를 컴포넌트 상태에서 가져와 렌더링 합니다.

이제 단추를 클릭 하는 시점에 상태를 변경해 보겠습니다.

```jsx{14-19}
import React from "react";

class Counter extends React.Component {
  constructor() {
    super()
    this.state = { count: 0 }
  }

  render() {
    return (
      <div>
        <h1>Counter</h1>
        <p>current count: {this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count +
          1 })}>plus
        </button>
        <button onClick={() => this.setState({ count: this.state.count -
          1 })}>minus
        </button>
      </div>
    )
  }
}

export default Counter
```

잘 됩니다! 정적 웹 사이트 내부에 React.js 카운터 가 동작합니다 👌

_보너스 도전_ : 재미있는 점 중 하나는 hot reloading이 콘텐츠 및 스타일에만 적용되는것이 아니라, 코드도 작동합니다. 
현재 카운터에서 버튼을 클릭하면 숫자가 1 씩 증가 또는 감소합니다. 카운터를 다른 증감 (예 : 5)으로 위아래로 이동하십시오.

## Deploying Gatsby.js websites on the web

Gatsby.js 는 _정적 사이트 생성기_ 입니다. 즉, 배포 하는데 설정을 해야하는 서버가 필요하다거나, 복잡한 데이터베이스가 필요하지 않다는 겁니다.
대신 Gatsby는 정적 사이트 호스팅 서비스에 배포 할 수있는 정적 HTML 및 JavaScript 파일을 한 디렉터리에 생성합니다.

첫 Gatsby 웹사이트를 [Surge](http://surge.sh/) 를 이용해서 배포해봅시다.
Surge 는 수많은 정적 사이트 호스팅 서비스중 하나로 Gatsby 사이트를 배포할 수 있습니다.

Surge 를 설치하지 않았다면 새로운 터미널 창을 열고 터미널 툴을 설치 해봅시다.  


```bash
npm install --global surge

# Then create a (free) account with them
surge
```

그런 다음 사이트의 루트에있는 터미널에서 다음 명령을 실행하여 사이트를 빌드하십시오 
(팁 : 사이트의 루트에서이 명령을 실행하고 있는지 확인하십시오. 현재 tutorial-part-one 폴더에 있습니다. 앞서 실행하는 데 사용했던 것과 동일한 창에서 새 탭을 열어서 `gatsby develop` 을 실행 할 수 있습니다.)


```bash
gatsby build
```

빌드 하는데 15-30 초가 걸릴 것입니다. 
이 시점에서 `gatsby build` 명령이 배포하려 준비한 파일을 살펴 보는 것이 유용합니다.
다음 터미널 명령을 사이트의 루트에서 입력하여 생성 된 파일 목록을 `public` 디렉토리 에서 확인 할 수 있습니다.

```bash
ls public
```

그런다음 생성 된 파일을 surge 명령을 통해서 사이트를 배포하십시오.

```bash
surge public/
```

이 작업이 끝나면 터미널에서 다음과 같은 내용을 볼 수 있습니다.

![Screenshot of publishing Gatsby site with Surge](surge-deployment.png)

Open the web address listed on the bottom line (`lowly-pain.surge.sh` in this
case) and you'll see your newly published site! Good work!

## What's coming next?

In this tutorial, you've installed Gatsby, played in the development
environment, and deployed your first site! Awesome! We hope you're enjoying
yourself so far. Feel free to continue now to part two of the tutorial,
["Introduction to using CSS in Gatsby"](/tutorial/part-two/), or go exploring around
the rest of the site.
