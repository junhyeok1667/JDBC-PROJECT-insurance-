오늘은 [그림 2-5] 보험계약 관리 화면 창에서 [고객 조회] 버튼을 클릭하면 아래 사진과 같이 “고객 조회” 창이 열리도록 만들고  "조회", "전체보기", "수정", "삭제", "닫기" 버튼들에 대해 Action을 만들어주도록 하겠습니다.<br>

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day8/img.png)


<br>
우선 아래의 사진과 같이 2부분으로 나누어 상단 부분인 Top패널 먼저 만들어보도록 하겠습니다.

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day8/img_1.png)
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day8/img_2.png)

이제는 하단부분에 보이는 JPanel을 만들어줘야합니다. JPanel을 만들기 위해서는 JTable에 대해 알고 있어야 합니다. JTable에 관한 내용은 아래에 포스팅 해놓겠습니다.<br>

[블로그 바로가기](https://chillysugar-study.tistory.com/4)
<br>
JTable은 클래스의 생성자안에 JTable을 생성해주도록 하겠습니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day8/img_3.png)
이렇게 코드를 작성 후 실행을 시켜주면 아래와 같이 GUI가 생성된는 것을 볼 수 있습니다.<br>

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day8/img_4.png)

감사합니다.
