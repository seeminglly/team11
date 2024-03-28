# team11
서버시스템구축실습 11팀
팀원: 박지호, 강세민, 신민정, 온수옥, 임혜진, 최지우
* * *

## 1. 프로젝트 개요

### 1.1 프로젝트 주제 및 설명

{서비스이름}은 영화 검색을 통해 해당 영화의 촬영지 및 배경지, 명소에 대한 정보를 제공하고, 각 영화나 장소에 대한 정보를 사용자들이 직접 입력하여 공유할 수 있는 서비스이다. 

### 1.2 주제 선정 이유

코로나로 한 때는 영화 산업이 죽었다는 얘기가 있었지만, OTT의 등장으로 여전히 영화는 많은 사람들이 즐기는 문화 중 하나이다. 영화를 보면서 해당 장소에 가보는 일명 ‘성지순례’ 또한 경험하는 사람이 늘어가고 있는 추세이다. 지금까지는 성지순례를 위한 정보를 직접 하나하나 검색해보거나 영화를 보면서 찾아가는 번거로움이 있었기 때문에 조금 더 편하게 정보를 얻기 위해 이와 같은 서비스를 선정하였다.

### 1.3 프로젝트 언어 및 환경

프로젝트 언어로는 JavaScript, 개발도구는 Node.js와 GCP, 데이터베이스는 MySQL를 사용하였다.

---

## 2. 연구 내용

### 2.1 주요 서비스

{서비스이름}은 아래와 같은 핵심 서비스를 제공한다.

1. 영화 데이터를 이용한 영화 검색 기능
2. 영화 평점 및 비슷한 영화 추천 기능
3. 영화 속 명소 정보 제공
4. 영화에 대한 리뷰와 장소 후기를 남길 수 있는 게시판 기능
5. 영화 및 장소를 저장할 수 있는 즐겨찾기 기능
6. 마이페이지를 통해 자신이 쓴 리뷰 조회, 즐겨찾기 목록 조회 기능

### 화면 흐름도
![메인페이지](https://github.com/seeminglly/team11/assets/80025304/4611ebdf-2d4f-40d8-99e7-170e44c9c47d)



---

## 3. 데이터베이스 설계

### 3.1 요구사항 명세서

1. 웹사이트에 회원으로 가입하려면 회원아이디, 비밀번호, 이름, 나이, 닉네임을 입력해야 한다.
2. 회원은 회원아이디로 식별한다.
3. 영화에 대한 영화 번호, 영화 제목, 제작년도, 감독, 출연자, 장르, 별점 정보에 대한 정보를 유지해야 한다.
4. 영화는 영화번호로 식별한다.
5. 하나의 영화는 여러 장소의 작품이 될 수 있고, 한 곳의 장소가 여러 영화의 장소로 쓰일 수 있다.
6. 장소에 대한 장소 번호, 지명, 주소, 영화번호, 지도에 표시할 사진이 저장된 파일경로에 대한 정보를 유지해야 한다.
7. 장소는 장소 번호로 식별한다.
8. 배우는 배우 번호, 이름, 출연영화에 대한 정보를 유지해야 한다.
9. 배우는 각 배우에 주어진 고유한 번호(배우번호)로 식별한다.
10. 한 영화에 여러 배우가 출연할 수 있고, 한 명의 배우가 여러 영화에서 등장할 수 있다.
11. 영화 리뷰 작성에는 회원아이디, 닉네임, 영화 번호, 글 번호, 글 내용, 작성일자, 별점에 대한 정보를 유지해야 한다.
12. 영화 리뷰의 별점 초기 값은 0.0 이다.
13. 장소 후기 작성에는 회원 아이디, 닉네임, 장소 번호, 글 번호, 글 내용, 별점에 대한 정보를 유지해야 한다.
14. 영화 리뷰 게시글과 장소 후기 게시글은 각 글에 부여된 글 번호로 식별한다.
15. 게시글의 수정 및 삭제는 게시글의 글 번호와 회원아이디로 판별하여 권한을 가진다.
16. 영화 리뷰에는 영화 번호, 회원아이디에 대한 정보를 유지해야 한다.

- 의견 나눠봐야 할 것
    - 영화 밑에 리뷰를 쓰는 것보다는 영화 번호로 데이터 이어질 수 있게 영화 리뷰 게시판이랑 장소 후기 남기는 게시판 두 개로 나누는 것 어떤지.
    - 장소 후기 게시판을 따로 만든다면, 장소 후기에도 별점을 남길 것인지.
    - 영화랑 장소 당 리뷰는 하나씩만 작성 가능하도록 할지, 아니면 여러 개 작성 가능하도록 할지 -> 영화는 하나 장소는 여러 개 또는 영화랑 장소 모두 여러 개
    - 마이페이지에 비밀번호 변경이나 닉네임 변경 기능을 추가하자고 말이 나왔는데, 우리가 지금 구현하고자 하는 서비스에 집중해서 즐겨찾기 목록 조회와 내 리뷰 조회하는 기능을 대신 추가하면 어떨지
    - 영화 정보에 여러 회원들의 별점 평균 나눠서 영화에 대한 별점 정보도 추가하는 건 어떨지
    - 장소에 대한 별점 평균 추가
    - 리뷰 조회 추가

### 3.2 개념적 설계
