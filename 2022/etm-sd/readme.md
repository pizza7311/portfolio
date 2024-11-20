# ETM-SD
전기회로 도안을 그리기 위한 (figma 와 비슷한) 웹 브라우저 기반 svg 에디터 입니다.
프론트엔드 에디터 개발과 관리 기능 백엔드 API(직원 로그인,도안 관리,파일 업로드 등) 개발을 담당하였습니다.

개발 기간 : 2022/03 ~ 2023/05 (중도 퇴사)
기여도 : 90% (디자인과 css를 제외한 모든 개발 작업 진행)

## 기술 스택
### Front-end
* React
* Fabric.js
* Paper.js

### Back-end
* Koa.js
* MariaDB

### Deploy (On-premise)
* Ubuntu
* Nginx

## 주요 기능


![main](https://github.com/pizza7311/portfolio/blob/main/2022/etm-sd/images/main.png)

프로젝트의 핵심 기능인 svg 에디터 개발을 전담하였습니다. 기존 사용자들이 어도비 일러스트레이터를 사용하고 있어서 최대한 어도비 일러스트레이터와 비슷하게 개발을 진행했습니다.

### 도형 그리기
![shapes](https://github.com/pizza7311/portfolio/blob/main/2022/etm-sd/images/shapes.gif)

### 눈금자 및 가이드라인
![rulerAndGuideline](https://github.com/pizza7311/portfolio/blob/main/2022/etm-sd/images/ruler-guideLine.gif)
메인 작업 영역을 기준으로 상단과 좌측에 눈금을 표시해주는 기능입니다. 화면 이동(panning)에 따라 눈금도 같이 이동하며 줌 in/out 비율에 맞춰 눈금이 조절되는 기능이 있습니다.
눈금자를 클릭하고 드래그하면 가이드라인을 꺼내서 길이를 측정할수 있습니다.

### 객체 스냅핑
![snapping](https://github.com/pizza7311/portfolio/blob/main/2022/etm-sd/images/snapping.gif)
에디터에서 특정 옵션을 켜면 작업영역에서 객체를 움직일때 가장 가까운 객체에 자동으로 스냅되는 기능입니다.

### 커스텀 단축키 지정
![customShortcuts](https://github.com/pizza7311/portfolio/blob/main/2022/etm-sd/images/shortCuts.gif)
에디터의 툴에 등록된 단축키를 사용자가 직접 지정하여 사용할수있는 기능입니다.

### 객체 변형 기능
![detailSelectExample](https://github.com/pizza7311/portfolio/blob/main/2022/etm-sd/images/detailSelectExample.webp)  
**(이해를 위한 예시용 이미지)**  
svg를 구성하고있는 path와 point를 직접 선택해여 요소를 변형시킬수 있는 기능입니다. 어도비 일러스트레이터에서 '직접 선택' 이라는 이름의 기능을 해당 프로젝트에 구현하였습니다.
  
  
## 개발중 겪은 문제들과 해결 과정

### 커스텀 단축키 기능 구현
해당 기능을 어떻게 구현해야할까 고민하며 비슷한 예시를 찾기위해 여러 여러 자료들을 찾던중 [boxy.svg](https://boxy-svg.com/app) 라는 온라인 svg 에디터를 발견했고 이 에디터에 [단축키 설정](https://boxy-svg.com/app?dialog=settings%E2%86%92keyboard)이 있는걸 발견하여 이 기능이 어떻게 동작하는지 분석하였습니다.  
![shortcutExample](https://github.com/pizza7311/portfolio/blob/main/2022/etm-sd/images/customShortcutExample.png)  
해당 기능이 단축키마다 key값을 가지고 있으며 로컬 스토리지에 변경된 key값을 저장한다는걸 확인한후 툴 마다 key 테이블을 정의하고 해당 key 이벤트가 발생했을때 지정된 툴로 전환하도록 구현하였습니다.
![appliedShortcuts](https://github.com/pizza7311/portfolio/blob/main/2022/etm-sd/images/appliedShortcuts.png)  
해당 기능은 아래의 원리대로 동작합니다.
* 단축키 지정탭에서 수정할 단축키를 클릭하여 수정모드 진입
* 수정 모드에선 사용자의 키보드 입력을 기록
* 기록된 키보드 조합을 로컬스토리지에 저장하며 해당 키보드 조합 이벤트가 발생하면 등록된 툴로 전환
  
  
### 두개의 패키지를 사용한 하이브리드 앱 개발
![detailSelectExample](https://github.com/pizza7311/portfolio/blob/main/2022/etm-sd/images/detailSelectExample.webp)  
이 이미지의 기능을 구현하기 위해선 svg 객체를 point와 path 단위로 직접 변형해야하는 작업이 필요했습니다.  
fabric.js에서는 이 기능을 지원하지 않았고 여러 시도를 해보았지만 fabric.js로는 개발이 불가능하다는 결론이 나왔습니다.  
하지만 이 기능은 반드시 필요한 사항이라 다른 자료를 찾던중 paper.js 라는 패키지를 발견했습니다.  
이 패키지는 svg를 point와 path 단위로 직접 조작할수 있는 기능이 있어 위의 요구사항을 충족하였지만 이미 개발이 많이 진행된 상황에서 paper.js로 처음부터 만들순 없는 상황이었습니다.  
그래서 기존의 fabric.js 에디터는 그대로 사용하되 '직접 선택' 기능 이 활성화 되었을때 fabric.js의 svg를 paper.js로 마이그레이션 하고 paper.js 에디터에서 작업후 그 결과를 다시 fabric.js로 옮기는 방식으로 구현하였습니다.  
위 이미지의 예시는 실제로 [paper.js로 구현된 에디터](https://w00dn.github.io/papergrapher/) 의 소스코드를 분석하여 구현하였습니다.  
이 기능은 아래의 순서대로 동작합니다.
* fabric.js에서 변형할 객체를 선택하고 '직접 선택' 모드 클릭
* 선택된 객체만 svg 형태로 추출
* 에디터 영역위에 새로운 paper.js 에디터를 생성하고 추출한 svg를 전달 후 위치 및 크기등 을 조절하여 삽입
* paper.js 에디터에서 작업후 저장 버튼을 눌렀을때 작업한 paper.js에서 작업한 svg를 추출
* 추출한 svg를 fabric.js에 다시 옮긴후 위치 및 크기등 을 조절하여 삽입
* 사용한 paper.js 에디터를 화면상에서 제거
  
### 사용중인 패키지의 소스코드 분석 및 오버라이딩
기능을 구현하기 위해 fabric.js의 메소드의 내부 동작을 수정해야할 일이 있었습니다. 예를 들어 `fabric.funcA()` 를 호출했을때 이 메소드 내부에서는 A와 B라는 두 가지 기능을 수행하고있었습니다.
하지만 이중 A기능만 필요하고 B는 실행이 되면 안되는 경우가 있어서 fabric.js의 소스코드 에서 fabric.funcA() 라는 메소드를 찾아 분석하고 A기능만 수행하도록 수정하여 해결한 경험이 있습니다.

### github 리포지토리에서 개발자와 직접 소통
패키지에서 지원하지 않는 기능이나 문서의 내용대로 동작하지 않는 경우 또는 버그를 발견했을때 해당 패키지의 리포지토리에 직접 질문과 문제사항을 올려 패키지 개발자들과 의견을 주고 받으며 소통한 경험이 있습니다.
