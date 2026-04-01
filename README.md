# 4/1

### JSX로 마크업 작성하기

1. 따옴표로 문자열을 전달하는 방법
2. 중괄호를 이용해서 JavaScript 변수를 참조하는 방법
3. 중괄호를 이용해서 JavaScript 함수를 호출하는 방법
4. 중괄호를 이용해서 JavaScript 객체를 적용하는 방법

- 
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

### 함수 사용 요일 추가

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

