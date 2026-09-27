# Assignment 04 - HTML Form & Validation

* 이름: 김근원 (22100072)
* GitHub Repository: https://github.com/kim-geun-won/2026_assign04
* Vercel Deploy URL: https://2026-assign04.vercel.app
* Clone Coding 원본 URL: https://getbootstrap.com/docs/5.2/examples/checkout/

## 파일 구성

index.html: 세 Form 페이지로 가는 링크 모음
form1.html: Bootstrap Checkout 예제의 Form 구조를 HTML로만 클론
form1_css.html: form1.html에 CSS 적용
form1_js.html: form1_css.html에 HTML Validation과 JavaScript 검사 적용

---

## Weekly Review

### Key Learning

1. `<form>` 안에서 `label`의 `for`와 `input`의 `id`를 연결하면, 글자를 클릭해도 입력칸이 선택된다.

2. CSS의 `:focus`, `:hover` 같은 상태 선택자로 사용자가 지금 어떤 칸을 쓰고 있는지 보여줄 수 있다.

3. `required`, `type="email"`, `minlength` 같은 HTML 속성으로 규칙을 정하고, JavaScript의 `checkValidity()`로 그 규칙을 검사할 수 있다.

### Form Elements

`input type="text"`: 이름, 성, 사용자명, 주소, 우편번호, 카드 정보

`input type="email"`: 이메일

`input type="password"`: 카드 비밀번호 앞 2자리

`input type="radio"`: 결제 방법 (신용카드 / 체크카드 / PayPal), 같은 `name`으로 묶어 하나만 선택되게 함

`input type="checkbox"`: 청구지 주소 동일 여부, 정보 저장 여부

`input type="date"`: 희망 배송일

`input type="color"`: 선물 포장 색상

`select` + `optgroup`: 지역 선택 (수도권 / 영남권 / 기타로 그룹)

`datalist`: 국가 입력 시 자동완성 목록

`textarea`: 배송 요청사항

`fieldset` + `legend`: "배송 정보"와 "결제 방법" 두 구역으로 나눔

원본 Checkout 예제에는 date, color, textarea, datalist, optgroup이 없어서 주문 상황에 어울리는 항목(희망 배송일, 포장 색상, 요청사항 등)으로 추가했다.

### HTML vs CSS

* form1.html은 CSS가 없어서 모든 입력칸이 기본 모양으로 한 줄에 이어 붙어 보인다.

* form1_css.html에서는 `label`을 `display: block`으로 바꿔 입력칸 위로 올리고, 입력칸은 `width: 100%`로 폭을 맞췄다.

* Form 영역에 흰 배경, 테두리, `border-radius`를 주어 카드처럼 보이게 했다.

* checkbox와 radio는 `display: flex`로 글자와 한 줄에 정렬했다.

* 입력칸을 클릭하면(`:focus`) 테두리가 파란색이 되고, 버튼에 마우스를 올리면(`:hover`) 색이 진해진다.

### Validation & JS

HTML Validation

* `required`: 이름, 성, 사용자명, 이메일, 주소, 카드 비밀번호

* `type="email"`: 이메일

* `minlength`: 이름 2자, 사용자명 4자, 카드 비밀번호 2자

JavaScript 처리 과정

1. `addEventListener("submit", ...)`로 제출 이벤트를 받는다.

2. `event.preventDefault()`로 페이지가 새로고침되는 기본 제출을 막는다.

3. 검사할 입력칸을 위에서부터 차례로 `checkValidity()`로 확인한다.

4. 잘못된 칸이 있으면 `alert()`로 안내하고, `focus()`로 그 칸으로 이동한 뒤 `return`으로 함수를 끝낸다.

5. 모두 통과하면 "등록이 완료되었습니다." 메시지를 띄운다.

빈칸 제출, 이메일에 `abc` 입력, 사용자명 2자 입력으로 실패 동작을 확인했고, 모든 칸을 올바르게 채워 성공 메시지도 확인했다.

### Problem & Solution

* 문제 1: `required`를 넣은 상태에서 제출하면 브라우저가 먼저 "이 입력란을 작성하세요" 말풍선을 띄우고 제출을 막아서, 내가 작성한 JavaScript 검사 코드가 실행되지 않았다.

  * 해결: `<form>`에 `novalidate`를 추가했다. 브라우저의 자동 검사만 꺼지고 `required`, `minlength` 규칙은 남아 있어서 `checkValidity()`로 직접 검사할 수 있었다.

* 문제 2: VS Code 터미널이 이전 폴더 경로에 머물러 있어서 `git status`에 파일이 보이지 않았다.

  * 해결: File → Open Folder로 저장소 폴더를 다시 열고 새 터미널을 열어 경로를 맞췄다.

### Reflection

* `novalidate`를 쓰면 HTML 속성이 무의미해질 줄 알았는데, 규칙은 그대로 남고 "누가 검사하느냐"만 바뀐다는 점이 새로웠다.

* 궁금한 점: 실제 서비스에서는 JavaScript 검사를 브라우저에서 끌 수도 있을 텐데, 서버에서는 어떻게 한 번 더 검사하는지 알고 싶다.
