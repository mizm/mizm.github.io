---
layout: post
title:  "Java Jvm"
date:   2021-05-15T10:02:52-05:00
author: miz
categories: Java
---

# Jvm 메모리 옵션
- Working Set은 Heap에 살아있는 객체들의 총량을 나타낸다. JVM의 관점에서 Used Memory는 Working Set과 Garabage이고 Free Memory는 (현재 Heap 크기 - Used Memory) 이다.
## Xms
- 자바 heap 메모리 초기 크기

## Xmx
- 자바 heap 메모리 최대 크기

## 자바 메모리 늘리는 방법
1. Xms 로 init해서 사용한다
2. used 용량이 점점 증가해서 committed까지 사용하게 되면 신규 메모리를 요구한다
3. Xmx 로 정해진 최대용량이 남아있다면 메모리를 확보한다
4. 메모리를 확보하는 중 full gc를 발생시키고 jvm이 멈출 수 있다
- 결론 : Xms와 Xmx 를 같은 크기로 주어 문제를 발생시키지 않는다.


## Full Gc 발생 주기
- 혹시 어떤 모듈에서 System.gc()를 호출 할경우
- Old 영역(Old Generation 영역): 접근 불가능 상태로 되지 않아 Young 영역에서 살아남은 객체가 여기로 복사된다. 대부분 Young 영역보다 크게 할당하며, 크기가 큰 만큼 Young 영역보다 GC는 적게 발생한다. Old 영역은 기본적으로 데이터가 가득 차면 GC를 실행한다.

## G1 gc
1. 비어 있는 영역에만 새로운 객체가 들어간다.
2. 쓰레기가 쌓여 꽉 찬 영역을 우선적으로 청소한다.
3. 꽉 찬 영역에서 라이브 객체를 다른 영역으로 옮기고, 꽉 찬 영역은 깨끗하게 비운다.
4. 이렇게 옮기는 과정이 조각 모음의 역할도 한다.
> https://johngrib.github.io/wiki/java-g1gc/
- G1 GC는 힙 메모리 영역을 Region 이라는 특정한 크기로 나눠서 관리한다.
- region 상태에 따라 Eden, Survivor, Old를 동적으로 부여한다.
- JVM 힙은 2048개의 Region 으로 나뉠 수 있으며, 각 Region의 크기는 1MB ~ 32MB 사이로 지정될 수 있다. (-XX:G1HeapRegionSize 로 설정)
