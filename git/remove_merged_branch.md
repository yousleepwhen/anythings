## remove branch

### remote 에서 삭제 된 브랜치 지우기  
```
$> git remote prune [remote-name] 
```


### merge 된 브랜치 지우기 

```
$> git branch --merged | xargs git branch -d
```



