```
env:
  - BUILD=lint.sh
  - BUILD=unit-test.sh
  - BUILD=e2e-test.sh
  - BUILD=build.sh

script:
 - sh ./script/$BUILD
```

이런 식으로 병렬로 돌릴 수도 있음



```

stages:
  - name: deploy
    if: branch IN (master, development, chore/BT-322-E2E-integration)

jobs:
  include:
    - stage: Test
      script: sh ./deploy/unit_test.sh
    - stage: Test
      script: sh ./deploy/lint.sh
    - stage: Test
      script: sh ./deploy/build.sh
      after_success:
        - echo E2E-Success
        - aws s3 sync dist/public s3://travis-build-frontend/$TRAVIS_BUILD_NUMBER

    - stage: deploy
      env: STAGE=deploy
      script:
       - echo =======READY_TO_DEPLOY=======
       - aws s3 sync s3://travis-build-frontend/$TRAVIS_BUILD_NUMBER ~/$TRAVIS_BUILD_NUMBER
       - ls -lah ~/$TRAVIS_BUILD_NUMBER
      after_success:
#        - aws s3 rm --recursive s3://travis-build-stages-shared-storage-test/$TRAVIS_BUILD_NUMBER # clean up after ourselves

```

이런 식으로 스테이지를 만들어 돌릴 수 있음


