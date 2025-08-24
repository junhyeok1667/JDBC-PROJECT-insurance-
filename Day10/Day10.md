오늘은 보험계약 관리화면의 [계약 관리] 버튼을 클릭하면 아래와 같이 “보험 계약” 창이 열리도록 하는 Gui를 생성하도록 하겠습니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day10/img.png)

우선 그림의 Gui를 3등분하여 만들어보겠습니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day10/img_1.png)
<br>

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day10/img_2.png)
<br>

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day10/img_3.png)
<br>

우선 표의 왼쪽의 부분 Panel 구현하겠습니다. <br>
GridLayout(4,2)를 이용하여 총 8개의 칸을 확보하여 준 후 "고객코드"가 들어갈 JLabel,  "고객코드"를 입력받을 JTextField, "보험상품"이 들어갈 JLabel, 보험의 종류에 대해 선택할수 있는 JComboBox, 고객명"이 들어갈 JLabel, 데이터베이스에 존재하는 고객명을 선택할수 있는 JComboBox 나머지 부분은 JLabel과 JTextField를 순서대로 넣어주면 됩니다.<br>
여기서 고객명을 선택할 수 있는 JComboBox를 위해 Mysql의 "cutomer"데이터베이스와 연동을 하고 " select name from customer"구문을 이용하여 구문의 결과값을 Vector에 저장을 하여 Vector를 ComboBox에 추가를 했습니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day10/img_4.png)
<br>
이렇게 코드를 입력하고 실행을 시켜주면 아래와 같은 결과값이 나오게 됩니다.
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day10/img_5.png)
<br>
이제 중간 부분 Panel을 만들겠습니다.<br>
중간부분은 아까 만든 Panel과 비슷하지만 "담당자"에 대한 JLabel, 데이터베이스(admin테이블)에 존재하는 데이터들을 선택할 수 있는 JComboBox, 나머지는 JButton으로 만들어주면 됩니다.<br><br>
여기서 담당자명을 선택할 수 있는 JComboBox를 위해 Mysql의 "cutomer"데이터베이스와 연동을 하고 " select name from admin"구문을 이용하여 구문의 결과값을 Vector에 저장을 하여 Vector를 ComboBox에 추가를 했습니다.<br>
<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day10/img_6.png)

이렇게 코드를 입력하고 실행을 시켜주면 아래와 같은 Gui가 생성됩니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day10/img_7.png)
<br>
마지막 Panel은 "customerCode", "customerName", "regPrice", "regData", "monthPrice","adminName" 행을 가진 JTable 을 만들어줍니다.<br>
JTable에 대한 내용은 다시 한번 아래에 포스팅 하겠습니다.<br>
[블로그 바로가기](https://chillysugar-study.tistory.com/4)

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day10/img_8.png)

이렇게 코드를 작성하고 코드를 실행시키면 최종적인 Gui가 생성되게 됩니다!!<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day10/img_9.png)

```java
package customer_ui;

import java.awt.BorderLayout;
import java.awt.Container;
import java.awt.FileDialog;
import java.awt.FlowLayout;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.FileWriter;
import java.io.IOException;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Calendar;
import java.util.Vector;

import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.JTextField;
import javax.swing.table.DefaultTableModel;

import customer_db.Driver_connect;
import customer_ui.Customer_Inquiry.Top;

public class Contract_Management extends JFrame {
	JComboBox cb1;
	JTextField jt;
	JTextField JtMenu[];
	Vector rowData;
	Vector<String> data = new Vector<String>();
	JTable table;
	JComboBox cb;
	JComboBox cb2;
	String[] s = new String[6];

	public Contract_Management() {
		setTitle("보험 계약");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		Container c = getContentPane();
		c.add(new Top(), BorderLayout.NORTH);
		c.add(new Center(), BorderLayout.CENTER);
		c.add(new Bottom(), BorderLayout.SOUTH);

		setSize(700, 700);
		setVisible(true);

	}

	class Top extends JPanel {
		public Top() {
			setLayout(new GridLayout(4, 2));
			JLabel code = new JLabel("고객코드: ");
			add(code);
			jt = new JTextField(15);
			add(jt);

			String insurance[] = { "무배당암보험", "변액연금보험", "여성건강보험", "연금보험", "의료실비보험", "종신보험" };
			JLabel insuranceProduct = new JLabel("보험상품: ");
			add(insuranceProduct);
			JComboBox cb = new JComboBox(insurance);
			add(cb);
			
			JLabel customerName = new JLabel("고객명: ");
			add(customerName);

			String customerSql = "select name from customer";
			try {
				Connection conn = Driver_connect.makeConnection("customer");
				Statement stmt = conn.createStatement();
				ResultSet rs = stmt.executeQuery(customerSql);

				Vector<String> v1 = new Vector<String>();
				while (rs.next()) {
					String name = rs.getString("name");
					v1.add(name);
				}
				// Vector에 저장된 정보를 ComboBox에 삽입
				cb1 = new JComboBox(v1);
				add(cb1);
				
				String Menu[] = { "가입금액", "생년월일", "월보험료", "연락처" };
				JtMenu = new JTextField[Menu.length];
				JLabel MenuLa[] = new JLabel[Menu.length];
				for (int i = 0; i < Menu.length; i++) {
					MenuLa[i] = new JLabel(Menu[i]);
					add(MenuLa[i]);
					JtMenu[i] = new JTextField(15);
					add(JtMenu[i]);

				}

			} catch (SQLException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
	}

	

	class Center extends JPanel {
		public Center() {
			JLabel la3 = new JLabel("담당자: ");
			add(la3);

			String adminSql = "select name from admin";
			// mysql admin에 있는 관리자 명단 Vector에 저장
			try {

				Connection conn = Driver_connect.makeConnection("customer");
				Statement stmt = conn.createStatement();
				ResultSet rs = stmt.executeQuery(adminSql);

				Vector<String> v2 = new Vector<String>();
				while (rs.next()) {
					String name = rs.getString("name");
					v2.add(name);
				}
				// Vector에 저장된 정보를 ComboBox에 삽입
				cb2 = new JComboBox(v2);
				add(cb2);

			} catch (SQLException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			// 가입,삭제,파일로 저장, 닫기 버튼 생성
			String ButtonMenu[] = { "가입", "삭제", "파일로 저장", "닫기" };
			JButton btn[] = new JButton[ButtonMenu.length];
			for (int t = 0; t < ButtonMenu.length; t++) {
				btn[t] = new JButton(ButtonMenu[t]);
				add(btn[t]);
			}

		}
		
		}


	class Bottom extends JPanel {
		public Bottom() {
			setLayout(new BorderLayout());
			JLabel centerLabel = new JLabel("<고객 보험 계약현황>");
			// BorderLayout으로 설정했기에 라벨을 중앙으로 정렬하기 위해 JPanel을 생성
			JPanel labelPanel = new JPanel(new FlowLayout(FlowLayout.CENTER));
			labelPanel.add(centerLabel);
			add(labelPanel, BorderLayout.NORTH);

			String JTable_Name[] = { "customerCode", "customerName", "regPrice", "regData", "monthPrice", "adminName" };

			rowData = new Vector<String>();
			Vector<String> colData = new Vector<String>();

			// JTable_Name의 길이만큼 행추가
			for (int i = 0; i < JTable_Name.length; i++) {
				colData.add(JTable_Name[i]);

			}
			table = new JTable(rowData, colData);
			JScrollPane jps = new JScrollPane(table);

			add(jps, BorderLayout.CENTER);

		}
	}

			public static void main(String[] args) {
			new Contract_Management();
	
	   }   
}

