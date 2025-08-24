Day4에서 만들었던 Gui의 틀에 이어서 Jbutton들에 ActionListener를 걸고 MySQL과 연동하여 MySQL의 admin테이블에 존재하는 정보들로 로그인이 되도록 해보겠습니다.<br>
우선 앞에서 했듯이 MySQL의 customer 데이터베이스에 접속하겠습니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day5/img.png)

이렇게 추가하고 실행을 해준다면 아래와 같이 Eclipse와 Mysql의 customer데이터베이스에 연결이 됬다는걸 확인 할 수 있습니다.!!<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day5/img_1.png)

이제 Bottom 클래스에 존재하는 Jbutton들에 대하여 ActionListener를 걸어주도록 하겠습니다.<br>
이렇게 각 버튼들에 대하여 addActionListener(추가할 클래스명)을 해주면 추가할 클래스 안에 존재하는 코드들이 버튼을 누를때마다 실행이 됩니다.<br>
하지만 지금 빨간줄이 뜨는 이유는 아직 추가할 클래스를 정의해 주지 않았기 때문입니다!<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day5/img_2.png)
<br>

이제 Action이라는 클래스를 정의해 주도록 하겠습니다.<br>
Action클래스는 Jbutton인 "확인","종료" 버튼을 눌렀을때 Mysql의 "admin" 관리자테이블로 접속해 name과 passwd의 정보와 자신이 입력한 이름과 비밀번호를 비교해 존재하면 로그인이 되는 클래스입니다. 또한 로그인을 성공했을때 Joptionpane, 실패했을때 Joptionpane을 만들어줍니다. <br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day5/img_3.png)

실행했을때 Mysql의 admin 테이블에 존재하는 이름과 일치하는 비밀번호이면 로그인이 되는것을 볼수 있습니다.


