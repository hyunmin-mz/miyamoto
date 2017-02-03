# 근태관리bot - 미야모토상(みやもとさん)

Google Apps Script으로 작성된, Slack에서 움직이는 근태관리 Bot.

Slack에서 아래와 같이 말하면, 미야모토상(みやもとさん)이 Google Spreadsheet에 근태를 기록해줍니다.

![demo1](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/demo1.png)


## 대화보기

- 안녕하세요 ← 현재 시간에 출근
- 안녕하세요 12:00 ← 지정된 시간에 출근
- 안녕하세요 10/2 12:00 ← 소급 출근을 기록
- 12:00에 출근했습니다 ← 지정된 시간에 출근
- 수고하셨습니다 ← 현재 시간에 퇴근
- 수고하셨습니다 20:00 ← 지정된 시간에 퇴근
- 20시에 퇴근했습니다 ← 지정된 시간에 퇴근
- 내일은 쉽니다 ← 휴가 신청
- 10/1은 쉽니다 ← 휴가 신청
- 내일 휴가를 취소합니다 ← 휴가 신청 취소
- 내일 역시 출근합니다 ← 휴가 신청 취소

- 누구 있어？ ← 출근중인 목록
- 누가 휴가？ ← 휴가중인 목록
- 9/21은 누가 휴가？ ← 지정일 휴가 목록


# 설치 방법

미야모토상(みやもとさん)은, 프로그램의 본체를 Google Drive에 저장하고 실행합니다. 데이터는 Google Spreadsheet에 저장됩니다.

설치는 다음 단계를 따르십시오.


## Google Apps Script에 설치

### 프로그램 본체를 설치

- https://drive.google.com/ 를 열고, 화면 왼쪽에 있는 파란색「새로 만들기」버튼을 누릅니다.
- 하단의 「더 보기」를 누르면 펼침메뉴가 추가로 나옵니다.
- 하단의 「연결할 앱 더 보기」를 눌러 대화 상자를 엽니다.
- 
- 검색어로「script」를 입력하고 목록에 나온「Google Apps Script」의「＋연결」버튼을 누릅니다.

![drive0](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/drive0.png)


- 다시「새로 만들기」버튼을 눌러서「Google Apps Script」를 선택합니다.
// 사라짐 - 「스크립트」아래에 있는「제목 없는 프로젝트」를 선택합니다.
- 새로운 스크립트를 만드는 화면으로 전환하므로, 왼쪽의「제목 없는 프로젝트」를 클릭해서, 「Miyamoto-san」으로 변경합니다.

![gas03](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/gas03.png)


- [main.gs](https://raw.githubusercontent.com/hyunmin-mz/miyamoto/master/main.gs)를 복사하여 브라우저에서 편집기 부분에 붙여 넣습니다.
- 메뉴에서「파일」→「저장」을 선택하여 저장합니다.
- 메뉴에서「파일」→「프로젝트 속성」을 열고「Time zone」을「서울」에 맞추십시오.


### 초기화

- 툴바의「함수를 선택」에서「setUp」을 선택하고, 왼쪽의 재생 버튼을 누릅니다.

![gas11](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/gas11.png)

- 권한 승인 화면이 나오면「승인」을 누르십시오.
- Google Drive에「Slack Timesheets」라는 Spreadsheet가 생성됩니다.


### API를 게시

- 메뉴에서「게시」→「웹 앱으로 배포...」를 선택합니다.
- 먼저「새로 만들기」버튼을 누른후,「웹에 액세스할 수 있는 사용자」에서「누구나（익명 사용자 포함）」을 선택합니다.
- 동시에「앱을 실행할 사용자」를「나」로 선택합니다.
- 등록 완료 후에 나오는「현재 웹 앱 URL」을 어딘가에 메모해두십시오.

![gas20](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/gas20.png)


- 「누구나（익명 사용자 포함）」이 없으면, https://admin.google.com/ 에서「Google Apps」→「드라이브」를 선택하고,「공유설정」의「사용자는 조직 외부 사용자와 파일을 공유 할 수 있다」를 선택합니다.

![admin2](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/admin2.png)



## Slack의 설정

- Slack의 웹사이트에 로그인 한 다음「timesheets」채널을 추가합니다.

### Slack Outgoing 설정

- 왼쪽 메뉴에서「Apps & integration」을 선택합니다.

![slack11](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/slack11.png)

- 검색어로「outgoing」을 검색하고, 목록에서「Outgoing WebHooks」을 선택합니다.
- 좌측에 위치한 녹색의「Add Configuration」을 누릅니다.
- 녹색의「Add Outgoing Webhooks integration」을 누릅니다.
- 「Integration Settings」의「Channel」에서「#timesheets」을 선택하고,「URL(s)」에는「API의 게시」에서 메모한「현재 웹 앱 URL」을 입력하고,「Save Settings」를 누릅니다.

![slack13](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/slack13.png)


### Slack Incoming 설정

- 왼쪽 메뉴에서「Apps & integration」을 선택합니다. 
- 검색어로「incoming」을 검색하고, 목록에서「Incoming WebHooks」을 선택합니다.
- 좌측에 위치한 녹색의「Add Configuration」을 누릅니다.
- 페이지 하단의「Choose a channel...」에서「#timesheets」를 선택하고,「Add Incoming WebHooks integration」를 선택합니다.
- 전환 페이지의「Webhook URL」에 적혀있는 URL을 어딘가에 메모해둡니다.

![slack21](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/slack21.png)

- 「Integration Settings」에서「Customize Name」의 입력칸에서「miyamoto」를 지정합니다.

![slack22](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/slack22.png)

- 「miyamoto」이외의 이름을 지정하는 경우, Spreadsheet의「_설정」시트에서「무시되는 사용자」에 이름을 추가하십시오.

## 미야모토상(みやもとさん)의 설정

- https://drive.google.com/ 에서「Slack Timesheets」를 선택합니다.
- 메뉴의「파일」→「스프레드 시트 설정」을 열고「시간대」를「서울」로 맞춰주세요.
- 아래의 탭에서「_설정」을 열고、「Slack Incoming URL」의「B1」칸에「Slack Incoming 설정」에서 메모한「Webhook URL」을 입력합니다.
- 이 bot의 이름을 변경한 경우에는,「무시되는 사용자」에 이름을 추가하십시오.

![gs3](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/gs3.png)


# 동작

Slack의 #timesheets 채널에「좋은 아침」이라고 말하면, 앞의「Slack Timesheets」에 사용자 이름의 탭이 만들어지고, 시간이 기록됩니다.

오늘 날자가 두개 컬럼에 설정되있지만, B〜C열을 시간 표시로 전환해야 합니다. 범위 지정을 해서 메뉴의 「서식」→「숫자」→「시간」을 선택하십시오.

주간 휴일은「Day Off」란에 쉼표(,) 로 구분해서 입력합니다.

![gs2](https://raw.githubusercontent.com/masuidrive/miyamoto/master/docs/images/gs2.png)

이제 설치가 끝났습니다. 어떤 메시지에 반응하는지는 [timesheets.js](https://github.com/masuidrive/miyamoto/blob/master/scripts/timesheets.js#L29)의 정규표현식을 확인해주십시오.

또한, 이 시트를 편집 불가로 공유하면, 업무 시간 확인등을 쉽게 할 수 있습니다.

## 협력해주십시오

미야모토상(みやもとさん)을 사용하고 있는 분은, 꼭 [미야모토상 설문조사](https://docs.google.com/forms/d/1Rnis14t2OImkwvfOc2L0B3GmvByxu6jVRoAcxJLY1tc/viewform?usp=send_form)에 협력해주십시오.

개발의 참고로 하겠습니다.


## 메시지의 변경

Spreadsheet의「_메시지」시트에 각 메시지의 템플릿이 적혀있습니다. 세로로 다양한 메시지를 적어두면, 랜덤으로 선택됩니다.

여기를 변경하면 미야모토상(みやもとさん)의 캐릭터가 바뀝니다. 꼭 재미있는 설정을 하십시오.


## 사양

- 사용자의 이름에 .(점) 이 있는 경우, mention이 되지 않는 것은 Slack Webhook의 사양입니다.
- Private Group에는 설치할 수 없습니다
- 사용자는 하나의 방에 90명정도까지입니다. 그 이상의 사용자인 경우 부서 단위 등으로 방을 나누어주세요.

# 개발

- 코드를 변경 한 경우에는, 「게시」→「웹 앱으로 배포...」에서 「프로젝트 버전」을 「새로 만들기」로 선택한 후 업데이트 버튼을 눌러주십시오.


## Todo

- 출근일수관리
- 시간 외 노동의 관리
- 휴식 시간


## 테스트 실행

미야모토상(みやもとさん)은 로직의 검증을 Node를 사용하여 수행할 수 있습니다. Node의 실행 환경을 설정한뒤 다음 명령을 실행하십시오.

```
npm install
make test
```

## 소스코드

- main.js
 - HTTP를 받는다

- 입력 내용을 분석하여 메소드를 호출
 - Slack에 입출력

- gs_template.js
 - Google Spreadsheet를 이용한 메시지 템플릿

- gs_properties.js
 - Google Spreadsheet를 이용한 설정 key-value store

- gs_timesheets.js
 - timesheets를 Google Spreadsheet에 저장하는 처리

- gas_properties.js
 - Google Apps Script를 이용한 설정 key-value store

- gas_utils.js
 - Google Apps Script용 유틸리티

- utils.js
 - global로 사용하는 유틸리티

- date_utils.js
 - 날짜 관련 유틸리티

- underscore.js
 - _.로 시작하는 유틸리티 모음
 - http://underscorejs.org


# License

- [MIT License](http://opensource.org/licenses/MIT)
- Copyright 2014- Yuichiro MASUI <masui@masuidrive.jp>
- https://github.com/masuidrive/miyamoto
