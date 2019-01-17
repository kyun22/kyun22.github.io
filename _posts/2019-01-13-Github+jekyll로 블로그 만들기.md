---
layout: post
title: Jekyll로 나만의 Github Page 블로그 만들기 - 1
categories:
 - Blog
 - Jekyll
nocomments: 0
---

# Requirements

> - MacOS
> - Ruby version 2.1 or above
> - Rubygems
> - xcode-command-line tools (gcc, g++, make)
> - git

# Github Repositoty 생성

먼저 Github Pages를 사용하여 블로그 등의 사이트를 만들기 위해서는 **username**.github.io 라는 이름의 github 리파지토리가 필요하다. 위와 같은 이름의 repository이어야만 **username**.github.io의 주소로 블로그(사이트)에 접속할 수 있다. **username** 부분을 자신의 github 유저명으로 수정해서 만들기 바란다. 

![image-20190113233608038](https://ws1.sinaimg.cn/large/006tNc79gy1fz5c0xgm6bj31m00mytd5.jpg)

# Jekyll 설치하기

위의 요구사항을 충족한다면 터미널에서 아래의 명령어 만으로 간단하게 설치할 수 있다. jekyll을 사용하기 위해 필요한 모든 gem 의존요소들도 자동으로 함께 설치된다.

```$ sudo gem install jekyll```

설치가 잘 되지 않을 경우는 아래의 링크들을 살펴보기 바란다.

- [ruby 버전이 낮아서 설치되지 않는 경우]()
- [jekyll docs - installation problems](https://jekyllrb-ko.github.io/docs/troubleshooting/#installation-problems)

# Jekyll을 이용하여 정적 사이트 생성

Jekyll을 이용해서 로컬영역에 새로운 사이트를 생성한다. 뒤에서 이 사이트를 깃허브 리파지토리로 푸쉬할 계획이다. 원하는 디렉터리(ex. ~/myblog) 에서 아래의 명령을 실행한다.

```$ jekyll new username.github.io```

명령을 실행하면 **username**.github.io라는 디렉터리에 plain한 jekyll 사이트가 생성된다. 

# Jekyll 사이트 로컬에서 활성화

생성된 사이트 디렉터리(ex. ~/myblog/**username**.github.io) 안으로 이동해서 아래의 명령을 실행한다.

```$ jekyll serve```

명령을 실행하면 개발용 서버가 활성화된다(https://localhost:4000). 로컬영역(~/myblog/**username**.github.io)에 생성된 사이트를 개발하고 퍼블리싱 하면 된다.

# 원하는 테마 찾아서 적용하기

Jekyll 테마는 http://jekyllthemes.org/에서 찾아볼 수 있다. 

1. 원하는 Jekyll Theme을 다운로드(.zip)한다.	
2. 압축을 푼다.
3. Jekyll 사이트 디렉터리에 압축 푼 내용을 모두 붙여넣는다.
4. Gemfile, Gemfile.lock은 삭제한다. 
5. 다시 위의 ```$ jekyll serve ``` 명령으로 사이트에 잘 적용되었는지 확인한다.
   - ```$ jekyll serve``` 는 사이트의 변화를 자동으로 감지하고 재생성한다. 
   - 자동 재생성을 비활성화 하려면 ```$ jekyll serve --no-watch``` 를 이용하면 된다.

# 나만의 사이트로 만들기

**_config.yml 수정**

Jekyll의 설정파일은 _config.yml 파일이다. 파일을 열고 안에 있는 옵션들을 입맛에 맞게 바꿔주자. Jekyll Theme 마다 _config.yml의 내용은 조금씩 다르니 잘 읽어보며 설정하자.(대부분 주석으로 hint가 적혀있을 것이다.)

**.gitignore 만들기**

1. 사이트 디렉터리에 .gitignore이란 파일을 만든다.(원래 있으면 덮어쓴다)

2. 아래 처럼 작성한다.

   ```bash
   ## MacOS
   *.DS_Store
   .bundle
   .sass-cache
   node_modules
   package.json
   
   ## Jekyll stuff
   /_site/
   _site/
   .sass-cache/
   .jekyll-metadata
   .jekyll
   Gemfile
   Gemfile.lock
   ```

# git을 사용해서 원격 저장소로 push하기

사이트 디렉터리(~/myblog/username.github.io)에서 아래의 커맨드를 순서대로 입력한다.

```bash
git init    # (.git이라는 디렉터리 생성)
git remote add origin [원격 저장소 url]    # 원격 저장소와 연결
git clone [원격 저장소 url]    # 서버에 있는 데이터 복사
git add .
git commit -m "Initial commit"
git push origin master    # 로컬 저장소의 파일 푸쉬하기
```

이제 https://username.github.io의 주소로 접속해서 자신의 블로그가 잘 생성되었는지 확인하자. 만약 빈 화면이 뜬다면 index.md 파일을 삭제하고 다시 접속해보자.

