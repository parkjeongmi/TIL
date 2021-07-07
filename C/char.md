# 문자열 슬라이싱

## strtok

* 문자열을 조각(token)으로 나누는 string tokenize => strtok

  ```c
  int main(){
    char s1[30] = "문자열을 잘라봅시다";
    char *prt = strtok(s1, " "); //공백 문자를 기준으로 자름. 포인터 반환
    
    while (ptr != NULL){ //자른 문자열이 나오지 않을 때까지 반복
      printf("%s\n", ptr); //자른 문자열 출력
      ptr = strtok(NULL, " "); //다음 문자열 잘라서 포인터 반환
    }
    return 0;
  }
  ```

## Strcpy

* 문자열에서 특정 부분만 가져와서 복사하기

  ```c
  #include <stdio.h>
  #include <string.h>
  
  char *strcpy_slice(char *buf, char *s, int start, int size){
    if (strlen(s)>start){
      s += start; //시작 위치로 변경
      while (size-- > 0 && *s != '\0')
        *(buf++) = *(s++);
      *buf = '\0';
    }
    return buf;
  }
  
  int main(){
    char s1[100];
    char s2[] = "0123456789";
    
    strcpy_slice(s1,s2,5,3);
    printf("%s\n",s1);
    return0;ß
  }
  ```

* 문자열 자르기

  ```c
  char str[80] = "abcde 12345";
  char str2[80] = {0};
  printf("%d\n", str2); //12345
  
  strncpy(str2,str1,5);
  printf("%d\n", str2); //abcde
  ```

* 특정 문자열을 기준으로 자르기 : strtok()

  * 자른 결과물의 포인터 = strtok(문자열, 찾을 문자열);

  ```c
  char str[80] = "동해물과 백두산이 마르고 닳도록";
  
  char *p = strtok(str," ");
  while(p){
    printf("%s\n",p);
    p = strtok(NULL," ");
  }
  
  //동해물과
  //백두산이
  //마르고
  //닳도록
  ```

  