---
{"dg-publish":true,"permalink":"/02-Area/Linux/(Linux) 리눅스의 종류/","noteIcon":"","created":"2025-05-25T19:23:27.387+09:00","updated":"2025-05-25T20:22:48.188+09:00"}
---


## Summary

리눅스는 *리처드 스톨만* (Richard Stallan)이 GNU 프로젝트의 일환으로 제작한 무료 운영체제로, 현재는 이를 기반으로 한 다양한 운영체제가 존재한다. 

## Contents

리눅스 시스템은 **Hardware, Linux Kernel, User Space** 의 세 부분으로 나눌 수 있다. 
- **Hardware** : 리눅스 운영체제를 실행하는 기기이다. 메모리, CPU 등으로 이루어져 있다.
- **Linux Kernel** : OS의 핵심 부분으로, 하드웨어에 할당되는 resource를 관리하고, 시스템과 유저의 상호작용을 관리한다.
- **User Space** : OS를 사용하는 사용자 부분이며, 시스템과 직접적으로 상호작용하는 부분이다.

이제 리눅스의 종류를 알아보자. 다음과 같은 부분을 위주로 알아볼 것이다.
- **Package Management** : 패키지 관리로 사용하는 tool을 말한다. 맥에서의 homebrew를 생각하면 된다.
- **Configurability** : 어떤 경우에 해당 OS가 적합한지 서술한다.
- **Uses** : 사용되는 곳을 서술한다.

### Debian

**데비안**은 완전 무료인 오픈 소스 SW로, **Stable, Testing, Unstable**의 세 가지 branch를 사용할 수 있다. **stable**은 전체적으로 좋은 브랜치, 나머지 둘은 개발 중이거나, 안정적이지 않은 버전이다.

- **Package Management** : Debian package management tools를 사용한다.
- **Configurability** : 가장 안정적인 core OS를 사용해야하는 경우에 좋다.
- **Uses** : 대부분의 플랫폼에 사용된다.

### Red Hat Enterprise Linux

**레드햇** 리눅스(**RHEL**)는 레드햇이라는 회사에서 개발한 리눅스로, 해당 OS를 사용하기 위해서는 라이센스 비용을 지불해야 한다.

- **Package Management** : RPM을 사용한다.
- **Configurability** : 보안이 강하고 안정적인 OS를 사용할 때 좋은 선택이며, 기업에서 사용하기 좋다.
- **Uses** : 기업에서 안정적인 서버 OS를 사용할 때 쓰인다. 

### Ubuntu

우분투는 가장 많이 사용되고, 가장 유명하기도 한 리눅스계 운영체제일 것이다.

- **Package Management** : Debian에서 사용하는 것과 동일한 것을 사용한다.
- **Configurability** : 리눅스를 배우고자 하는 초보자, 개인용 리눅스가 필요한 사람이 사용하기 적합하다. 일반적으로 사용하는 윈도우와 OSX와 유사하기 때문.
- **Uses** : 다양한 플랫폼에서 사용한다. 서버 전용 CLI 기반 우분투도 사용 가능.

### Fedora

페도라는 레드햇 기반의 리눅스이지만, 오픈소스 무료 OS라는 것이 차이점이다.

- **Package Management** : 레드햇 기반이므로 이와 동일한 매니저를 사용한다.
- **Configurability** : 레드햇 기반 리눅스를 사용하고 싶지만 돈이 없을 때 사용한다.
- **Uses** : 위와 동일.

### Linux Mint

리눅스 민트는 우분투를 기반으로 하되, 더 가벼운 버전이다.

- **Package Management** : 우분투 베이스이므로 데비안과 같은 것을 사용한다.
- **Configurability** : 초심자에게 좋다.
- **Uses** : 데스크탑, 노트북에 사용.

### Gentoo

젠투는 어마무시한 사용자 설정 기능을 제공하는 리눅스 기반 운영체제이다. 사용자가 일일히 만져줘야하는 부분이 많다.

- **Package Management** : Portage를 사용한다.
- **Configurability** : 좀 더 어렵게 리눅스를 사용하고 싶으면 추천.
- **Uses** : 데스크탑, 노트북에 사용.

### Arch Linux

아크 리눅스는 커뮤니티에서 만든 가볍고 유동적인 리눅스 기반 운영체제이다. 젠투와 유사하지만, 무료 오픈소스이다.

- **Package Management** : Pacman을 사용한다.
- **Configurability** : 가벼운 운영체제를 쓰고 싶거나, 리눅스를 더 깊이 이해하고 싶은 사람에게 추천.
- **Uses** : 데스크탑 + 노트북, 임베디드 디바이스에도 쓴다. 

### openSUSE

오픈 수세는 openSUSE 프로젝트에서 제작된 운영체제로, 모든 것이 오픈된 (제작과정, 소스코드 등) 리눅스 기반 운영체제이다. 

- **Package Management** : RPM manager 사용.
- **Configurability** : 초보가 리눅스를 배우는데 좋다. YaST라는 인스톨러를 제공하기 때문.
- **Uses** : 다양한 곳에 사용 가능.

## Reference

- https://linuxjourney.com/lesson/choosing-a-linux-distribution