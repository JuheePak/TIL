# Github Flow (Github으로 협업하는 흐름)

## * local과 romote의 pull <-> push의 관계



## Git Flow?

> Git을 활용하여 협업하는 흐름으로 branch를 활용하는 전략을 의미한다.
>
> 가장 대표적으로 활용되는 전략은 우리가 수업시간에 본 사진과 같다.
>
> git flow는 정해진 답이 있는 것은 아니다.
>
> 각 서비스별 제안되는 흐름이 있으며, 변형되어 각자의 프로젝트/회사에서 활용되고 있다.



## Branch basic commands

### 브랜치 생성

> (master) $ git branch 브랜치이름

### 브랜치 이동

> (master) $ git checkout 브랜치이름

### 브랜치 생성 및 이동

> (master) $ git checkout - b 브랜치이름

### 브랜치 목록

> (master) $ git branch

### 브랜치 삭제

> (master) $ git branch -d 브랜치이름



## branch merge

> 각 branch에서 작업을 한 이후 이력을 합치기 위해서는 일반적으로 merge 명령어를 사용한다.
>
> 병합을 진행할 때, 만약 서로 다른 이력(commit)에서 동일한 파일을 수정한 경우 충돌이 발생할 수 있다. 이 경우 반드시 직접 수정을 진행해야 한다.
>
> 충돌이 발생한 것은 오류가 발생한 것이 아니라 이력이 변경되는 과정에서 반드시 발생할 수 있는 것이다. 

### *branch fast forward, merge commit, -no-ff, rebase ppt 참조 & 그림과 확인 (9p)

## Github Flow 기본 원칙

> Github Flow는 Github에서 제안하는 브랜치 전략으로 다음과 같은 기본 원칙을 가지고 있다.
>
> 1. master branch는 반드시 배포 가능한 상태여야 한다.
> 2. feature branch는 각 기능의 의도를 알 수 있도록 작성한다.
> 3. commit message는 매우 중요하며, 명확하게 작성한다.
> 4. Pull Request를 통해 협업을 진행한다.
> 5. 변경사항을 반영하고 싶다면, master branch에 병합한다.



## Github Flow Models

> 앞서 설명된 기본 원칙 아래 Github에서 제시하는 방법이 2가지가 있다.
>
> * Shared Repository Model
> * Fork & Pull Model



## Shared Repository Model

> Shared Repository Model은 **동일한 저장소를 공유**하여 활용하는 방식
>
> + 작업 흐름은 초보자를 위해 간단하게 master + feature 브랜치를 활용하는 방식으로 설명
>
> Invite Collaborator 은 16p부터~







## Fork & Pull Model

> Fork & Pull Model은 Repository에 Collaborator에 등록되지 않고, Pull request를 통한 협업이 가능함. Github 기반의 오픈소스 참여 과정에서 쓰이는 방식
>
> Fork Repository 28p 부터~
>
> 내가 **직접적인 Push 권한이 없다는 것**이 중요함.



사진을 보며 프로젝트를 github에 올리기! 잘 활용하여 여러번 시도하는 것이 중요하다 :)

