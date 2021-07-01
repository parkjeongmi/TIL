# Oracle-DBMS 연동

Jdbc 드라이버를 통해 Oracle DBMS를 사용하는 java code

- Java 파일의 3 part
  - MovieDBMSMain.java : 전체 코드의 실행을 담당
  - MovieDAO.java : DB와 연관딘 변수와 쿼리 메소드
  - MovieDTO.java : 캡슐화를 통해 데이터의 입출력 매개
- 코드의 작성은 Movie DBMSMain.Java에서 출발

---

## 연동 순서

1. driver 설정

2. connection 가져오기

3. statement 얻어오기

4. select 실행하기(executeQuery)

5. 결과를 ResultSet에 받아서 Book객체 만들기

6. 목록에 있는 객체 출력하기



1. **Driver 설정, Connection 가져오기**

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

2.  **Sql 쓸 컬럼 선택** ex) insert into movie values(1,'인터스텔라', 'sf', '21/03/24','홍길동');

```java
String sql = "insesrt into movie values (?,?,?,?,?)";
```

3. **statement 가져오기**

```java
//conn 객체에는 prepareStatement 메소드가 있는데, 이 메소드에 sql을 전달해준다.
//그 값을 pstmt 변수에 넣어준다 -> pstmt는 sql를 담은 상자
pstmt = conn.prepareStatement(sql);
```

4. **Query에 필요한 값들 설정하기**

```java
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

5. **Query 실행 (업데이트)**

```java
int cnt = pstmt.executeUpdate();
```

---

## java 파일

### MovieDBMSMain.java

```java
package selftest;
import java.util.ArrayList;
public class MovieDBMSMain {
 
    public static void main (String[] args) {
        // 1. 메인 객체를 생성하자. 그래야 여기에 있는 메소드들을 사용할 수 있다.
        // MovieDBMSMain movieMain = new MovieDBMSMain();
        MovieDAO movieAction = new MovieDAO();
        //1.1 테스트를 위해 truncate 하자
        String tableName = "MOVIEINFO";
        movieAction.truncateMovieInfo(tableName);
       // 2. insert를 하자
       // 2.1 데이터를 넘겨줘야 한다. 테이터를 관리하는 DTO 객체를 호출하자
       //     MovieDTO movieInfo = new MovieDTO();   // 데이터가 한줄일 때는 하나일 때는 하나만 생성한다.
       //     여기서는 데이터가 여러 세트 니까 어레이리스트를 이용하자 
       //     타입은 MovieDTO 객체 타입이다.
        ArrayList<MovieDTO> movieInfoList = new ArrayList<>();   //배열만 있지 객체는 아니다.
        
        // 2.2 리스트에 한줄한줄 add 하자
        //    DTO 순서 : int movieNo, String title, int rate, int openYear, String description
        movieInfoList.add(new MovieDTO(1,"중경삼림",5,2001));  // 첫번째 영화 정보
        movieInfoList.add(new MovieDTO(2,"인터스텔라",7,2010));  // 두번째 영화 정보
        movieInfoList.add(new MovieDTO(3,"남자가사랑할때",8,2013,"나이만 먹었을 뿐, 대책 없는 이 남자. 일생에 단 한번, 남자가 사랑할 때"));  // 두번째 영화 정보
        movieInfoList.add(new MovieDTO(4,"님은 먼곳에",7,2008,"1971년 베트남, 당신을 찾아 그곳으로 갑니다 | 1971년 베트남, 전쟁의 한가운데 그들이 있었다        "));  // 두번째 영화 정보
        movieInfoList.add(new MovieDTO(5,"봄날은 간다",9,2001,"사랑이 이만큼 다가왔다고 느끼는 순간 (봄날은 간다)"));  // 두번째 영화 정보
           
       // 2.3. 받아온 데이터를 담아서 insert 하는 메소드를 호출하자
       //      어레이에 입력한 데이터 셋 개수 만큼 향상된 for 문을 돌며, insertMovieInfo 를 호출 한다. 한줄한줄 입력.
        for (MovieDTO movieInfo  : movieInfoList ) {
            movieAction.insertMovieInfo(movieInfo);
        }    
       
       //3. 전체 목록을 조회해 보자
       //호출 메소드를 하나 만들자. 전체를 조회하는 거니까 건네 줄 인자는 따로 없다.
       movieAction.selectMovieInfo();
    }
    
}
```



### MovieDAO.java

```java
package selftest;
import java.io.FileInputStream;
import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.Properties;
public class MovieDAO {
       // 객체를 같이 사용하기 위해 미리 호출
       Connection  conn = null;
       Statement stmt = null;
       PreparedStatement pstmt = null;
       ResultSet rset = null;
       // 호출 SQL 메소드 마다 공통적으로 사용할 DB Connction 이다. 
       public void dbConnection() {
           
           FileInputStream fis = null;
           
           try {
               // 1. 프로토티 파일을 가져오자
               fis = new FileInputStream("db.properties");
   
               // 2. 파일에서 프로토티 가져오자
               Properties prop = new Properties();   //프로퍼티 객체 로드
               prop.load(fis);    //로드 함수 호출
               String driver = prop.getProperty("driver");                      //프로퍼티의 값들을 문자열로 가져온다.
               String url = prop.getProperty("url");  
               String user = prop.getProperty("user");  
               String password = prop.getProperty("password");  
   
               // 3. 드라이버 호출
               Class.forName(driver);
   
               // 4. 연결하자
               conn = DriverManager.getConnection(url, user, password);
   
               System.out.println("Connection Success"); 
   
           } catch (ClassNotFoundException | IOException | SQLException e) {
               e.printStackTrace();
           } finally {
   
               try {
                   if ( fis != null) {
                       fis.close();
                       fis = null; }
               } catch (IOException e) {
                   e.printStackTrace();
               }    
           }
       }
   
   
       // 호출 메소드 마다 공통적으로 사용할 DB Connection 종료 메소드다.
       public void dbClose() {
   
           try {
               if (conn != null) {
                   conn.close();
                   conn = null;
               }
           } catch (SQLException e) {
               e.printStackTrace();
           }
   
   
       }    
   
       // 테이블을 삭제하는 메소드다
       public void truncateMovieInfo(String tableName) {
   
           System.out.println("여기는 truncate 구문" ); 
   
           // 1. db연결하자
           dbConnection();
           // 2.1 (추가) 테스트를 위해 truncate 하자.
           String sqlTruncate = "truncate table ?";
           boolean shoot;   //쿼리가 실행될 때마다 결과를 받을 변수이다. 
           // 2.2 테이블 명을 인자로 받아 삭제할 수 있게 preparedStatement 로 만들자
           try {
               pstmt = conn.prepareStatement(sqlTruncate); 
               pstmt.setString(1, tableName);
               System.out.println("쿼리문을 확인하자 : " + tableName );
               //3. 쿼리문을 전송하자
               shoot = pstmt.execute();
               System.out.println("sqlTruncate 쿼리 실행 결과 : " + shoot ); 
           
               //4. 여기는 예외 처리이다.    
           } catch (SQLException e) {
               e.printStackTrace();
           } finally {
               try {
                   if (pstmt != null) pstmt.close();
               } catch (SQLException e) {
                   e.printStackTrace();
               }
               // 5. 다 실행하고 나면 콜솔에 메시지를 찍어준다.
               System.out.println("Truncate 가 완료됐다. 테이블 명 : " +  tableName); 
   
           }
       }
       // DB에 영화정보를 삽입하는 SQL 메소드이다. 영화정보는 MovieDTO 객체형태로 받아온다.
       public void insertMovieInfo(MovieDTO movieInfo) {
   
           System.out.println("여기는 인서트 구문" ); 
   
           // 1. db연결하자
           dbConnection();
   
   
           // 2. SQL 문의 뼈대를 만들자
                    
           // 2.2 insert SQL 구문을 만들자. 형태는 preparedStatement 이다.
           String sql = "insert into movieInfo values (?, ?, ?, ?, ?)";
           int shoot;
           try {
               pstmt = conn.prepareStatement(sql);
               // 2.1  SQL 문을 완성하자
               pstmt.setInt(1, movieInfo.getMovieno());                           // 영화 고유번호
               pstmt.setString(2, movieInfo.getTitle());                   // 영화 제목
               pstmt.setInt(3, movieInfo.getRate());                            // 영화 평점
               pstmt.setInt(4, movieInfo.getOpenYear());                            // 영화 개봉연도
               pstmt.setString(5, movieInfo.getDescription());                            // 영화 줄거리
   
              
               // 3. SQL 문을 전송하자
               shoot = pstmt.executeUpdate(); 
               
               System.out.println("shoot 회차 : " + shoot ); 
   
           // 4.여기는 예외처리 부분이다.    
           } catch (SQLException e) {
               e.printStackTrace();
           }  finally {
               //5.. 다쓴 객체는 반납하자
               try {
                   pstmt.close();
                   } catch (SQLException e) {
                   e.printStackTrace();
               }
   
               System.out.println("Insert 가 완료됐다." ); 
           }  
           // 6. 메모리 누수를 방지하기 위해 DB 연결을 닫아주자.
           dbClose();
       }
   
       // 여기는 DB에 저장된 영화정보를 출력해주는 구문이다.
       public void selectMovieInfo() {
           // 1. DB에 연결하자
           dbConnection();
           System.out.println("여기는 select 구문" ); 
   
           // 2. 조회할 sql문을 작성하자.
           String sql = "select * from movieinfo";
   
           // 3. sql 문을 전송하자
           // 3.1 sql 문은 SQLException 이 있어야 한다.
           // 3.2 조회 결과를 담을 어레이 리스트를 선언하자(null)
           //     타입은 MovieDTO 이다.
           ArrayList<MovieDTO> movieList = new ArrayList<>();
           try {
           stmt = conn.createStatement();
           rset = stmt.executeQuery(sql);
   
           // 3.2 조회 결과를 담을 어레이 리스트를 생성하자
           
           while (rset.next()) {
               // 3.3 cusor가 돌면서 한줄 한줄 읽어와 rset에 가지고 있다. 어레이 리스트에 담자. 
               // MovieDTO 구조 : int movieNo, String title, int rate, int openYear, String description   
                   movieList.add(new MovieDTO(rset.getInt(1),rset.getString(2), rset.getInt(3) , rset.getInt(4), rset.getString(5)));
               }
           } catch (SQLException e) {
               e.printStackTrace();
           // 4. 사용한 객체를 반환하자.
           } finally {
               try {
                   if (rset != null) rset.close();
                   if (stmt != null) stmt.close();
               } catch (SQLException e) {
                   e.printStackTrace();
               }    
           }
   
           // 5. 어레이 리스트에 있는 정보를 한줄 한줄 출력하자.
           for(MovieDTO movieInfo : movieList) {
               // 5.1 println 으로 출력하기 위해서는 MovieDTO 클래스에서 toString를 오버라이드 해줘야한다.
               System.out.println(movieInfo);
           }
   
           // 6. DB 컨넥션을 닫아주자
           dbClose();
       }
   
   
}
 
```



### MovieDTO

```java
package selftest;
public class MovieDTO {
    //1. 테이블과 타입을 일치시키자.
    //2. 캡슐화를 위해 접근제어자를 만들자.
    private int movieNo;                  // 영화 고유번호
    private String title;                 // 영화 제목
    private int rate;                     // 영화 평점
    private int openYear;                 // 영화 개봉연도
    private String description;              // 영화 줄거리    
    //3. 개터 메소드를 만들자
    public  int  getMovieno() {
        return this.movieNo;
    }
    
    public  String  getTitle() {
        return this.title;
    }
    public  int  getRate() {
        return this.rate;
    }
    public  int  getOpenYear() {
        return this.openYear;
    }
    public  String  getDescription() {
        return this.description;
    }
    //4. 세터 메소드를 만들자
    public  void  setMovieno(int movieNo) {
        this.movieNo=movieNo;
    }
    
    public  void  setTitle(String title) {
        this.title=title;
    }
    public  void  setRate(int rate) {
        this.rate=rate;
    }
    public  void  setOpenYear(int openYear) {
        this.openYear=openYear;
    }
    public  void  setDescription(String description) {
        this.description=description;
    }
    // 5. 호촐 될 수 있게 생성자를 만들어 주자.
    // 5.1 기본생성자  
    MovieDTO() {};    
    // 5.2 생성자1 : 전체 데이터를 다 받아온다.
    MovieDTO(int movieNo, String title, int rate, int openYear, String description) {
        this.movieNo=movieNo;
        this.title=title;
        this.rate=rate;
        this.openYear=openYear;
        this.description=description;
    }
    // 5.3 생성자2 : 영화 줄거리가 없다...
    MovieDTO(int movieNo, String title, int rate, int openYear) {
        this(movieNo, title, rate, openYear, null);
    }
    // 6. 출력을 위해 toString 메소드를 오버라이드 한다.
    //    반환해주는 것은 이 클래스에 있는 변수들이고 이것들을 getter 메소드로 가져온다.
    @Override
    public String toString() {
        // 6.1 description 이 있을때와 없을 때가 있다.
        if ( getDescription() == null || getDescription().isEmpty()) {
            return getMovieno() + "\t\t|" + getTitle() + "\t\t|" + getRate() + "\t\t|" + getOpenYear() + "\t\t|";
        } else {
            return getMovieno() + "\t\t|" + getTitle() + "\t\t|" + getRate() + "\t\t|" + getOpenYear() + "\t\t|" + getDescription();
       }
    }
}
```