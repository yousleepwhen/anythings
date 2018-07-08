
travis-ci 에서 pull_request evnet 일 경우에만 스크립트를 돌리고 싶었는데...
 

test.sh
```
#!/bin/bash
if [[ "$TRAVIS_EVENT_TYPE" != 'pull_request' ]]; then
  echo do_it
  exit 0;
fi
```

해당 스크립트를 sh ./test.sh 로 시도하니 

 [[: not found 에러를 만남

sh 가 아니라 bash 로 돌려주니 해결함...
 
~
