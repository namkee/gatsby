---
title: Gatsby.js Tutorial Part Four
typora-copy-images-to: ./
---

튜토리얼의 제 4 부에 오신 것을 환영합니다! 반 정도 진행된 겁니다! 
희망적인 것은 꽤 편안하게 느끼기 시작한 것일 겁니다.😀

그러나 너무 편안하지 마십시오😉. 
이번 튜토리얼에서는 완전히 이해하려면, 약간의 두뇌 스트레칭이 필요한 새로운 영역으로 향하고 있거든요.
이 튜토리얼의 다음 두 부분에서는 Gatsby의 강력한 기능인 Gatsby 데이터 레이어를 살펴봅니다. 데이터 레이어를 통해서 Markdown, WordPress, 헤드리스 CMS 및 기타 모든 데이터 소스에서 사이트를 쉽게 만들 수 있습니다.

**NOTE:** Gatsby의 데이터 계층은 GraphQL을 사용합니다. 
GraphQL을 처음 접 하셨다면이 부분이 약간 압도 될 것입니다. 
GraphQL에 대한 심도있는 튜토리얼을 보려면 [How to GraphQL](https://www.howtographql.com/)을 참조하십시오.

## 튜토리얼 전반부 요점 정리

지금까지 우리는 React.js를 사용하는 방법을 배웠습니다. 
웹 사이트의 커스텀 요소 역할을 하는 _자체_ 컴포넌트를 만드는 것이 얼마나 강력한 것인지 말이죠.

우리는 또한 CSS 모듈과 CSS-in-JS를 사용하여 스타일링 구성 요소를 탐구했습니다.
이 구성 요소 내에서 CSS를 캡슐화 할 수 있습니다.

## Data in Gatsby

웹 사이트는 HTML, CSS, JS 및 데이터의 네 부분으로 구성됩니다. 
튜토리얼의 전반부는 처음 세 부분에 중점을 둡니다. 이제 Gatsby 사이트에서 데이터를 사용하는 방법을 배우게 됩니다. 

데이터 란 무엇입니까?

컴퓨터 과학 스러운 대답은 아마 `"strings"`, integers (`42`), objects (`{ pizza: true }`) 등과 같은 것일 겁니다.

그러나 Gatsby 로 작업하기 위해서는 "React 컴포넌트 외부에있는 모든 것"이 더 유용한 대답이됩니다.

지금까지 텍스트를 작성하고 이미지를 컴포넌트에 _직접_ 추가했습니다. 이미 수 많은 웹 사이트를 구축했던 _훌륭한_ 방법입니다. 
하지만 종종 컴포넌트의 _외부에_ 데이터를 저장 하고, 필요에 따라 데이터를 컴포넌트로 가져오려고 할 경우가 있습니다. 

예를 들어, WordPress로 사이트를 구축하는 경우 (다른 참여자가 콘텐츠를 추가하고 유지하기위한 좋은 인터페이스를 가짐),
Gatsby 에서는 사이트 (페이지 및 게시물)의 _데이터_가 WordPress에 있고 필요에 따라 해당 데이터를 _가져와_ 이를 구성 요소에 추가합니다.


Markdown, CSV 등의 파일 유형뿐만 아니라 모든 종류의 데이터베이스 및 API 가 데이터가 될수 있습니다.

** Gatsby의 데이터 레이어를 사용하면 이러한 데이터(여러 소스)의 데이터를 구성 요소로 직접 가져올 수 있습니다. 
우리가 원하는 모양과 형태로 데이터를 가져올 수 있습니다.

## How Gatsby's data layer uses GraphQL to pull data into components

React 컴포넌트에 데이터를 로드하는 방법은 여러 가지 옵션이 있습니다. 
가장 인기 있고 강력한 도구 중 하나는 [GraphQL](http://graphql.org/) 이라는 기술입니다.

GraphQL은 Facebook 에서 엔지니어가 필요한 데이터를 컴포넌트에 _pull_ 할 수 있도록 개발되었습니다.

GraphQL은 **q**uery **l**anguage (이름의 _QL_ 부분)입니다. SQL에 익숙하다면 매우 유사한 방식으로 작동합니다. 
특수 구문을 사용하면 컴포넌트에 원하는 데이터를 설명하고 그 데이터가 사용자에게 제공됩니다.

Gatsby는 GraphQL을 사용하여 컴포넌트 에서 필요한 데이터를 선언 할 수 있도록합니다.

## Our first GraphQL query

이전 부분과 같이 이 튜토리얼의 이 파트를 위해서 또 다른 새 사이트를 생성해 보겠습니다. 
우리는 "Pandas Eating Lots"라는 Markdown 블로그를 만들 예정입니다. 
그것은 많이 먹는 팬더의 최고의 사진과 비디오를 보여주는 데 전념합니다. 
그 과정에서 우리는 GraphQL과 Gatsby의 Markdown 지원하는 부분에 발을 담궈 볼것 입니다.

새 터미널 창에서이 명령을 실행하십시오.

```shell
gatsby new tutorial-part-four https://github.com/gatsbyjs/gatsby-starter-hello-world
```

그런 다음 프로젝트의 루트에 다른 필요한 의존 라이브러리들을 추가해 설치하십시오. 

Typography 테마 Kirkham 와 CSS-in-JS 라이브러리 [Glamorous](https://glamorous.rocks/) 를 사용해 보겠습니다. 
새로운 `tutorial-part-four` 디렉토리로 이동하여 다음을 실행하십시오.

```shell
npm install --save gatsby-plugin-typography gatsby-plugin-glamor glamorous typography-theme-kirkham
```

3 부에서 끝내었던 것과 유사한 사이트를 만들어 보겠습니다. 
이 사이트에는 레이아웃 컴포넌트와 두 개의 페이지 컴포넌트가 있습니다.

`src/pages/index.js`

```jsx
import React from "react";

export default () => (
  <div>
    <h1>Amazing Pandas Eating Things</h1>
    <div>
      <img
        src="https://2.bp.blogspot.com/-BMP2l6Hwvp4/TiAxeGx4CTI/AAAAAAAAD_M/XlC_mY3SoEw/s1600/panda-group-eating-bamboo.jpg"
        alt="Group of pandas eating bamboo"
      />
    </div>
  </div>
);
```

`src/pages/about.js`

```jsx
import React from "react";

export default () => (
  <div>
    <h1>About Pandas Eating Lots</h1>
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </div>
);
```

`src/layouts/index.js`

```jsx
import React from "react";
import g from "glamorous";
import { css } from "glamor";
import Link from "gatsby-link";

import { rhythm } from "../utils/typography";

const linkStyle = css({ float: `right` });

export default ({ children }) => (
  <g.Div
    margin={`0 auto`}
    maxWidth={700}
    padding={rhythm(2)}
    paddingTop={rhythm(1.5)}
  >
    <Link to={`/`}>
      <g.H3
        marginBottom={rhythm(2)}
        display={`inline-block`}
        fontStyle={`normal`}
      >
        Pandas Eating Lots
      </g.H3>
    </Link>
    <Link className={linkStyle} to={`/about/`}>
      About
    </Link>
    {children()}
  </g.Div>
);
```

`src/utils/typography.js`

```javascript
import Typography from "typography";
import kirkhamTheme from "typography-theme-kirkham";

const typography = new Typography(kirkhamTheme);

export default typography;
```

`gatsby-config.js` (must be in the root of your project, not under src)

```javascript
module.exports = {
  plugins: [
    `gatsby-plugin-glamor`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
};
```

위의 파일을 추가 한 다음 `gatsby develop` 실행하면 다음이 표시됩니다.

![start](start.png)

우리는 레이아웃과 두 페이지가있는 또 다른 작은 사이트를 만들었습니다.

이제 query 를 시작하겠습니다. 😋

사이트를 구축 할 때 사이트 전체에서 공통된 데이터를 재사용하는 것이 일반적입니다. 
예를 들어 _사이트 제목_과 같습니다. `/about/` page를 보십시오. 
레이아웃 컴포넌트 (사이트 헤더)와 정보 페이지 제목에 모두 사이트 제목이 있음을 알 수 있습니다. 
그러나 앞으로 어떤 시점에서 사이트 제목을 변경하려면 어떻게해야합니까? 사이트 제목을 사용하는 스팟에 대해서는 모든 구성 요소를 검색하고 각 제목 인스턴스를 편집해야합니다. 
이 과정은 복잡하고 오류가 발생하기 쉽습니다.
 특히 사이트가 더 커지고 복잡해지면 더욱 그렇습니다. 
 제목을 한 곳에 저장 한 다음 필요할 때마다 해당 제목을 구성 요소로 _pull_ 하는 것이 훨씬 좋습니다.

이를 해결하기 위해 `gatsby-config.js` 파일에 페이지 제목이나 설명과 같은 사이트 "메타 데이터"를 추가 할 수 있습니다. 
`gatsby-config.js` 파일에 사이트 제목을 추가 한 다음 레이아웃 및 페이지에 대해 쿼리하십시오!

gatsby-config.js 를 수정해 봅시다.

```javascript{2-4}
module.exports = {
  siteMetadata: {
    title: `Blah Blah Fake Title`,
  },
  plugins: [
    `gatsby-plugin-glamor`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
};
```
개발 서버를 다시 시작하십시오.

그런 다음 두 컴포넌트를 수정해주세요.

`src/pages/about.js`

```jsx{3,5-7,14-23}
import React from "react";

export default ({ data }) =>
  <div>
    <h1>
      About {data.site.siteMetadata.title}
    </h1>
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </div>

export const query = graphql`
  query AboutQuery {
    site {
      siteMetadata {
        title
      }
    }
  }
`
```

`src/layouts/index.js`

```jsx{10,19,28-33}
import React from "react";
import g from "glamorous";
import { css } from "glamor";
import Link from "gatsby-link";

import { rhythm } from "../utils/typography";

const linkStyle = css({ float: `right` })

export default ({ children, data }) =>
  <g.Div
    margin={`0 auto`}
    maxWidth={700}
    padding={rhythm(2)}
    paddingTop={rhythm(1.5)}
  >
    <Link to={`/`}>
      <g.H3 marginBottom={rhythm(2)} display={`inline-block`}>
        {data.site.siteMetadata.title}
      </g.H3>
    </Link>
    <Link className={linkStyle} to={`/about/`}>
      About
    </Link>
    {children()}
  </g.Div>

export const query = graphql`
  query LayoutQuery {
    site {
      siteMetadata {
        title
      }
    }
  }
`
```

잘 동작합니다!! 🎉

![fake-title-graphql](fake-title-graphql.png)

이제 진짜 제목으로 복원해 봅시다.

Gatsby 의 핵심 원칙 중 하나는 제작자가 제작중인 내용에 즉시 적용되어야 한다는 것입니다.
([hat tip to Bret Victor](http://blog.ezyang.com/2012/02/transcript-of-inventing-on-principleb/)). 
즉, 코드를 변경하면 해당 변경의 영향을 즉시 확인해야합니다. 
Gatsby의 입력을 조작하면 새 출력이 화면에 표시됩니다.

거의 모든 곳에서 변경 사항이 즉시 적용됩니다.

`siteMetadata` 에서 제목 편집해서 제목을 "Pandas Eating Lots"로 다시 변경하십시오. 브라우저에서 변경 사항이 매우 빠르게 나타납니다.

## Wait — where did the graphql tag come from?

`graphql` 이라는 [tag function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_template_literals)를 사용했음을 알았지만 
실제로는 `graphql` 태그를 _import_ 하지 않았습니다. 음... 어떻게 오류가 발생하지 않았을까요?

짧은 살명하면 다음과 같습니다.
Gatsby 빌드 프로세스 중에 Graphql 쿼리를 구문 분석을 위해 원본 소스에서 제거/추출합니다.

더 긴 대답은 좀 더 복잡합니다. 
Gatsby는 빌드 단계에서 소스 코드를 [abstract syntax tree (AST)](https://en.wikipedia.org/wiki/Abstract_syntax_tree)로 변환하는 
[Relay](https://facebook.github.io/relay/) 기술을 사용합니다. 

모든 `graphql` 태그가있는 템플릿은 [`file-parser.js`](https://github.com/gatsbyjs/gatsby/blob/v1.6.3/packages/gatsby/src/internal-plugins/query-runner/file-parser.js#L63)
와 [`query-compiler.js`](https://github.com/gatsbyjs/gatsby/blob/v1.6.3/packages/gatsby/src/internal-plugins/query-runner/query-compiler.js)에 있으며, 
원본 소스 코드에서 효과적으로 제거합니다. 
이는 `graphql` 태그가 예상 하는대로 실행되지 않는다는 것을 의미합니다. 
우리가 기술적으로 소스에서 정의되지 않은 태그를 사용하고 있음에도 불구하고 오류가없는 것입니다.

## Introducing Graph_i_QL

Graph_i_QL 은 GraphQL 통합 개발 환경 (IDE)입니다. Gatsby 웹사이트를 개발하는 과정에서 종종 사용하게되는 강력한 도구 입니다.

서버가 정상동작하고 있다면 다음의 주소를 통해서 접근 할수 있습니다. <http://localhost:8000/___graphql>.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="/graphiql-explore.mp4"></source>
  <p>Your browser does not support the video element.</p>
</video>

여기서 우리는 내장 된 `Site` "type"과 앞서 쿼리 한 `siteMetadata` 객체를 포함하여 어떤 필드가 사용 가능한지 살펴 봅니다. 

Graph_i_QL 을 열어보고 데이터와 함께 놀아보죠! 

<kbd>Ctrl + Space</kbd> 를 누르면 자동 완성 창이 나타나고 <kbd>Ctrl + Enter</kbd>를 누르면 쿼리가 실행됩니다. 
우리는 Graph_i_QL을 나머지 튜토리얼을 통해 더 많이 사용할 것입니다.


## Source plugins

Gatsby 사이트의 데이터는 API, 데이터베이스, CMS, 로컬 파일 등 어디서나 올 수 있습니다.

소스 플러그인은 소스에서 데이터를 가져옵니다. 예를들어 
파일 시스템 소스 플러그인은 파일 시스템에서 데이터를 가져 오는 방법을 구현하고 있습니다. 
WordPress 플러그인은 WordPress API에서 데이터를 가져 오는 방법을 구현하고 있습니다.


우선 [`gatsby-source-filesystem`](/packages/gatsby-source-filesystem/) 을 추가하고 어떻게 동작하게 되는지 알아봅시다.

프로젝트 루트에서 플러그인을 인스톨 합니다.

```sh
npm install --save gatsby-source-filesystem
```

그리고 `gatsby-config.js` 파일에 다음을 추가합니다.`:

```javascript{6-12}
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    `gatsby-plugin-glamor`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
};
```

저장한후 개발서버를 재시작 합니다. 그리고 Graph_i_QL 을 다시 열어봅니다.

자동 완성 창이 나타나면 다음과 같이 표시됩니다.

![graphiql-filesystem](graphiql-filesystem.png)

`allFile` 항목을 선택하고 <kbd>Enter</kbd> 를 누릅니다. 그리고 <kbd>Ctrl + Enter</kbd> 를 누르면 쿼리를 실행합니다. 

![filesystem-query](filesystem-query.png)

쿼리 부분에서 `id` 를 제거하고 자동완성 창을 나타나게 합니다. (<kbd>Ctrl + Space</kbd>).

![filesystem-autocomplete](filesystem-autocomplete.png)

쿼리에서 몇개의 필드를 추가하고, <kbd>Ctrl + Enter</kbd> 를 누르면 각기 쿼리가 재실행됩니다.
그러면 다음과 같이 표시됩니다. 

![allfile-query](allfile-query.png)

파일 "nodes"의 배열이 결과입니다.(node 는 "graph" 에서 쓰이는 객체를 지칭하는 이름입니다.)
각 파일 객체는 우리가 쿼리한 필드를 가지고 있습니다.

## Build a page with a GraphQL query

Gatsby로 새로운 페이지를 만드는 것은 종종 Graph_i_QL 에서 시작됩니다. 

먼저 Graph_i_QL 에서 실행하여 데이터 쿼리를 만들어 본 다음, 이를 React 페이지 컴포넌트에 복사하여 UI 작성을 시작합니다.

한번 해보도록 하죠.

`src/pages/my-files.js` 파일을 생성하고 `allFile` 쿼리를 추가해 봅시다.

```jsx{4}
import React from "react"

export default ({ data }) => {
  console.log(data)
  return <div>Hello world</div>
}

export const query = graphql`
  query MyFilesQuery {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

`console.log(data)` 라인이 하일라이팅되어 있습니다. 
UI 를 새롭게 만드는 과정에서 새로운 컴포넌트를 생성하면서, 브라우저 콘솔에 데이터를 탐색 할 수 있도록 쿼리 결과 데이터를 콘솔 로그로 찍는것은 종종 도움이 되는 코드입니다.

`/my-files/` 페이지에 접근하게 되면 브라우저 콘솔에서 다음의 결과를 확인 할 수 있습니다.

![data-in-console](data-in-console.png)

데이터 형태가 쿼리의 형태와 동일합니다.

우리의 컴포넌트에 몇줄의 코드를 추가해서 파일데이터를 출력해 보도록 합시다.

```jsx{5-37}
import React from "react"

export default ({ data }) => {
  console.log(data)
  return (
    <div>
      <h1>My Site's Files</h1>
      <table>
        <thead>
          <tr>
            <th>relativePath</th>
            <th>prettySize</th>
            <th>extension</th>
            <th>birthTime</th>
          </tr>
        </thead>
        <tbody>
          {data.allFile.edges.map(({ node }, index) =>
            <tr key={index}>
              <td>
                {node.relativePath}
              </td>
              <td>
                {node.prettySize}
              </td>
              <td>
                {node.extension}
              </td>
              <td>
                {node.birthTime}
              </td>
            </tr>
          )}
        </tbody>
      </table>
    </div>
  )
}

export const query = graphql`
  query MyFilesQuery {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

그러면 ... 😲

![my-files-page](my-files-page.png)

## Transformer plugins

Often, the format of the data we get from source plugins isn't what you want to
use to build your website. The filesystem source plugin lets you query data
_about_ files but what if you want to query data _inside_ files?

To make this possible, Gatsby supports transformer plugins which take raw
content from source plugins and _transform_ it into something more usable.

For example, Markdown files. Markdown is nice to write in but when you build a
page with it, you need the Markdown to be HTML.

Let's add a Markdown file to our site at
`src/pages/sweet-pandas-eating-sweets.md` (This will become our first Markdown
blog post) and learn how to _transform_ it to HTML using transformer plugins and
GraphQL.

흔히 소스 플러그인에서 얻는 데이터의 형식은 웹 사이트를 구축하는 데 사용하려는 형식이 아닙니다. 
파일 시스템 소스 플러그인을 사용하면 _파일에 대한 데이터_를 쿼리 할 수 있지만 _파일 내부의 데이터_를 쿼리하려면 어떻게해야합니까?

이를 가능하게하기 위해 Gatsby는 소스 플러그인에서 원시 컨텐츠를 가져 와서 더 유용한 것으로 _변환_ 하는 트랜스포머 플러그인을 지원합니다.

Markdown 파일을 예로 들어봅시다. Markdown은 글을 쓰는 것이 좋지만, 웹 페이지로 보여주려면 Markdown 내용이 곧 HTML이어야합니다.

Markdown 페이지를 `src/pages/sweet-pandas-eating-sweets.md` (이것이 첫번째 마크다운 블로그 포스팅이 될겁니다) 에 추가하고
Markdown 파일을 Transform 플러그인과 GraphQL을 사용하여 HTML로 _변환_하는 방법을 배워 봅시다.

```markdown
---
title: "Sweet Pandas Eating Sweets"
date: "2017-08-10"
---

Pandas are really sweet.

Here's a video of a panda eating sweets.

<iframe width="560" height="315" src="https://www.youtube.com/embed/4n0xNbfJLR8" frameborder="0" allowfullscreen></iframe>
```

파일을 저장하고 나서 `/my-files/` 를 다시 봅니다. 
새 Markdown 파일이 테이블에 있습니다. 
이것은 Gatsby 의 매우 강력한 특징입니다. 
앞서 `siteMetadata` 예제와 마찬가지로 소스 플러그인도 데이터를 다시로드 할 수 있습니다. 
`gatsby-source-filesystem` 은 항상 추가 할 새 파일을 검색하고 검색 할 때 쿼리를 다시 실행합니다.

Markdown 파일을 변형 할 수있는 변환기 플러그인을 추가해 보겠습니다.


```shell
npm install --save gatsby-transformer-remark
```

그리고 `gatsby-config.js` 파일에 추가합니다. 

```javascript{13}
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    `gatsby-transformer-remark`,
    `gatsby-plugin-glamor`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
};
```

개발서버를 재시작하고 Graph_i_QL 을 새로고침(혹은 새로 불러들여서) 자동완성 부분을 확인해보세요. 

![markdown-autocomplete](markdown-autocomplete.png)

`allMarkdownRemark`을 다시 선택하고 `allFile` 때 했던 것처럼 실행해봅시다.
최근에 추가한 마크다운 파일을 확인 할 수 있습니다. 
`MarkdownRemark` 노드에서 사용할수 있는 필드들을 한번 살펴 보세요. 

![markdown-query](markdown-query.png)

좋아요! 몇몇 기초적인 기능이 잘동작하기를 바래봅니다.
소스 플러그인은 Gatsby 의 데이터 시스템에 데이터를 가져오고 
트랜스포머 플러그인은 소스 플러그인으로 가져온 원시 컨텐츠를 변환합니다. 
이 패턴을 통해서 Gatsby 사이트를 구축 할 때 필요할 수있는 모든 데이터 소싱 및 데이터 변환을 처리 할 수 있습니다.


## Create a list of our site's Markdown files in `src/pages/index.js`

이제 Markdown 파일 목록을 첫 페이지에 보여주도록 해 보겠습니다. 
많은 블로그와 마찬가지로, 각 블로그 게시물을 가리키는 첫 페이지의 링크 목록을 보여주도록 하는것이 목표입니다.
GraphQL을 사용하면 목록을 수동으로 관리 할 필요가 없도록 Markdown 블로그 게시물의 현재 목록을 _query_ 할 수 있습니다.

`src/pages/my-files.js` 에서 `src/pages/index.js` 를 다음과 같이 변경합니다.
쿼리를 추가하고 기본 HTML 과 스타일링을 추가했습니다. 

```jsx
import React from "react";
import g from "glamorous";

import { rhythm } from "../utils/typography";

export default ({ data }) => {
  console.log(data);
  return (
    <div>
      <g.H1 display={"inline-block"} borderBottom={"1px solid"}>
        Amazing Pandas Eating Things
      </g.H1>
      <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
      {data.allMarkdownRemark.edges.map(({ node }) => (
        <div key={node.id}>
          <g.H3 marginBottom={rhythm(1 / 4)}>
            {node.frontmatter.title}{" "}
            <g.Span color="#BBB">— {node.frontmatter.date}</g.Span>
          </g.H3>
          <p>{node.excerpt}</p>
        </div>
      ))}
    </div>
  );
};

export const query = graphql`
  query IndexQuery {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          excerpt
        }
      }
    }
  }
`;
```

이제 첫번째 페이지는 다음과 같습니다.

![frontpage](frontpage.png)


하지만 아직 블로그 포스트가 조금 외로워보입니다. 다른 포스트 `src/pages/pandas-and-bananas.md` 를 추가해보도록 합시다.


```markdown
---
title: Pandas and Bananas
date: "2017-08-21"
---

Do Pandas eat bananas? Check out this short video that shows that yes! pandas do
seem to really enjoy bananas!

<iframe width="560" height="315" src="https://www.youtube.com/embed/4SZl1r2O_bY" frameborder="0" allowfullscreen></iframe>
```

![two-posts](two-posts.png)

멋지게 잘동작합니다!. 근데 포스트 출력 순서가 잘못 되었습니다. 

그러나 이것은 쉽게 고칠 수 있습니다. 
어떤 유형의 연결을 쿼리 할 때 쿼리에 다양한 인수를 전달할 수 있습니다. 
노드 `sort` 및 `filter`, `skip` 할 노드 수 설정 및 검색 할 노드 수 `limit` 선택. 
이 강력한 연산자 세트를 사용하여 원하는 데이터를 원하는 형식으로 선택할 수 있습니다.

색인 페이지의 검색어에서 `allMarkdownRemark` 를 `allMarkdownRemark(sort: {fields: [frontmatter___date], order: DESC})` 로 변경하십시오. 
이것을 저장하면 정렬 순서가 고정되어야합니다.

Graph_i_QL 을 열고 다른 정렬 옵션으로 재생 해보십시오. `allFile`  연결을 다른 연결과 함께 정렬 할 수 있습니다.


## Programmatically creating pages from data

그래서 이것은 대단합니다! Markdown 파일을 쿼리하는 멋진 인덱스 페이지가 있습니다. 
그러나 우리는 발췌 부분을보고 싶지 않습니다. Markdown 파일의 실제 페이지를 원합니다.

시작하자.

지금까지 우리는 React 컴포넌트를 `src/pages` 에 배치하여 페이지를 만들었습니다. 
이제 _프로그래밍 방식_으로 _data_에서 페이지를 만드는 방법에 대해 알아 보겠습니다. 
Gatsby는 많은 정적 사이트 생성기와 같은 파일에서 페이지를 만드는 것에 국한되지 않습니다. 
Gatsby를 사용하면 GraphQL을 사용하여 데이터를 쿼리하고 데이터를 페이지에 매핑 할 수 있습니다. 
이것은 정말 강력한 아이디어입니다. 
우리는이 튜토리얼의 나머지 부분에서 그 의미와 방법을 탐구 할 것입니다.


새 페이지를 만드는 데는 두 단계가 있습니다.

1. 페이지의 "path" 또는 "slug" 를 생성하십시오.
2. 페이지를 만듭니다.

Markdown 페이지를 만들기 위해 [`onCreateNode`](/docs/node-apis/#onCreateNode)와 [`createPages`](/docs/node-apis/#createPages) 
두 개의 Gatsby API를 사용하는 방법을 배웁니다. 이것들은 많은 사이트와 플러그인에서 사용되는 두 가지 핵심 API입니다.

Gatsby API를 구현하기 위해 최선을 다하고 있습니다. API를 구현하려면 `gatsby-node.js`에서 API 이름으로 함수를 내 보냅니다.

그럼 그렇게 하죠. 사이트 루트에 `gatsby-node.js`라는 파일을 만듭니다. 그런 다음 다음을 추가하십시오. 이 함수는 새로운 노드가 생성 (또는 업데이트) 될 때마다 Gatsby에 의해 호출됩니다.


```javascript
exports.onCreateNode = ({ node }) => {
  console.log(node.internal.type);
};
```

개발 서버를 중지했다가 다시 시작하십시오. 
마찬가지로 새로 생성 된 노드 몇 개가 터미널 콘솔에 기록되는 것을 볼 수 있습니다.

이 API를 사용하여 Markdown 페이지의 슬러그를 `MarkdownRemark` 노드에 추가해 봅시다.

MarkdownRemark 노드 만 바라보도록 함수를 변경하십시오.

```javascript{2-4}
exports.onCreateNode = ({ node }) => {
  if (node.internal.type === `MarkdownRemark`) {
    console.log(node.internal.type)
  }
};
```

우리는 각 Markdown 파일 이름을 사용하여 페이지 슬러그를 생성하려고합니다. 
그래서 `pandas-and-bananas.md`는 `/pandas-and-bananas/`가 될 것입니다.
하지만 `MarkdownRemark` 노드에서 파일 이름을 얻으려면 어떻게해야 할까요?
이를 얻으려면, "node graph" 가 자신의 _부모_ `File` 노드 를 탐색하도록 합니다. `File` 노드는 디스크에있는 특정파일의 데이터가 포함되어 있습니다. 
이렇게하려면 함수를 다시 수정하십시오.

```javascript{1,3-4}
exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    const fileNode = getNode(node.parent)
    console.log(`\n`, fileNode.relativePath)
  }
};
```

터미널에 두 개의 Markdown 파일에 대한 상대 경로가 표시되어야합니다.

![markdown-relative-path](markdown-relative-path.png)

이제는 slug를 만들어 봅시다. 
파일 이름에서 slug를 만드는 로직이 까다로울 수 있으므로 `gatsby-source-filesystem` 플러그인에는 slug 생성 기능이 포함되어 있습니다. 그걸 사용합시다.


```javascript{1,5}
const { createFilePath } = require(`gatsby-source-filesystem`);

exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    console.log(createFilePath({ node, getNode, basePath: `pages` }))
  }
};
```

이 함수는 slug 생성과 함께 부모 `File` 노드를 찾는 것을 처리합니다. 
개발 서버를 다시 실행하면 터미널에 두 개의 슬러그 (각 Markdown 파일에 하나씩)가 기록됩니다.

`MarkdownRemark` 노드에 새로운 slugs를 직접 추가 합시다.
이것은 우리가 노드에 추가하는 모든 데이터를 나중에 GraphQL로 쿼리 할 수 있기 때문에 강력합니다. 
따라서 페이지를 만들 때 슬러그를 쉽게 얻을 수 있습니다.

이를 위해 우리는 [`createNodeField`](/docs/bound-action-creators/#createNodeField) 라는 API 구현체에 전달 된 함수를 사용합니다. 
이 함수는 다른 플러그인에 의해 생성 된 노드에 추가 필드를 생성 할 수있게합니다. 
노드의 원래 생성자 만 노드를 직접 수정할 수 있습니다. 
다른 모든 플러그인 (`gatsby-node.js` 포함)은 이 함수를 사용하여 추가 필드를 만들어야합니다.


```javascript{3,4,6-11}
const { createFilePath } = require(`gatsby-source-filesystem`);

exports.onCreateNode = ({ node, getNode, boundActionCreators }) => {
  const { createNodeField } = boundActionCreators
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
};
```
개발 서버를 다시 시작하고 Graph_i_QL 을 열거나 새로 고칩니다. 
그런 다음이 쿼리를 실행하여 새로운 슬러그를 확인하십시오.

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        fields {
          slug
        }
      }
    }
  }
}
```

이제는 slug가 만들어 졌으므로 페이지를 만들 수 있습니다.

동일한 `gatsby-node.js` 파일에 다음을 추가하십시오. 
여기에서 Gatsby 에게 우리 페이지가 경로는 무엇이며 템플릿 구성 요소는 무엇인지에 대해 알려줍니다.


```javascript{15-34}
const { createFilePath } = require(`gatsby-source-filesystem`);

exports.onCreateNode = ({ node, getNode, boundActionCreators }) => {
  const { createNodeField } = boundActionCreators
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
};

exports.createPages = ({ graphql, boundActionCreators }) => {
  return new Promise((resolve, reject) => {
    graphql(`
      {
        allMarkdownRemark {
          edges {
            node {
              fields {
                slug
              }
            }
          }
        }
      }
    `).then(result => {
      console.log(JSON.stringify(result, null, 4))
      resolve()
    })
  })
};
```

Gatsby가 페이지를 추가하기 위해 호출하는 [`createPages`](/docs/node-apis/#createPages) API 구현을 추가했습니다. 
우리는 방금 생성 한 Markdown slug를 쿼리하기 위해 전달 된 `graphql` 함수를 사용하고 있습니다. 
그런 다음 쿼리 결과를 로그로 출력합니다.


![query-markdown-slugs](query-markdown-slugs.png)

페이지를 생성하려면 페이지 템플릿 컴포넌트가 필요합니다. 
Gatsby의 모든 기능과 마찬가지로 프로그래밍 방식의 페이지는 React 컴포넌트로 제공됩니다. 
페이지를 만들 때 사용할 구성 요소를 지정해 주어야 합니다.

`src/templates` 에 디렉토리를 만들고 `src/templates/blog-post.js` 라는 파일에 다음을 추가하십시오.

```jsx
import React from "react";

export default () => {
  return <div>Hello blog post</div>;
};
```

그리고나서 `gatsby-node.js` 를 다음과 같이 수정하세요.

```javascript{1,17,32-41}
const path = require(`path`);
const { createFilePath } = require(`gatsby-source-filesystem`);

exports.onCreateNode = ({ node, getNode, boundActionCreators }) => {
  const { createNodeField } = boundActionCreators
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
};

exports.createPages = ({ graphql, boundActionCreators }) => {
  const { createPage } = boundActionCreators
  return new Promise((resolve, reject) => {
    graphql(`
      {
        allMarkdownRemark {
          edges {
            node {
              fields {
                slug
              }
            }
          }
        }
      }
    `).then(result => {
      result.data.allMarkdownRemark.edges.forEach(({ node }) => {
        createPage({
          path: node.fields.slug,
          component: path.resolve(`./src/templates/blog-post.js`),
          context: {
            // Data passed to context is available in page queries as GraphQL variables.
            slug: node.fields.slug,
          },
        })
      })
      resolve()
    })
  })
};
```

개발 서버를 다시 시작하면 페이지가 생성됩니다! 
개발하는 동안 만드는 새 페이지를 쉽게 찾을 수있는 방법은 Gatsby가 사이트의 페이지 목록을 유용하게 보여주는 임의의 경로로 이동하는 것입니다. 

<http://localhost:8000/sdf> 로 이동하면 우리가 만든 새 페이지가 표시됩니다.


![new-pages](new-pages.png)

그 중 하나를 방문하면 다음을 볼 수 있습니다.

![hello-world-blog-post](hello-world-blog-post.png)

약간 지루한 내용입니다. Markdown 게시물에서 데이터를 가져와 봅시다. `src/templates/blog-post.js`  를 다음으로 변경하십시오.

Which is a bit boring. Let's pull in data from our Markdown post. Change
`src/templates/blog-post.js` to:

```jsx
import React from "react";

export default ({ data }) => {
  const post = data.markdownRemark;
  return (
    <div>
      <h1>{post.frontmatter.title}</h1>
      <div dangerouslySetInnerHTML={{ __html: post.html }} />
    </div>
  );
};

export const query = graphql`
  query BlogPostQuery($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
    }
  }
`;
```

그러면…

![blog-post](blog-post.png)

좋네요!

마지막 단계는 index 페이지에서 새로운 페이지를 연결하는 것입니다.

`src/pages/index.js`로 돌아가서 Markdown slug를 쿼리하고 링크를 만듭니다.

```jsx{3,18-19,29,47-49}
import React from "react";
import g from "glamorous";
import Link from "gatsby-link";

import { rhythm } from "../utils/typography";

export default ({ data }) => {
  return (
    <div>
      <g.H1 display={"inline-block"} borderBottom={"1px solid"}>
        Amazing Pandas Eating Things
      </g.H1>
      <h4>
        {data.allMarkdownRemark.totalCount} Posts
      </h4>
      {data.allMarkdownRemark.edges.map(({ node }) =>
        <div key={node.id}>
          <Link
            to={node.fields.slug}
            css={{ textDecoration: `none`, color: `inherit` }}
          >
            <g.H3 marginBottom={rhythm(1 / 4)}>
              {node.frontmatter.title}{" "}
              <g.Span color="#BBB">— {node.frontmatter.date}</g.Span>
            </g.H3>
            <p>
              {node.excerpt}
            </p>
          </Link>
        </div>
      )}
    </div>
  )
}

export const query = graphql`
  query IndexQuery {
    allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC }) {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          fields {
            slug
          }
          excerpt
        }
      }
    }
  }
`
```

잘 되었나요? 잘 동작하기는 하지만 여전히 작은 블로그일뿐입니다!

사이트를 좀더 둘러보고 만드는걸 즐겨보세요. 
Markdown 파일을 추가해보십시오. 
`MarkdownRemark` 노드에서 다른 데이터 쿼리를 탐색하고 이를 FrontPage 또는 블로그 게시물 페이지에 추가하십시오.

이 튜토리얼의 이번 부분에서는 Gatsby의 데이터 레이어로 구축하는 기초를 배웠습니다. 
플러그인을 사용하여 데이터를 _source_ 및 _transform_ 하는 방법을 배웠습니다. GraphQL을 사용하여 데이터를 페이지에 매핑하는 방법. 그런 다음 각 페이지의 데이터를 쿼리하는 페이지 템플릿 구성 요소를 작성하는 방법.


And there we go! A working, albeit small, blog!

Try playing more with the site. Try adding some more Markdown files. Explore
querying other data from the `MarkdownRemark` nodes and adding them to the
frontpage or blog posts pages.

In this part of the tutorial, we've learned the foundations of building with
Gatsby's data layer. You've learned how to _source_ and _transform_ data using
plugins. How to use GraphQL to _map_ data to pages. Then how to build _page
template components_ where you query for data for each page.

## Where next?

Now that you've built a Gatsby site, where do you head to next?

You could take a look at some [example sites](https://github.com/gatsbyjs/gatsby/tree/master/examples#gatsby-example-websites) and [plugins](/docs/plugins/), see what [other people are building with Gatsby](https://github.com/gatsbyjs/gatsby/#showcase), or check out the documentation on [Gatsby's APIs](/docs/api-specification/), [nodes](/docs/node-interface/) or [GraphQL](/docs/graphql-reference/).
