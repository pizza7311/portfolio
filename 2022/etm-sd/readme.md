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

