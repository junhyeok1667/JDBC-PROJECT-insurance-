오늘은 Day5에 이어 로그인이 성공하면 나타나는 창에 대해 만들어보도록 하겠습니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day6/img.png)

우선 상단의 버튼들을 배치할 Top Panel과 하단에 사진을 배치할 Bottom Panel 총 2가지 Panel을 Conatiner에 올려야 하는 것을 생각할 수 있습니다.<br>
Top Panel에 대한 코드입니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day6/img_1.png)
<br>
위와 같은 코드를 작성하고 실행을 시켜주면 아래와 같이 사진은 없고 버튼들은 존재하는 창이 생성되는 것을 확인할 수 있습니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day6/img_2.png)
이제 사진을 넣는 Bottom Panel을 생성하겠습니다.<br>
저는 JLabel을 이용하여 사진을 출력하겠습니다. JLabel에 대하여 모르시는 분이 있다면 아래의 JLabel에 대한 포스팅을 참고 부탁드립니다!!<br>
[블로그 바로가기](https://chillysugar-study.tistory.com/3)
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day6/img_3.png)
<br>
이렇게 두 Panel을 Container에 올려 실행을 하면 아래와 같은 화면이 출력됩니다!<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day6/img_4.png)
<br>
이제 화면을 설계했으니 로그인이 성공했을경우 지금 설계한 화면이 나타나도록 하겠습니다.<br>
이전 Day5에서 만든 코드(Login)를 보면 로그인을 성공하면  "일치하는 관리자가 있습니다." 라는 문구가 나오도록 하는 코드가 존재합니다. 하지만 그 코드를 지우고 아까 설계한 화면의 생성자를 추가해주도록 하겠습니다.<br>

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day6/img_5.png)
이제 다시 Login코드를 실행하겠습니다!<br>


 
