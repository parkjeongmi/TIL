# Oracle-DB 연동

1. DB 연결

```java
dbConnection();
```

```java
//복붙
public class MovieTest{
  Connection conn;
  PreparedStatement pstmt;
  
  public void dbConnection() {
      FileInputStream fis = null;
      try {
        fis = new FileInputStream("db.properties");
        Properties dbprop = new Properties();
        dbprop.load(fis);
        String driver = dbprop.getProperty("driver");
        String url = dbprop.getProperty("url");
        String user = dbprop.getProperty("user");
        String password = dbprop.getProperty("password");
        Class.forName(driver); //드라이버 설정
        conn = DriverManager.getConnection(url, user, password); //url, user,password 지정하여 connection 가져오기
      } catch(IOException e) {
        e.printStackTrace();
      }  catch(SQLException e) {
        e.printStackTrace();
      } catch(ClassNotFoundException e) {
        e.printStackTrace();
      } finally {
        try {
          if(fis!=null) fis.close();
        } catch(Exception e) {
          e.printStackTrace();
        }
      }
    }
}
```

2.  Sql 쓸 컬럼 선택 ex) insert into movie values(1,'인터스텔라', 'sf', '21/03/24','홍길동');

```java
String sql = "insesrt into movie values (?,?,?,?,?)";
```

3. statement 가져오기

```java
//conn 객체에는 prepareStatement 메소드가 있는데, 이 메소드에 sql을 전달해준다.
//그 값을 pstmt 변수에 넣어준다 -> pstmt는 sql를 담은 상자
pstmt = conn.prepareStatement(sql);

//DTO 만든 후에!
try{
  pstmt.setInt(1,movie.getMovie());
  pstmt.setString(2,movie.getTitle());
  pstmt.setString(3,movie.getGenre());
  pstmt.setDate(4,movie.getmdate());
  pstmt.setString(5,movie.getDirector());
} catch(SQLException e){
  e.printStackTrace();
} finally {
  try{
    if(pstmt!=null){
      pstmt.close();
      pstmt=null;
    }
  } catch(SQLException e){
    e.printStackTrace();
  }
}
connClose();
}
```

3. Query에 필요한 값들 설정하기

```java

```

5. Query 실행 (업데이트)

```java
int cnt = pstmt.executeUpdate();
```



6. 예외처리



7. 



```java
public static void main(String[] args){
  MovieTest m = new MovieTest();
  MovieDTO m = new MovieDTO(2,"영화제목","장르","2021/03/24","박길동");
  m1.insert(m);
}
```



----

1. DTO

```java
mov
```





---

# 코드 정리

#### public void dbConnection()

```java
	public void dbConnection() {
		FileInputStream fis = null;
		try {
			fis = new FileInputStream("db.properties");
			Properties dbprop = new Properties();
			dbprop.load(fis);
			String driver = dbprop.getProperty("driver");
			String url = dbprop.getProperty("url");
			String user = dbprop.getProperty("user");
			String password = dbprop.getProperty("password");
			Class.forName(driver); //드라이버 설정
			conn = DriverManager.getConnection(url, user, password); //url, user,password 지정하여 connection 가져오기
		} catch(IOException e) {
			e.printStackTrace();
		}  catch(SQLException e) {
			e.printStackTrace();
		} catch(ClassNotFoundException e) {
			e.printStackTrace();
		} finally {
			try {
				if(fis!=null) fis.close();
			} catch(Exception e) {
				e.printStackTrace();
			}
		}
	}
```

#### public void connClose()

```java
	public void connClose() {
		try {
			if(conn!=null) {
				conn.close();
				conn=null;
			}
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}
```

#### public void insertEmp(EmpDTO emp)

```java
	public void insertEmp(EmpDTO emp) {
		dbConnection();
		String sql = "insert into emp values(?,?,?,?,?,?,?,?)";
		try {
			pstmt = conn.prepareStatement(sql);
			pstmt.setInt(1, emp.getEmpno());
			pstmt.setString(2, emp.getEname());
			pstmt.setString(3, emp.getJob());
			pstmt.setInt(4, emp.getMgr());
			pstmt.setString(5, emp.getHiredate());
			pstmt.setDouble(6, emp.getSal());
			pstmt.setDouble(7, emp.getComm());
			pstmt.setInt(8, emp.getDeptno());
			int cnt = pstmt.executeUpdate();
		} catch(SQLException e) {
			e.printStackTrace();
		} finally {
			try {
				if(pstmt!=null) {
					pstmt.close();
					pstmt=null;
				}
			} catch(SQLException e) {
				e.printStackTrace();
			}
		}
		connClose();
	}
```

#### public static void main(String[] args)

```java
	
	public static void main(String[] args) {
		EmpTest empDao = new EmpTest();
//		empDao.removeEmp(9997);
		
//		empDao.changeEmpJob(9997, "홍보");
		empDao.printAllEmp();
//		EmpDTO emp1 = new EmpDTO(9997,"홍길동","SALESMAN",7698,"2015/07/02",2700,0,30);
//		empDao.insertEmp(emp1);
//		EmpDTO emp = empDao.queryEmp(9999);
//		System.out.println(emp);
	}
```

