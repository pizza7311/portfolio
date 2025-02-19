## COOS
화장품 원료 정보검색과 원료 판매자와 구매자를 연결시켜주는 플랫폼 [https://coos.kr/](https://coos.kr/) 의 프론트엔드와 백엔드 개발을 담당하였습니다.

## 기술 스택

### Front-end
* Next.js
* Apollo graphql

### Back-end
* Express.js
* Apollo server
* MongoDB

### Deploy
* vultr cloud
* Ubuntu
* nginx

## 담당 업무
### 스팸관리 어드민 페이지 기능 개발
![img](https://github.com/pizza7311/portfolio/blob/main/2025/coos/images/1.png)
coos의 기능중 판매업체가 판매할 원료를 홍보할수있도록 게시글을 등록할수있습니다. 해당 기능은 유료 기능으로 멤버십에 가입된 사용자만 판매자의 연락처가 노출되며 멤버십이 없는 경우 게시글을 등록할순있지만 판매자의 연락처는 가려집니다.  
  
하지만 이 제한을 우회하려고 악의적으로 설명을 적는 부분에 회사의 연락처를 적어놓는 사용자들이 있어 해당 사용자들을 걸러내기 위해 스팸관리 기능을 개발하였습니다.
사용자가 작성하는 게시물에 연락처,이메일 등 홍보 문구가 포함된 게시글을 찾아 목록으로 보여주며 어드민 페이지에서 삭제 처리할수있는 기능을 개발하였습니다.  
  
### 데이터 스크래핑 기능 업데이트
기존 cron으로 외부 사이트를 스크래핑하여 데이터를 업데이트하는 기능 있습니다. 해당 기능은 7000건 이상의 목록을 반복문을 돌며 갱신을 하는방식으로 동작하는데 아래의 문제점들이 있었습니다.  
1. 외부 사이트에서 요청 차단
2. cron을 실행하는 서버 자체에 에러가 발생하여 중단됨
3. 업데이트 해야할 데이터 자체가 외부 사이트에서 사라진경우(url이 404로 바뀜)

위의 문제 때문에 매일 cron은 실행되지만 모든 데이터가 완벽하게 갱신되는 경우는 드물었습니다.  
이 문제를 해결하기위해 db에 해당 사이트의 마지막 검증 시간 필드를 추가하고 반복문을 돌기전에 검증시간을 기준으로 정렬하여 cron 실행시 오래전에 업데이트된 데이터를 가장 최우선으로 갱신하도록 수정하였습니다.  

https://github.com/user-attachments/assets/882bd14c-0773-42e5-a775-e95fb4f1db48

또한 어드민 페이지에서 데이터 업데이트 현황을 한눈에 보기위한 최신 데이터와 오래된 데이터를 확인할수있는 그래프를 개발하였습니다.  


### 검색 랭킹 생성 기능 개발
사용자가 검색창
