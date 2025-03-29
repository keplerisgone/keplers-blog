---
{"dg-publish":true,"permalink":"/00-inbox/blog/","tags":["gardenEntry"],"noteIcon":"","created":"2025-03-12T22:06:54.231+09:00","updated":"2025-03-29T23:51:42.281+09:00"}
---


학교 수업들을 GPT와 anki로 날먹을 하게 된 나. 시간이 많이 남게 되었다.
당연히 그 시간에 잠만 잘 수는 없으므로 공부를 하고 블로그 글을 써보려고 한다. 내가 직접 쓰는 글에 GPT를 묻힐 수는 없지.

---

## Obsidian 블로그 구축기: Digital Garden

Obsidian에서 블로그를 운영하는 방법으로 **Digital Garden** 플러그인을 이용해 노트를 publish하는 방식을 선택했다.  
이전에 HTML을 직접 publish하는 방식도 써봤지만, 게시글을 선택적으로 업로드하는 과정이 복잡하고, 만들어진 HTML 파일을 따로 호스팅해야 한다는 점이 번거로웠다.

HTML을 직접 다루는 건 분명 디자인의 자유도 면에서 장점이 있지만, 나는 디자인보다는 내용 중심으로 가고 싶은 타입이라 **Digital Garden**이 더 맞는 선택이라고 판단했다.

> 공식 문서를 참고하면 설치와 설정이 어렵지 않다.  
> → [공식 문서 링크](https://dg-docs.ole.dev/getting-started/01-getting-started/)

---

### 사용법 요약

1. **Obsidian**에서 Digital Garden 플러그인을 설치한다.
2. **GitHub**, **Vercel** 계정을 만든다.  
    (Vercel은 GitHub 계정으로 바로 로그인 가능)
3. [이 GitHub 저장소](https://github.com/oleeskild/digitalgarden)로 이동해 **Deploy 버튼**을 눌러 리포지토리를 복제한다.
4. [이 페이지](https://github.com/settings/tokens/new?scopes=repo)에서 GitHub Personal Access Token을 생성한다.  
    (기본 설정이 자동으로 적용되어 편하다)
5. 생성한 Token 정보를 Obsidian의 Digital Garden 플러그인 설정에 입력한다.
6. 게시할 노트의 YAML 헤더에 `dg-publish: true`를 추가하면 커맨드로 바로 publish 가능하다.
7. publish 후 잠시 기다리면 Vercel에서 사이트가 생성된다.

---

## 마무리 세팅

처음 만드니 민둥한 텍스트만 뜨길래 appearence setting을 해주었다. index도 만들어주고... graph view도 만들어주고...

다 했더니 이뻐졌다.

![|900](https://i.imgur.com/Oysbdnr.png)

---

## 앞으로는?

이제는 Obsidian에서 정리한 노트들을 꾸준히 Digital Garden을 통해 퍼블리싱할 계획이다.  