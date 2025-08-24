오늘은 파일을 읽고 파일 내용을 관리자 테이블에 삽입해보도록 하겠습니다.<br>

저번 Day2에서 관리자 테이블은 생성했지만 테이블 안에 데이터들이 존재하지는 않습니다.<br>
이번에는 관리자 테이블 안에 데이터를 넣는 작업을 해보겠습니다!<br>

우선 customer데이터베이스를 선택해야 하기에 customer데이터베이스로 이동해줍니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day3/img.png)


Eclipse안에서 SQL문을 실행시켜야 하기 때문에 Day2에서 사용한 바와 같이 Statement st = null을 잡아 주는게 맞겠죠?<br>
하지만 저는 Statement인터페이스를 사용하지 않고 이번에는 PreparedStatement 인터페이스를 사용할 것입니다.<br>
그러면 갑자기 왜?? 라는 의문이 생길겁니다. 의문이 생기시면 밑에 제가 작성한 블로그인데 한번 들어가서 읽어보시면 좋을거 같습니다!<br>
[블로그 바로가기](https://chillysugar-study.tistory.com/1)


제가 Day2에서 관리자테이블을 3개를 만들었고 3개의 테이블에 데이터를 삽입해야 하므로 PreparedStatement를 사용하겠습니다.<br>
또한 제가 사용해야 할 SQL구문과 파일을 읽어 파일에 들어있는 데이터를 관리자데이터에 삽입해야하므로 읽어야 할 파일의 이름을 배열에 저장합니다.<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day3/img_1.png)


for문을 이용하여 배열 sql의 길이만큼 반복을 하여 제가 읽어야 할 파일을 읽고 파일을 \t단위로 나눈 후 나누어진 String을 관리자 데이터에 삽입하면 완성이됩니다.<br>
코드를 전체적으로 보여드리면 
```java
package customer_db;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Scanner;
import java.util.StringTokenizer;

public class insert_customer {

	public static void main(String[] args) {
		
		PreparedStatement psmt = null;
		Connection con = Driver_connect.makeConnection("customer");
		
		
		//읽어와야 할 파일의 폴더 이름을 fileName배열에 삽입
		String []fileName = {"admin", "customer", "contract"};
		//데이터 삽입을 위해 필요한 sql구문을 sql배열에 삽입
		String []sql = {"insert into admin values(?,?,?,?,?)","insert into customer values(?,?,?,?,?,?)",
				"insert into contract values(?,?,?,?,?,?)"};
		
		for(int i = 0; i<sql.length; i++) {
			try {
				psmt = con.prepareStatement(sql[i]);
			} catch (SQLException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			try {
				//파일을 읽기 위해 try-catch구문을 이용
				Scanner fscanner = new Scanner(new FileReader("DataFiles/"+fileName[i]+".txt"));
				String f = fscanner.nextLine();
				//파일을 한줄씩 읽고 읽은 줄을 \t단위로 쪼개기
				StringTokenizer ta = new StringTokenizer(f,"\t");
				int n = ta.countTokens();
				String k[] = new String[n];
				
				while(fscanner.hasNext()) {
					f = fscanner.nextLine();
					ta = new StringTokenizer(f,"\t");
					int j = 0;
					while(ta.hasMoreTokens()) {
						k[j]= ta.nextToken();
						try {
							//Query안에 들어갈 매개변수 설정
							psmt.setString(j+1, k[j]);
							j++;
						} catch (SQLException e) { e.printStackTrace();}
					}
					try {
						psmt.executeUpdate();
					} catch (SQLException e) {e.printStackTrace();}
				}
			} catch (FileNotFoundException e) { e.printStackTrace();}
			finally {
		        //PreparedStatement 닫기
		        if (psmt != null) {
		            try {
		                psmt.close();
		            } catch (SQLException e) {
		                e.printStackTrace();
		            }
		        }

			System.out.println("");
		}
		
	}

	}
}
```
코드를 실행 시킨 이후Mysql에 들어가서 관리자 테이블을 보면 이렇게 데이터가 들어간 것을 볼 수 있습니다<br>
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day3/img_2.png)
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day3/img_3.png)
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day3/img_4.png)
 
