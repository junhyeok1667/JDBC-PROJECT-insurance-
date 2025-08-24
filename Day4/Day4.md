오늘은 Day3까지 MySQL과 Eclipse의 연동, 관리자데이터베이스 생성 및 정보추가를 완료했으니 이제 Gui를 만들어보겠습니다!<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day4/img.png)

조건 1. 로그인 창에서 비밀번호 입력은 패스워드 형식으로 입력 내용이 숨겨지도록 하시오.<br>
조건 2. 로그인 창에서 이름과 비밀번호를 입력하고 [확인] 버튼을 누르면 이름과 비밀번호가 일치하는 관리작 있을 경우 보험계약관리화면으로 이동하고 로그인창은 닫히도록 하시오.<br>
조건 3. [종료] 버튼을 누르면 이 닫히고 프로그램이 종료되도록 하시오.<br>

위의 조건은 나중에 추가하도록 하고 먼저 Gui 틀을 먼저 잡아보도록 하겠습니다.<br>
제가 생각했을 때에 가장 좋은 방법은 아래의 그림과 같이 3 부분 Jpanel으로 나누어 Container에 올리는 것입니다.<br>

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day4/img_1.png)
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day4/img_2.png)
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day4/img_3.png)

첫번째 사진(Top panel)을 먼저 만들어보도록 하겠습니다.<br>
"관리자 로그인"을 JLabel으로 만들고 글꼴을 바꾸도록 하겠습니다.<br>
글꼴 바꾸는 방법에 대해서는 아래에 포스팅한 내용을 첨부하도록 하겠습니다.<br>
[블로그 바로가기](https://chillysugar-study.tistory.com/2)<br>
<br>

아래 코드는 첫번째 사진(Top panel)에 대한 코드입니다. 
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day4/img_4.png)

<br>
이제 두번째 사진(Center panel)에 대해 만들어보도록 하겠습니다.
Center panel에는 "이름", "비밀번호"에 대한 JLabel이 필요하고 각 JLabel에 대해 입력받을 수 있는 JTextField가 필요합니다. 하지만 문제에서 주어진 조건을 봤을 때 비밀번호에 대해서는 보이지 않게 하라 했기에 비밀번호를 입력하는 부분을 JTextField가 아닌 JPassword를 사용해 줍니다.<br>

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day4/img_5.png)


마지막으로 세번째 사진(Bottom panel)에 대해 만들어보겠습니다.
Bottom panel에는 "확인", "종료" 에 대한 JButton이 2개 존재합니다.<br>
따라서 JButton을 추가하는 코드만 추가하겠습니다/
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day4/img_6.png)

이제 마지막으로 Top panel, Center panel, Bottom panel을 Container에 올리는 코드를 작성하겠습니다. panel에 대해서는 BorderLayout을 이용하여 North, Center, South 방향에 배치하도록 하겠습니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day4/img_7.png)

이렇게 실행을 한다면!!!!<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day4/img_8.png)
<br>
이렇게 결과가 나옵니다!!!!<br>

이렇게 이번에는 화면 틀만 만드는 작업을 했는데 다음에는 이 Gui에 이어 버튼들에 ActionListener을 달고 Mysql과 연도시켜 로그인이 되도록 해보겠습니다!<br>

```java
package customer_ui;


import java.awt.BorderLayout;
import java.awt.Container;
import java.awt.Font;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JPasswordField;
import javax.swing.JTextField;

public class Login extends JFrame{

	JTextField jt;
	JPasswordField jp;
	
	public Login() {
		setTitle("로그인");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		Container c = getContentPane();
		c.setLayout(new BorderLayout());
		
		c.add(new Top(),BorderLayout.NORTH);
		c.add(new Center(),BorderLayout.CENTER);
		c.add(new Bottom(),BorderLayout.SOUTH);
		
		setSize(300,200);
		setVisible(true);
		
	}
	
	class Top extends JPanel{
		public Top() {
			JLabel la1 = new JLabel("관리자 로그인");
			la1.setFont(new Font("고딕체",Font.BOLD,20));
			add(la1);
		}
	}
	
	class Center extends JPanel{
		public Center() {
			String labelName[] = {"이름       ","비밀번호"};
			JLabel la2[] = new JLabel[labelName.length];
			jt = new JTextField(18);
			jp = new JPasswordField(18);
			
			la2[0] = new JLabel(labelName[0]);
			add(la2[0]);
			add(jt);
			la2[1] = new JLabel(labelName[1]);
			add(la2[1]);
			add(jp);
				
			
		}
	}
	
	class Bottom extends JPanel{
		
		public Bottom() {	
			String buttonName[] = {"확인","종료"};
			JButton btn[] = new JButton[buttonName.length];
			
			for(int i = 0; i<btn.length; i++){
				btn[i] = new JButton(buttonName[i]);
				add(btn[i]);
			}
		}
	}

	public static void main(String[] args) {
		new Login();
	}

}


 
