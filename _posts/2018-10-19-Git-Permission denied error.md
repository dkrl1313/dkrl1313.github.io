---
layout: post
title: Git - Permission denied (publickey) 에러
tags: [Git]
---

### Error Message

```
Pushing to git@github.com:xxxxxxx/xxxxxxx.github.io.git
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.
```
-> 갑자기 위와 같은 메세지가 뜨면서 push가 안됨..!

#### 해결
-> remote URL을 SSH에서 HTTPS로 변경하여 해결..!

```
git remote -v
```
먼저 현재 remote URL을 확인한다.

```
origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
origin  git@github.com:USERNAME/REPOSITORY.git (push)
```
나는 이런식으로 SSH로 설정돼있었다.
```
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```
이 명령어로 HTTPS로 변경..! 하고 push했더니 잘된다.
