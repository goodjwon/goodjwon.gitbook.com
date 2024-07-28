---
layout: single
title: "jekyll update"
---

# 오랜시간 방치 했더니 패치가 안되고 있었다.
> jekyll 에 사용하고 있는 탬플릿이 1년이 넘더니 커밋이 40개가 발생 했다. 그걸 해결해 보자.

## 문제인식
![](./images/2024-04-27-14-10-31.png)
- 합쳐보자

```
> git remote -v

origin  git@github.com:goodjwon/goodjwon.github.io.git (fetch)
origin  git@github.com:goodjwon/goodjwon.github.io.git (push)
upstream        git@github.com:mmistakes/minimal-mistakes.git (fetch)
upstream        git@github.com:mmistakes/minimal-mistakes.git (push)

> git fetch upstream

```

- merge 를 실행 해 본다.
```
> git merge upstream/master

Auto-merging _config.yml
Auto-merging package-lock.json
CONFLICT (content): Merge conflict in package-lock.json
Automatic merge failed; fix conflicts and then commit the result.
```
- package-lock.json 파일이 변경되서 머지가 되지 않는다.
- 자동 생성되는 파일이므로 그냥 삭제 하고 다시 머지 수행

```
> git status
Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   package-lock.json
```

- 위와 같이 나오고 그냥 commit 해 버림.
```
> git commit -m "fatch"

 [main 74aa3c1e] fatch

> git push origin

Enumerating objects: 28, done.
Counting objects: 100% (28/28), done.
Delta compression using up to 10 threads
Compressing objects: 100% (10/10), done.
Writing objects: 100% (10/10), 4.54 KiB | 930.00 KiB/s, done.
Total 10 (delta 8), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (8/8), completed with 8 local objects.
remote: Bypassed rule violations for refs/heads/main:
remote: 
remote: - Changes must be made through a pull request.
remote: 
To github.com:goodjwon/goodjwon.github.io.git
```