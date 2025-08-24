오늘은 Day6에 만든 GUI에서 한번 더 나아가 고객등록 버튼을 눌렀을때 조건에 맞추어 GUI가 나타나도록 만들어보겠습니다.<br>
만들어야 하는 GUI의 조건에 대하여 말씀드리겠습니다.<br>
● 보험계약 관리 화면 창에서 [고객 등록] 버튼을 클릭하면 [그림 2-6]과 같이 “고객 등록” 창이 열리도록 하시오.
● [그림 2-6]의 고객등록 창에 “고객코드”는 입력할 수 없도록 하시오.
● “생년월일”을 입력하고 엔터를 누를 경우 [그림 2-7]와 같이 고객코드를 생성하여 화면에 나타나도록 하시오. 고객코드는 “S”와 현재 년도 2자리와 생년월일의 합계를 조합한 형식이다.
예) 현재년도가 ‘2015’년이고 생년월일이 ‘1982-11-13’일 경우 고객코드는 ‘S’, ‘15’, (1982+11+13)를 조합한 ‘S152006’이 된다.
● 만약 필수항목(*)을 입력하지 않았을 경우 [그림 2-8]과 같이 메시지를 출력하고 저장되지 않도록 하시오.
● “고객명”, “생년월일”, “연락처”, “주소”, “회사” 항목을 입력하고 [추가] 버튼을 클릭하면 DB에 저장되도록 하시오. 만약 정상적으로 저장이 되면 [그림 2-9]와 같이 성공메시지를 출력하시오.
● [그림 2-6] 고객등록 창에서 [닫기] 버튼을 클릭하면 “고객 등록” 창이 닫히도록 하시오.<br>
<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day7/img.png)


[그림 2-6]에 보시는 것처럼 GUI의 틀을 만들어보겠습니다.<br>
우선 상단에 가로 2줄, 세로 6줄의 공간이 나오도록 GridLayout을 이용하여 Panel을 하나 생성해줍니다. 1행 부분에는 JLabel을 통한 label이 들어갈 것이고 2행 부분에는 각 부분에 대해 JTextField객체가 들어갈 것입니다. 그리고 조건을 보면 고객코드 부분은 비활성화를 하라고 명시되어있기에 setEnabled(false)를 이용하여 비활성화하는 코드를 사용하겠습니다.<br>
<br>
하단에는 "추가", "닫기" 버튼을 만들 Panel2를 생성해줍니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day7/img_1.png)

이렇게 코드를 작성하고 실행을 시켜주면 아래와 같은 화면이 생성이 되는 것을 볼 수 있습니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day7/img_2.png)
<br>
이제는 생년월일(YYYY_MM_DD)을 입력하는 JTextField부분에 입력을 한 후 키보드의 'Enter'를 눌렀을 때 비활성화된 고객코드 부분이 자동으로 고객코드를 생성하여 화면에 나타나도록 만들겠습니다.<br>
키보드의 'Enter'을 눌렀을때 고객코드가 생성되어 화면에 나타나야 하므로 KeyAdapter를 상속받은 클래스를 하나 생성합니다. 키보드의 버튼중 'Enter'가 눌려진 순간 Calendar클래스를 이용하여 현재연도를 얻은 후 조건에 맞게 고객코드를 만드는 코드를 작성합니다.<br>
단 입력한 생년월일 코드가 YYYY-MM-DD 이 형식이 아니라면 다시 입력을 하도록 하기 위해 생년월일의 JTextField를 split 함수를 이용해 '-' 단위로 나눈 후 split함수로 나누어진 부분이 3개가 나오지 않는다면 다시 입력하도록 만들었습니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day7/img_3.png)
<br>
하단 Panel에 "추가", "닫기"에 대한 ActionListener를 생성해보겠습니다.<br>
만일 "추가"버튼을 눌렀을때 필수항목인(고객명, 생년월일, 연락처)가 한개라도 비어있으면 JOptionPane을 통해 다시 입력력하라는 메세지가 출력되도록 하고 필수항목을 다 채워넣고 "추가"를 누르면 Mysql의 customer 테이블에 입력한 정보가 저장이 되도록 하는 mathAdd()함수 실행되도록 합니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day7/img_4.png)
<br>
mathAdd() 함수는 Mysql의 customer 테이블에 접속을 하고 직접 작성한 JTextField의 정보를 기반으로 customer 테이블에 정보를 추가를 하는 함수입니다. 만일 customer테이블에 존재하는 고객이름과 JTextField를 통해 작성한 고객이름이 중복이 되면 다른 고객이름을 입력하라는 JOptionPanel을 통해 메세지를 출력하도록 합니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day7/img_5.png)
이제 Day1부터 현재까지 작성한 전체코드를 실행시켜보겠습니다.<br>


