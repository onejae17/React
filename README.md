# 202230137 최원재

# 4/29 (9주차)

### UI를 트리 구조로 이해하기 - Render 트리

- 예제를 분석하고 Render 트리를 구성할 때는 컴포넌트의 부모, 자식관계 즉 호출한 곳이 어디인가를 확인함
- 트리는 노드로 구성되어 있으며, 각 노드는 컴포넌트를 나타냄
- App, FancyText, Copyright 등은 모두 트리의 노드임
- React Render 트리에서 루트 노드는 앱의 Root 컴포넌트임
- 이 경우 루트 컴포넌트는 App이며 React가 렌더링하는 첫 번째 컴포넌트임
- 트리의 각 화살표는 부모 컴포넌트에서 자식 컴포넌트를 가리킴
- DOM 트리와는 달리 Render 트리는 HTML 태그 없이 React 컴포넌트로만 구성됨

###  UI를 트리 구조로 이해하기 – 모듈 의존성 트리

- 모듈 의존성 트리는 React의 또다른 트리 구조 모델링 방법으로 모듈의 종속성을 나타냄
- 컴포넌트와 로직을 별도의 파일로 분리하면 컴포넌트 뿐만 아니라 함수 또는 상수를 export할 수 있는 JS 모듈을 만들 수 있음
- 모듈 의존성 트리의 각 노드는 모듈이며, 가지는 해당 모듈의 import 문을 나타냄
- 트리의 루트 노드는 루트 모듈이며, 엔트리 포인트 파일이라고도 함
- Render 트리 비교 차이점
    1. 트리를 구성하는 노드는 컴포넌트가 아닌 모듈을 나타냄
    2. inspiration.js와 같은 컴포넌트가 아닌 모듈도 이 트리에 나타남
    3. Render 트리는 컴포넌트만 캡슐화 하지만 모듈 트리는 모듈도 포함함 (컴포넌트 + 모듈)
- 일반적으로 앱이 커짐에 따라 번들 크기도 커짐
- 번들 크기가 그려지는 데 시간이 지체될 수 있음
- 또한 UI가 그려지는 데 시간이 지체될 수 있음

### jsx에 스타일 적용하기

- jsx에 스타일 적용하는 방법은 매우 다양 : 일반 CSS, 인라인 CSS, CSS-in-JS, CSS 프레임워크, css Module
- React에 권장하는 방법은 CSS Module

### 일반 CSS

- 가장 간단하게 사용할 수 있는 방법으로 HTML에서 CSS를 사용하는 방법과 동일함
- style.css 파일을 만들어서 필요한 스타일을 정의한 후에 사용할 컴포넌트에서 import한 후 사용함
- 단, 속성의 이름으로 class가 아닌 className을 사용합니다. 이 것은 앞에서 소개한 모든 방법에서 동일하게 적용됨
- 익숙한 방법이기 때문에 프로젝트에 빠르게 적용할 수 있다는 장점을 가지고 있음
- 컴포넌트 단위로 관리하기가 어렵고, 전역 스코프(global)의 클래스 이름과 충돌 가능성이 있기 때문에 주의해야 함

### 인라인 스타일
- HTML에서도 인라인 스타일은 유지보수의 어려움 등의 단점이 있어서 자주 사용하는 방법은 아님
- 조건부 스타일에서만 제한적으로 사용됨
- 속성 이름은 kebab-case가 아닌 camelCase를 사용해야 함

### CSS-in-JS

- 자바스크립트 코드 내에서 CSS를 직접 작성하여, 컴포넌트 단위로 스타일을 관리하는 방법임
- styled-components, emotion, JSS 등 외부 라이브러리를 사용함

- 장점
    - 스타일이 컴포넌트 내에 바인딩되기 때문에 관리와 유지보수가 용이함
    - props를 기반으로 한 동적(조건부) 스타일링 적용에 매우 편리함
    - 고유한 클래스명을 자동으로 생성하여 스타일의 충돌을 방지함
    - Provider 컴포넌트를 통해 전역 테마 설정을 쉽게 적용할 수 있음

- 단점
    - 스타일을 문자열로 변환하여 삽입하는 과정에서 런타임 성능의 저하가 발생할 수 있음
    - 라이브러리 추가로 인한 자바스크립트 번들 사이즈가 커짐
    - 기존 CSS/SCSS와 다른 각 라이브러리 고유의 문법을 학습해야 함

### CSS Mudule

- CSS Module은 클래스명을 [클래스이름]_[해쉬값]의 형태로 자동 변환하여, 고유한 이름의 로컬 스코프(Local Scope)를 제공하는 기술
- 컴포넌트 기반의 프레임워크인 React나 Vue 등에서 채택하고 있는 이 기술은 스타일의 충동을 완벽하게 방지할 뿐만 아니라 유지보수에도 유리함
- 컴포넌트 단위로 스타일링 한다는 것이 가장 큰 특징으로 컴포넌트의 재사용에도 유라하게 작용함
- 일반 CSS의 문제점 중 하나는 전역으로 선언되기 떄문애 다른 컴포넌트와 충돌의 위험이 있는 것

### CSS Module 사용 방법

- 파일 이름의 규칙 : 파일 이름은[커모넌트 이름].module.css의 형태로 확장자는 반드시.module.css로 함
- css 작성 :
    - CSS의 내용은 일반 CSS의 작성법을 따르고
    - class 선택자로 스타일을 선언
    - Tag 선택자를 사용하는 것은 특별한 경우가 아니라면 권장하지 않음
    - Tag 선택자는 CSS Module 빌드 시에 고유한 이름을 할당 받지 않고, 전역으로 사용되기 때문

### 실습
~~~jsx
import style from "./ButtonCom.module.css"

export default function ButtonCom() {
    return (
        <>  
            <h1 className={style.title}>ButtonCom 컴포넌트</h1>
            <nav className={style.navBar}>
                <button>버튼1</button>
                <button>버튼2</button>
            </nav>
        </>
        
    )
}
-------------------------------------------
.title {
    color: salmon;
    text-align: center;
}
.navBar {
    display: flex;
    justify-content: center;
    gap: 20px;
}
~~~

### 이벤트에 응답하기
- React에서는 JSX에 이벤트 핸들러를 추가할 수 있음
- 이벤트 핸들러는 클릭, 마우스 호버(hover), 폼 입력의 포커스 등 사용자와의 상호작용에 따라 유발되는 사용자 정의함수임

### 이벤트 핸들러 추가하기 [실습]

~~~jsx
import style from "./ButtonCom.module.css"

export default function ButtonCom() {
    function handleClick() {
        alert("버튼 클릭")
    }

    return (
        <>  
            <h1 className={style.title}>ButtonCom 컴포넌트</h1>
            <nav className={style.navBar}>
                <button onClick={handleClick} className={style.myButton}>
                    버튼1
                </button>
                <button onClick={handleClick} className={style.myButton}>
                    버튼2
                </button>
            </nav>
        </>
        
    )
}
~~~

# 4/15 (7주차)

### 배열의 항목들을 필터링하기 [실습]
~~~jsx
import {heroes} from './HeroesData'; 

export default function MovieHeroes() {
    const filterTest = heroes.filter(hero =>
        hero.name === '피터 파커'
    );
    const listHeroes = filterTest.map(hero =>
    <li>
        <p>
            {hero.name}의 배역은 {hero.casting}입니다
        </p>
    </li>
    );
    return (
        <section>
            <h1>영화 속 영웅들</h1>
            <ul>
                {listHeroes}
            </ul>
        </section>
    );
}
// HeroesData --------------------------------------------
export const heroes = [
    {
    id: 0,
    casting: "스파이더맨",
    name: "피터 파커",
    },
    {
    id: 1,
    casting: "아이언맨",
    name: "토니 스타크",
    },
    {
    id: 2,
    casting: "배트맨",
    name: "브루스 웨인",
    },
    {
    id: 3,
    casting: "슈퍼맨",
    name: "클라크 켄트",
    },
    {
    id: 4,
    casting: "헐크",
    name: "로버트 브루스 배너",
    }
]
~~~

### 복수 데이터 필터링 [실습]
~~~jsx
import {heroes} from './HeroesData'; 

export default function MovieHeroes() {
    const filterTest = heroes.filter(hero =>
        hero.power === 3
    );
    const listHeroes = filterTest.map(hero =>
    <li>
        <p>
            {hero.name}의 배역은 {hero.casting}입니다
        </p>
        <p>
            {hero.name}의 파워는 {hero.power}입니다
        </p>
    </li>
    );
    return (
        <section>
            <h1>영화 속 영웅들</h1>
            <ul>
                {listHeroes}
            </ul>
        </section>
    );
}
// ---------------------------------------------------
export const heroes = [
    {
    id: 0,
    casting: "스파이더맨",
    name: "피터 파커",
    power: 4,
    },
    {
    id: 1,
    casting: "아이언맨",
    name: "토니 스타크",
    power: 5,
    },
    {
    id: 2,
    casting: "배트맨",
    name: "브루스 웨인",
    power: 3,
    },
    {
    id: 3,
    casting: "슈퍼맨",
    name: "클라크 켄트",
    power: 5,
    },
    {
    id: 4,
    casting: "헐크",
    name: "로버트 브루스 배너",
    power: 4
    }
]
~~~

### key prop를 사용하는 이유
- key prop은 배열 중 어떤 자식 요소인지 확인할 수 있도록 한다
- key prop은 배열의 자식 요소가 정렬 등으로 인해 이동, 삽입 혹은 삭제되어도 각 자식 요소를 구별하는데 중요하게 사용됨
- key prop은 즉석해서 생성하는 것이 아니고, 배열 안에 포함되어 있어야 함

### 컴포넌트를 순수하게 유지하기
- 순수 함수
    - 같은 입력 값을 넣으면 항상 같은 결과를 반환하는 함수
    - 외부의 상태를 변경하지 않는 즉, 사이드 이펙트(side effect)가 없는 함수를 의미함

### 순수함수로 구현되는 컴포넌트 [실습]
~~~jsx
import OrderUp from "./OrderUp";

export default function Kiosk() {
  return (
    <section>
        <h2>치즈버거 세트 메뉴를 주문하세요</h2>
        <p>일반 세트 : </p>
      <OrderUp order={1} />
        <p>패밀리 세트 : </p>
      <OrderUp order={2} />
    </section>
  );
}
// ------------------------------------
import OrderUp from "./OrderUp";

export default function Kiosk() {
  return (
    <section>
        <h2>치즈버거 세트 메뉴를 주문하세요</h2>
        <p>일반 세트 : </p>
      <OrderUp order={1} />
        <p>패밀리 세트 : </p>
      <OrderUp order={2} />
    </section>
  );
}
~~~

### 사이드 이펙트(Side Effect): 의도하지 않은 결과 [실습]
~~~jsx
let guest = 0;

function Cup() {
  // 컴포넌트 외부의 guest 변수를 변경하고 있습니다. 🚨
  guest = guest + 1;
  return <h2>Tea cup for guest #{guest}</h2>;
}

export default function TeaSet() {
  return (
    <>
      <Cup />
      <Cup />
      <Cup />
    </>
  );
}
// ------------------------------------
function Cup({ guest }) {
    // 컴포넌트 외부의 guest 변수를 변경하고 있습니다. 🚨
  return <h2>Tea cup for guest #{guest}</h2>;
}

export default function TeaSet() {
  return (
    <>
      <Cup guest={1} />
      <Cup guest={2} />
      <Cup guest={3} />
    </>
  );
}
// ------------------------------------
function Cup({ guest }) {
    // 컴포넌트 외부의 guest 변수를 변경하고 있습니다. 🚨
  return <h2>Tea cup for guest #{guest}</h2>;
}

export default function TeaSet() {
  const cups =[];
    for (let i = 1; i <= 12; i++) {
      cups.push(<Cup key={i} guest={i}/>);
    }
  return cups;
}
~~~

# 4/8 (6주차)

### 조건부로 JSX 반환하기 [실습]
~~~jsx
import Item from "./Item";

export default function PackingList() {
    return (
        <section>
            <h1>여행 준비 목록</h1>
            <ul>
                {/* <li>여분 옷</li>
                <li>책</li>
                <li>노트북</li> */}
                <Item name="여분 옷" isPacked={true} />
                <Item name="책" isPacked={true} />
                <Item name="노트북" isPacked={true} />
            </ul>
        </section>
    )
}
// ---------------------------------
export default function Item({name, isPacked}) {
    if (isPacked) {
        return <li>{name} ✔</li>
    }
    return <li>{name}</li>
}
~~~

### 중복된 코드 제거하기 [실습]
~~~jsx
// 실습 1
export default function Item({name, isPacked}) {
    return (
        <li>
            {isPacked ? (
            <del>
                {name + " ✔"}
            </del>
            ) : (
                name
            )}
        </li>
    )
}
// ------------------------------------------------
// 실습 2

export default function Item({name, isPacked}) {
    let itemContent = name
    if (isPacked) {
        itemContent = <del>{name + " ✔"}</del>
}
    return (<li>{itemContent}</li>)

}
~~~

### 논리 연산자 AND(&&) 사용하기

~~~jsx
export default function Item({name, isPacked}) {
    return (
        <li>
            {name} {isPacked && "✔"}
        </li>
    )
}
~~~

### 리스트 렌더링
- 컴포넌트에서 여러 개의 데이터를 같은 형식으로 출력해야 하는 경우가 있다
- 이럴 때는 JavaScript의 배열관련 함수를 사용해서, 배열을 컴포넌트의 기능에 맞게 렌더링할 수 있다.



# 4/1

### JSX로 마크업 작성하기 [실습]

1. 따옴표로 문자열을 전달하는 방법
2. 중괄호를 이용해서 JavaScript 변수를 참조하는 방법
3. 중괄호를 이용해서 JavaScript 함수를 호출하는 방법
4. 중괄호를 이용해서 JavaScript 객체를 적용하는 방법

~~~jsx
import NamedComponentTest from './components/NamedComponentTest'
import Gallery from './components/Profile'
import UseJsx from './components/UseJsx'

export default function App() {
  return (
    <>
      {/* <NamedComponentTest/>
      <Gallery /> */}
      <UseJsx />  
    </>
  )
}
~~~

### 함수 사용 요일 추가 [실습]

~~~jsx
export default function UseJsx() {
    const name = 'React'

    function foramtDate(date) {
        return new Intl.DateTimeFormat(
            "en-US", 
            { weekdate: "long" },
        ).format(date)
    }
    return (
        <>
            <h1>Hello, {name}</h1>
            <p>Today is {foramtDate(new Date())}</p>
        </>
    )
}
~~~

### Props의 데이터 전달
- React에선, props를 통해 JSX 태그에 정보를 전달 -> 예를 들어,
src, alt, width, height의 속성값을 <img> 태그에 전달할 수 있음

- <img> 태그에 전달할 수 있는 props는 HTML 표준으로 이미 정의되어 있음

### 컴포넌트에 props 전달하기
- 부모 컴포넌트 (Parent Component)
    - 자식 컴포넌트를 자신의 구조 안에 포함(import 및 호출)하고, 데이터를 전달(props)하는 컴포넌트
- 자식 컴포넌트 (Child Component)
    - 부모 컴포넌트로 부터 전달받은 props를 통해 구체적인 UI를 만들어서 부모 컴포넌트에 다시 반환함
    - 독립적으로 재사용될 수 있음

~~~jsx
// 실습 1
import ChildComp from "./ChildComp"

export default function ParentComp() {
    return (
        <>
            <ChildComp alt="React" width={100}
             height={100}/>
        </>
    )
}
// ----------------------------------------
import reactLogo from '../assets/react.svg'



export default function ChildComp({alt, width, height}) {
  return (
    <>
      <img className="button-icon" src={reactLogo} alt={alt} 
      width={width} height={height} />
    </>
  )
}
~~~

~~~jsx
// 실습2
import ChildComp from "./ChildComp"
import reactLogo from '../assets/react.svg'

export default function ParentComp() {
    return (
        <>
            <ChildComp 
                imageInfo={
                    {
                        src: reactLogo,
                        alt: "React",
                    }
                } 
            width={100}
            height={100}/>
        </>
    )
}
// ----------------------------------------
export default function ChildComp({imageInfo, width, height}) {
  return (
    <>
      <img className="button-icon" src={imageInfo.src} alt={imageInfo.alt} 
      width={width} height={height} />
    </>
  )
}
~~~

### Props의 기본값 지정

- 부모 컴퐆넌트로부터 전달받은 prop이 없을 때는 기본값을 지정해 줄 수 있음
- 지정할 때는 변수 뒤에 = 과 함께 기본값을 넣음

~~~jsx
// 실습
export default function ChildComp({imageInfo, width=300, height}) {
  return (
    <>
      <img className="button-icon" src={imageInfo.src} alt={imageInfo.alt} 
      width={width} height={height} />
    </>
  )
}
// -------------------------------------
import ChildComp from "./ChildComp"
import reactLogo from '../assets/react.svg'
import viteLogo from '../assets/vite.svg'

export default function ParentComp() {
    return (
        <>
            <ChildComp 
                imageInfo={{
                        src: reactLogo,
                        alt: "React",
                    }} 
                />
            <ChildComp 
                imageInfo={{
                        src: reactLogo,
                        alt: "React",
                    }} 
            width={100}
            height={100}/>
            <ChildComp
                imageInfo={{
                        src: viteLogo,
                        alt: "Vite",
                    }}
                width={200}
                height={200}

            />
        </>
    )
}
~~~

### JSX spread 문법으로 props 전달하기
- 모든 props를 한 번에 자식 컴포넌트에 전달하는 방법은 자바 스크립트의 spread 문법 이용
- 전달받은 props 그대로 넘겨줄 때 : 부모 컴포넌트가 받은 props를 중간 단계 컴포넌트가 그대로 자식에게 토스할 때 매우 유용함

~~~jsx
// 실습
import NameCard from "./NameCard"

export default function SpreadComp() {
    const userData = {
        id: 1,
        name: "Tom",
        age: 25,
        job: "Developer",
        location: "Seoul",
    }

    return (
        <>
            <NameCard {...userData} />
        </>
    )
}
// -----------------------------------
export default function NameCard({ ...userData }) {
    return (
        <div>
            <h2>사용자 정보</h2>
            <p>ID: {userData.id}</p>
            <p>이름: {userData.name}</p>
            <p>나이: {userData.age}</p>
            <p>직업: {userData.job}</p>
            <p>거주지: {userData.location}</p>
        </div>
    )
}
~~~

# 3/25

### 2026/3/12 vite 업데이트
- 플러그인 관련 항목은 실험적인 통합 단계로 이슈 발생가능성 있음

### vite의 트렌스파일러에서 javascript + SWC가 사라진 이유
- 전 - 자바스크립트 선택 - babel
- 현 - 자바스크립트 선택 - 0xc
- 이유 : 특별한 이유가 아니라면 굳이 babel을 사용할 이유가 없기 때문
- 명령어로 프로젝트 생성할 때 -swc를 빼고 사용해야 됨

### 0xc와 swc
- 둘다 rust로 작성되어 매우 빠른 속도를 자랑하는 차세대 자바스크립트/타임스크립트 도구

#### swc
- 바벨을 대체하기 위해 만들어진 컴파일러 및 번들러
- 트랜스파일링과 번들링에 특화
- 바벨을 완벽하게 대체할 수 있어 현대적인 프레임워크에서 기본으로 사용됨

#### 0xc
- 트랜스파일러 등을 모두 대체하려는 고성능 도구 모음

#### 컴포넌트 중첩(Nesting)

- React에서의 중첩은 특정 컴포넌트를 다른 컴포넌트 안에서 호출하는 것을 의미
- 호출이지 선언이라 이해해서는 안됨

#### Default Export와 Named Export의 차이
- Default Export의 사용
1. import 키워드 다음에 다른 이름으로 변수명을 선언할 수 있음
2. 이 이름을 로컬 식별자 혹은 변수명이라고 함
3. 변수명은 대문자로 시작

- Named Export를 사용
1. export하는 곳과 import하는 곳의 컴포넌트의 이름이 같아야 함
2. 모듈에 여러 개의 named 컴포넌트가 있을 경우 전부 혹은 일부만 import해서 사용할 수 있음

#### Named Export를 권장하는 이유
1. 일관성 : 팀원 모두가 같은 컴포넌트를 같은 이름으로 부르게 됨
2. 리팩토링 용이성 : 커모넌트 이름을 바꿀 때, 에디터가 연결된 모든 파일의 이름을 한꺼번에 안전하게 바꿔줌
3. 트리 쉐이킹(Tree Shaking) : 사용하지 않는 코드를 제거하는 과정에서 Named Export가 더 유리한 경우가 많음
# 3/18

### React Project
#### 도입 방법
1. React 프레임워크를 사용하지 않고 직접 React 앱을 개발하는 방법.
2. 기존 프로젝트 일부에만 React를 도입하는 방법.
3. 새로운 React 앱을 개발하는 경우의 도입 방법.

- 프로젝트를 생성해도 git은 직접 초기화해야함

#### 컴포넌트 만들기 전
- 어디에 사용할 컴포넌트인가?
- 어떤 기능을 구현할 것인가?
- 재사용이 가능한 컴포넌트로 구현할 것인가?
- 컴포넌트 이름은 무엇으로 할 것인가?
- 어떤 디렉토리에 만들 것인가?

### 나의 첫 번째 컴포넌트 만들기


# 3/11

### Git의 학습 방법
- [초급을 위한 필수 명령어]
    - git init
    - git add .
    - git commit -m "설명"
    - git remote add origin URL

- [고급]
    - Pull Request(PR), 충돌 해결, Git 기록 정리 등의 학습이 목표
    - 이 단계에서는 "*Git 히스토리를 정리하는 법과 PR를 활용한 협업*"이 중요
- [고급을 위한 명령어]
    - git pull request
    - git fetcch-pick <commit-id>
    - git reset --soft HEAD~1
    - git revert <commit-id>
    - git reflog
### .gitignore
- Git 버전 관리에서 제외할 파일이나 디렉터리 목록을 정의하는 설정 파일
- .gitignore 파일 생성후 필요한 파일을 입력

### Node.js
- 라이언 달은 2009년 Node.js를 발표
- 비동기 논 블로킹 방식으로 고성능 처리 가능
- javascript 풀스택 개발 가능
- 활발한 생태계 : npm을 통해 다양한 패키지 사용 가능

- 경량 서버 개발에 적합
- 실시간 데이터 처리가 강력
#### React 이전과 이후의 개발 방식의 차이
* 이전
1. HTML과 CSS를 이용하여 화면을 만들고 
2. JavaScript로 DOM을 직접 조작
3. 특정 이벤트 발생 -> 필요한 부분만 수정
4. 화면이 복잡해질 수록 수정과 DOM 추적이 어려워짐
* 이후(React가 나온 이후)
1. 화면을 직접 고치지 않고 state를 바꾸면, 화면은 다시 계산됨 -> DOM을 조작하지 않고 렌더링을 함
    - React에서 렌더링이란 "현재 상태(state)를 기준으로 UI를 다시 계산하는 과정
2. 개발자는 DOM을 어떻게 고칠지를 고민하지 말고, 상태가 무엇인지만 정의하면 됨
#### 공식 문서에서 소개하는 React
- React를 잘 쓴다는 것은 상태와 렌더링의 관계를 명확하게 설명할 수 있고, 사용할 수 있는것
1. 왜 이 상태(state)가 여기 있어야 하는지 설명할 수 있어야함
2. 왜 이 컴포넌트가 다시 렌더링 되는지를 설명할 수 있어야 함
3. 왜 effect가 필요한지 혹은 필요 없는지를 설명할 수 있어야 함
#### React를 잘 쓴다는 것의 의미
- UI를 컴포넌트 단위로 개발해서 레고를 조립하듯이 완성

