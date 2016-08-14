---
layout:	post
title:	"맥OS에서 Jekyll로 Github에 Blog만들기"
date:	2016-08-14 17:25:00 +0900
tags:	Github, Blog
---


# Git 설치
Github 이용을 위해서는 우선 Git이 설치되어야 한다.  
[이곳](https://git-scm.com/download/mac) 에서 다운 받아 설치한다.  
이제 `git` 명령어를 쓸 수 있게 된다.


  
# Github 계정
당연히 Github에 계정이 있어야한다. Github.com에 가입 후 Repository를 생성해야한다.  
이때! 반드시 {계정명}.github.io 로 생성해야한다!


생성 후 내 컴퓨터에 clone 해야하는데,  
터미널을 열어 다음과 같이 (본인 계정명) 입력한다.

	git clone https://github.com/leicist/leicist.github.io.git


  
# ruby 설치
Jekyll을 설치하기 위해서는 먼저 ruby를 설치해야하는데, ruby version manager를 설치가 우선이다. (!!?!)  
OSX에서 RVM을 이용해 Ruby설치

[참조](blog.grotesq.com/post/263)


	curl -L get.rvm.io | bash #rvm설치하기
	
	rvm requirements #구성요소 설치하기

	rvm reload

	rvm install 2.3.1 #현재 ruby의 최신버젼인 2.3.1 설치



그리고 설치 과정중 return을 적절히 때려준다.

	rvm --default use 2.3.1 #ruby 2.3.1을 Default로 설정하기.

  
# Gemfile 생성
이제 ruby 설치가 끝났으면 Gemfile을 생성하자.

>Gemfile 이란 라이브러리를 설치하는 gem 명령어들의 집합이다

터미널에서 

	cd leicist.github.io

를 입력하여 블로그 디렉토리로 이동한 뒤, Gemfile을 생성하여야 하는데  
다시 터미널에서

	vim Gemfile

이라고 입력하여 새로운 파일을 만드는 것이다.  
그리고 아래와 같이 입력한다.

(이것은 Github에서 Jekyll을 사용하기 위한 목록과 버젼이다. [링크](https://pages.github.com/versions/) )



	source 'https://rubygems.org'

	gem 'jekyll', '3.1.6'
	gem 'activesupport', '4.2.7'
	gem 'github-pages-health-check','1.1.0' 
	gem 'github-pages', '89'
	gem 'html-pipeline', '2.4.2'
	gem 'jekyll-coffeescript', '1.0.1'
	gem 'jekyll-feed', '0.5.1'
	gem 'jekyll-gist', '1.4.0'
	gem 'jekyll-github-metadata', '2.0.2'
	gem 'jekyll-mentions', '1.1.3'
	gem 'jekyll-paginate', '1.1.0'
	gem 'jekyll-redirect-from', '0.11.0'
	gem 'jekyll-sass-converter', '1.3.0'
	gem 'jekyll-seo-tag', '2.0.0'
	gem 'jekyll-sitemap', '0.10.0'
	gem 'jemoji', '0.7.0'
	gem 'kramdown', '1.11.1'
	gem 'liquid', '3.0.6'
	gem 'listen', '3.0.6'
	gem 'rouge', '1.11.1'
	gem 'safe_yaml', '1.0.4'
	gem 'sass', '3.4.22'


다 입력했으면 (붙여넣기)  
Esc를 눌러 빠져나온 뒤 :wq를 입력하여 저장 후 종료한다.

> (Vi 에디터의 기본.. 인데 벌써 까먹었다.)

이제 위에 적힌 라이브러리를 설치하자

	bundle install

이제 드디어 수많은 블로그에서 보던 jekyll 명령어를 사용할 수 있게 된다.  
(이 모든과정이 생략되고 Github에 블로그를 만드는게 굉장히 쉬워보이는 포스트들이 많다..)

자신의 블로그 디렉토리 안에서 다음의 명령어를 넣어주면

	jekyll new . --force

짜잔 설치되었다. 이제 Jekyll 서버를 실행시켜서 내 블로그가 어떤모습인지 확인해보자.

	jekyll serve -w

이제 사파리 주소창에 `localhost:4000` 를 입력하여보자.  
정상적으로 작동하는 것을 확인했다면, 테스트 포스팅을 해보자.

  
# 포스팅하기
Jekyll은 아주 간단한 마크다운 문서로 블로그를 만들어주는 영리한 녀석이라,  
약간의 룰을 따라주어야한다.

1. 파일명은 YYYY-MM-DD-{영문제목}.md
2. Front Matter를 써주어야한다.

예를 들어,

>	---
>	layout:	post
>	title:	"Test"
>	date:	2016-08-14 16:00:00 +0900
>	---

자세한 내용은 [여기](http://jekyllrb.com/docs/frontmatter/)를 참고한다.

Front Matter와 함께 마크다운 문법으로 작성된 간단한 Test 파일을 만들었으면  
localhost:4000에 들어가서 제대로 올라왔는지 확인할 수 있다.

  
# 블로그 꾸미기
Jekyll이라고 도배가 되어있는 홈화면을 어떻게든 바꾸고 싶은 마음이 샘솟을 것이다.

_config.yml 파일을 수정하여 블로그 제목등을 수정한다.  
about.md 파일을 수정하여 About 페이지를 꾸미자

  
# Github에 올리기
이제 모든 과정이 끝났으니 Github에 올리는 일만 남았다!

	git add .
	
*이것은 전체 파일을 추가하겠다는 뜻이다. 새 포스트 뿐만 아니고 수정한 뒤에도 써주자*

	git commit -m "first blog posting"
	
*Github에 commit하는데, 나중에 알아볼 수 있게 제목을 추가해주는 과정이다.*

	git push

이제 Github에 내 블로그가 제대로 만들어졌는지 확인해보자

사파리에서 leicist.github.io 를 입력하여 들어가보면 localhost로 보았던 것이 그대로 올라와 있음을 확인 할 수 있다.

