오늘은 관리자 테이블을 생성하겠습니다.<br>
문제에서 주어진 정보는 아래의 사진과 같습니다.

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day2/img.png)
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day2/img_1.png)
![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day2/img_2.png)

구조상 데이터베이스가 존재하고 그 안에 테이블이 존재하기 때문에 우선 테이블을 먼저 만들고 그 후 데이터베이스를 각각 만들어 주겠습니다.<br>
우선 첫번째로 데이터베이스를 생성하는 Mysql구문을 String 변수로 설정해줍니다.<br>

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day2/img_3.png)
그 후 위에 표에 존재하는 테이블을 만들기 위해 테이블을 생성하는 Mysql구문을 String 변수로 설정해줍니다.<br>

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day2/img_4.png)
위에서 변수로 지정한 Mysql구문을 사용하기 위해 Statement 인터페이스를 이용하여 객체를 우선 null로 잡아줍니다.<br>
또한 Day1에서 작성한  Driver_connect.makeConnection을 이용하여 사용중인 컴퓨터의 Mysql주소 로 접속을 합니다.<br>

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day2/img_5.png)

데이터베이스에 대한 Sql문을 실행하기 위해 'Connection'의 객체인 'con'을 통해 'Statement' 객체를 생성합니다.<br>
그 후 st.executeUpdate()구문을 이용하여 'st'를 통해 ()안에 들어가 있는 Sql구문을 실행시킵니다. 여기서try-catch구문을 이용하여 sql문의 구문오류에 대한 예외처리를 시켜줍니다!


🔥 **여기서 잠깐!!** 🔥<br>
excuteUpdate()와 excute() 2가지 구문이 있는데 어떨때 어떤 구문을 사용해야 할까 궁금중이 생길 수도 있습니다.<br>
excuteUpdate()는 주로 INSERT, UPDATE, DELETE와 같은 데이터를 변경하는 Sql문을 실행할 때 사용이 됩니다. 이 메소드는 반환되는 결과는 필요하지 않고 단순히 데이터 베이스의 상태를 변경할때 주로 사용이 됩니다.<br>
excute()는 주로 SELECT와 같이 결과를 반환하는 Sql문을 실행할때 사용이 됩니다. 반환 값은 'boolean' 형식이며 반환값이 'true'이면 ResultSet객체를 반환한다는 의미이며 'false'이면 ResultSet 객체를 반환하지 않는다는 뜻입니다.

![실행 결과](https://github.com/junhyeok1667/JDBC-PROJECT-insurance-/blob/main/Day2/img_6.png)

```java
package customer_db;

import java.sql.Connection;
import java.sql.SQLException;
import java.sql.Statement;

public class create_customer {

	public static void main(String[] args) {
		String createdb = "create database if not exists customer";
		
		String createadmin = "create table if not exists admin(name varchar(20) not null,"
				+ "passwd varchar(20) not null, position varchar(20), "
				+ "jumin char(14), inputDate date, primary Key(name, passwd));";
		
		String createcustomer = "create table if not exists customer(code char(7) not null,"
				+ "name varchar(20) not null, birth date, tel varchar(20),"
				+ "address varchar(100), company varchar(20), primary Key(code, name));";
		
		String createcontract = "create table if not exists contract(customerCode char(7) not null,"
				+ "contractName varchar(20) not null, regPrice integer,"
				+ "regData date not null, monthPrice int, adminName varchar(20) not null);";
		
		Statement st = null;
		Connection con = Driver_connect.makeConnection("");
		
		
		try {
			st = con.createStatement();
			st.executeUpdate(createdb);
			st.executeUpdate("use customer");
			st.executeUpdate(createadmin);
			st.executeUpdate(createcustomer);
			st.executeUpdate(createcontract);
			System.out.println("만들기 성공");
		} catch (SQLException e) {
			System.out.println("SQL 오류!!");
		}

	}

}

