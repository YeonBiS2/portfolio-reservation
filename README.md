# 뷰티샵 예약 웹사이트 제작 프로젝트
##### 진행 기간 : 2021.10.28 ~ 2021.11.30
***
[>기획 서류 보기](https://docs.google.com/presentation/d/1xz1dUmLcSBKLsGCIZbe461g0_D9stIBzCUA10Tc2SYA/edit?usp=sharing)
    
    + 프로젝트 시작 시 구상했던 화면/기능/DB와 실제 구현한 화면을 확인하실 수 있습니다.
***

### 1. 사용한 기술 및 개발 환경

> Language
+ Java - version 8
+ Javascript
+ JQuery
+ HTML
+ CSS


> Framework
+ SpringBoot
+ Gradle
+ Ajax

> DB
+ MySQL

***

### 2. 주요 기능
> A. 메인페이지, 검색페이지의 검색 기능
1. 메인 페이지
    + 카테고리 버튼 클릭 또는 검색창에 검색어(업종 or 업체명 일부) 입력 시 검색 페이지로 넘어가며, 검색 페이지에는 검색된 리스트가 출력됩니다.

2. 검색 페이지
    + 카테고리 버튼 클릭 또는 검색창에 새로운 검색어(업종 or 업체명 일부) 입력 시 화면에 새로운 검색 내역이 반영된다.
    + 셀렉트 박스에서 지역을 선택 시 출력되어있는 검색 리스트에서 해당 지역에 존재하는 업소만 남깁니다.
    + 라디오 버튼을 클릭해 조회수 높은 순, 조회수 낮은 순, 비용 높은 순, 비용 낮은 순으로 정렬할 수 있습니다.


> B. 상세페이지, 마이페이지의 예약, 변경, 취소 기능
1. 상세 페이지
    + 검색 페이지에서 간략히 출력된 업체 정보를 선택하면 선택한 업체의 상세 페이지로 이동합니다.
    + 상세 페이지에서는 데이터베이스에 저장된 업체 정보 조회가 가능합니다. 아래 달력의 날짜(지난 날짜는 선택할 수 없습니다.)를 선택하면 달력의 오른쪽 영역에서 이미 예약된 시간들을 확인할 수 있습니다.
    + 로그인 한 상태에서 달력의 날짜를 선택한 뒤, 오른쪽 셀렉트 박스에서 원하는 시간을 선택하고 예약 버튼을 누르면 point 결제 이후 예약이 완료됩니다.

2. 마이 페이지
    + 마이 페이지는 로그인 이후 접근이 가능합니다.
    + 가입되어있는 개인 정보와 예약 정보를 확인할 수 있습니다.
    + 예약 취소 버튼을 누르면 예약이 취소되며, 결제했던 point를 돌려받습니다.
    + 예약 변경 버튼을 누르면 예약 날짜/시간으로 세팅되어있는 상세페이지로 이동합니다. 상세 페이지에서 다시 원하는 날짜/시간을 선택한 후 예약 변경 버튼을 누르면 예약 정보가 변경됩니다.


> C. 기타 기능
1. 회원 가입 기능
2. ID/비밀번호 찾기 기능
3. 로그인 기능
    + 해당 프로젝트에서는 스프링 시큐리티로 기능이 구현되어 있습니다.
4. 상세 페이지 클릭 시 조회수 갱신 기능
5.리뷰 댓글 기능
    + 상세 페이지에서 리뷰 댓글 작성이 가능하며, 마찬가지로 상세 페이지에서 리뷰 댓글 리스트를 확인할 수 있습니다.


***

### 3. 구현 작업
> A. 검색 기능
* GET 방식으로 검색어를 간단히 파라미터로 넘기고, ModelAndView를 이용해 검색 결과를 JSTL로 화면에 띄웠습니다.
* URL에서 파라미터값을 가지고 오는 방식으로 검색창에 검색어를 유지시키고, 지역 셀렉트 박스에서도 값이 유지될 수 있도록 했습니다.
* 컨트롤러에서 데이터를 넘길 때, HashMap에 특정 값을 함께 넘기는 방식으로 정렬 필터 선택값이 유지될 수 있도록 했습니다.

> B. 예약/변경/취소 기능
* DB상 존재하는 회원의 point를 예약할 업소의 price만큼 차감하는 방식으로 간단하게나마 결제 기능을 구현했습니다. point 결제가 성공했을 때에만 예약을 진행할 수 있습니다.
* 달력의 날짜를 클릭할 때마다 Ajax를 통해 예약 일정이 검색되고, 새로고침 없이 달력의 오른쪽 영역에서 이미 예약된 시간 일정 리스트를 확인할 수 있게 했습니다.
* 이미 예약이 완료된 시간은 셀렉트 박스에서 삭제 되어 되어있으며, 예약 기능은 선택한 시간, 날짜와 회원의 idx, 업체의 idx를 저장하는 방식으로 이루어져 있습니다.
* 예약 취소는 마이페이지에서만 가능하도록 되어있습니다. 예약리스트에서 확인할 수 있는 예약 날짜, 예약 시간, 회원의 idx와 예약된 업체의 idx를 모두 확인해 해당 예약만 삭제합니다.
* 마이페이지 예약리스트에서 선택해 변경 버튼을 눌렀을 때, 예약 시간, 날짜 등의 정보를 넘겨받아 세팅된 해당 업체의 상세페이지로 이동합니다. 원하는 날짜, 시간을 선택하면 예약 정보를 Update해 예약 내용을 변경할 수 있습니다.

> C. 기타 기능
* 회원가입 기능 : Ajax를 활용해 POST 방식으로 input란에 입력된 정보를 DB에 저장합니다.
* ID/ 비밀번호 찾기 기능 : 이름과 연락처, ID와 이름을 파라미터로 받아 찾은 정보를 alert으로 띄웠습니다.
* 로그인 기능 : 스프링 시큐리티로 기능이 구현되어 있습니다. 들었던 수업 과정에 스프링 시큐리티가 포함되어 있지 않았고, 선생님께서 경험 삼아 따로 공부해보라고 설정해주셨습니다. 접근 권한과 관련된 부분과 대체적인 흐름 정도만 이해하고 있습니다.
* 상세페이지 조회수 갱신 기능 : 상세페이지에 접근할 때 넘어가는 idx를 활용해 조회수를 Update합니다.
* 리뷰 댓글 기능 : 예약했던 회원이 서비스 후기를 작성하는 목적으로 만들어진 기능이지만 간단히 댓글을 작성하고, 작성된 댓글을 리스트로 띄우는 정도로만 구현되어 있습니다. 보기 좋게 리스트로 띄우기 위해 innerJoin을 사용했습니다.

***


> 사용된 리소스 출처
* 모든 이미지 : [픽사베이](https://pixabay.com/ko/)
* 아이콘
    * [로고 아이콘](https://www.flaticon.com/free-icon/click_1545244?term=click&page=1&position=6&page=1&position=6&related_id=1545244&origin=search)
    * [헤어샵 아이콘](https://www.flaticon.com/free-icon/hairdresser_3465230?term=hair&page=1&position=6&page=1&position=6&related_id=3465230&origin=search)
    * [네일샵 아이콘](https://www.flaticon.com/free-icon/manicure_3461937?term=nail&page=1&position=6&page=1&position=6&related_id=3461937&origin=search)
    * [마사지샵 아이콘](https://www.flaticon.com/premium-icon/bath-towel_2948446?term=massage&page=1&position=8&page=1&position=8&related_id=2948446&origin=search)