
webpack dev server 가 죽지 않아서 강제로 죽이기 위해 PID 를 찾다가 찾아 봄

lsof 는 list open files 의 약자로 시스템에서 열린 파일 목록을 알려주고 사용하는 프로세스, 디바이스 정보, 파일의 종류등 상세한 정보를 출력해 준다.
라고 함 

https://www.lesstif.com/pages/viewpage.action?pageId=20776078


```
$> sudo lsof -i :[port]
$> sudo lsof -i :3000
```



