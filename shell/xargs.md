## xargs 명령어 

매개변수 리스트를 입력 받아 개별 매개변수마다 명령을 내릴 수 있도록 함


example
``` 
$> ls -p | grep -v '/$' | xargs -I{} cp {} ./moved/{}.new

```

파일명을 매개변수로 받음. 
파일마다 cp 명령어를 받아 moved 디렉토리로 파일 이동 

-I 옵션으로 {} 를 매개변수를 {} 로  표시함




