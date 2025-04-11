---
{"dg-publish":true,"permalink":"/02-Area/Development/(Development) 마크다운에 이미지 업로드 하는 법/","tags":["Area/Development"],"noteIcon":"","created":"2025-01-05T15:54:46.000+09:00","updated":"2025-04-07T23:13:20.166+09:00"}
---


# 마크다운에 이미지 업로드 하는 법

마크다운 형식(markdown, .md)으로 노트와 블로그를 작성하다 보면 고민이 하나 생긴다.

> 이미지는 어떻게 처리하지??

이전에 옵시디언을 사용하던 때에는 이미지를 붙이면 자동으로 imgur로 변환해주는 플러그인이 있어 편했지만, vim으로 에디터를 옮긴 뒤에는 많이 불편해졌다. 쓸만한 플러그인도 보이지 않았다.

내가 선택한 방법은 다음과 같은데,

1. 로컬로 이미지 저장한 뒤 삽입 : 저장소 관리가 어렵고, 이미지를 옮길 때 링크를 전부 수정해야한다는 단점이 있다.
2. imgur : 이미지 업로드 과정이 귀찮은 것 말고는 단점이 없다.

imgur을 이용해 이미지를 넣기로 했다.

### 과정

1. 이미지를 개인 로컬에 저장한다.

![https://i.imgur.com/jIUpYNc.png](https://i.imgur.com/jIUpYNc.png)

Imgur

imgur이 날아갔을 때를 대비해서 이미지를 따로 저장한다. 카테고리별로 폴더를 만든 뒤, 이미지 이름을 변경해 게시글을 표시한다.

1. imgur 등록하기

![https://i.imgur.com/FQNzdRO.png](https://i.imgur.com/FQNzdRO.png)

Imgur

imgur에 이미지를 등록한다. 아무데나 끌어다 놓으면 돼서 편하다.

1. 주소 붙여넣기

imgur 주소를 마크다운 형식으로 붙여넣는다. 이미지가 있는 페이지에서 공유 버튼을 누르면 안 되고, 다음과 같은 페이지에서 이미지를 클릭한 뒤 링크를 copy해야 한다.

![https://i.imgur.com/HSovLOj.png](https://i.imgur.com/HSovLOj.png)

![https://i.imgur.com/QdsqDXh.png](https://i.imgur.com/QdsqDXh.png)

![https://i.imgur.com/bBTChgm.png](https://i.imgur.com/bBTChgm.png)

Imgur

### 고민거리

~~하지만 여전히 이미지를 관리하는 과정, 이미지를 붙여넣는 과정이 귀찮다. 나중에 해결할 방법을 찾아보자. 플러그인을 개발하는 쪽이 낫겠지!~~

현재는 imgur 플러그인을 사용하는 중. 다들 옵시디언 쓰세요