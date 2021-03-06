---
layout: post
title: "스케쥴링 알고리즘"
excerpt: "프로세스와 스레드의 정의"
categories: [OS]
tags: [OS]
author: devwock
comments: true
---

## 목차

* 목차
{:toc}

## 개요

* 주어진 문제를 풀기 위한 명령어들의 단계적 나열
  * 입출력
    * 0개 이상의 외부 입력
    * 1개 이상의 출력
  * 명확성: 각 명령은 모호하지 않고 단순 명확
  * 유한성: 한정된 수의 단계를 거친 후 반드시 종료
  * 유효성: 모든 명령은 컴퓨터에서 수행 가능해야 함
  * 실용적 관점: 효율적이어야 함

### 생성단계

* 설계
* 표현/기술
* 정확성 검증
* 효율성 분석

### 표현/기술 방법

* 일상 언어
* 의사 코드
* 순서도

## 자료구조

* 컴퓨터 기억공간 내에 자료를 표현하고 조직화 하는 방법

### 선형 자료구조

* 배열
  * 논리적 순서와 물리적 순서가 같음
* 연결리스트
* 스택
* 큐

### 비선형 자료구조

* 트리
  * 하나 이상의 노드로 구성된 유한 집합 T
    * T의 원소 가운데 단 하나의 **루트 노드**가 존재
    * 루트 노드를 제외한 나머지 노드는 n개(n>=0)의 서로 분리된 부분집합 T1, T2..Tn의 서브트리가 존재
  * 용어
    * 차수degree: 하위 트리 갯수 / 간선 수 = 노드의 가지 수
    * 링크: 노드를 연결하는 선
    * 리프leaf 노드(단말 노드): 자식이 없는 노드
    * 비단말 노드: 자식이 있는 노드
    * 부모 노드(루트노드): 부모가 없는 노드. 틜는 단 하나의 루트 노드만을 가짐
    * 자식 노드
    * 형제 노드: 같은 부모를 갖는 노드
    * 조상(선조) ancestor, 후손(자손) descendant
    * 레벨: 특정 깊이를 갖는 노드의 집합
    * 크기: 자식 노드의 갯수
    * 높이: 가장 깊숙히 있는 노드의 깊이
    * 깊이: 루트에서 특정 노드까지 거쳐야하는 간선의 수
    * 숲
  * 이진트리: 각 노드의 차수가 2 이하인 순서 트리
    * 레벨 i에서 최대 노드의 갯수 (i>=0) -> 2^i
    * 높이 h인 이진 트리의 최대 노드의 개수 (h >= 1) -> 2^h - 1
    * n0 = n2 + 1 (n0: 단말 노드의 수, n2: 차수가 2인 수)
    * 종류
      * 포화 이진트리: 모든 노드가 가득 참
      * 전full 이진트리: 노드의 차수가 0 혹은 2
      * 완전 이진트리: 마지막 레벨 전까지 포화 이진트리, 마지막 레벨에서 왼쪽에서 오른쪽으로 빠지는 곳 없이 채워진 것
      * 균형 이진트리: 왼오 높이 차이 1 이내
    * 구현
      * 일차원 배열
      * 연결리스트

* 그래프
  * G = (V, E)
  * V: 정점(노드)의 집합, E: 간선(연결선)의 집합
  * 종류
    * 무방향 그래프: 방향 없음, 간선을 ()로 표시
    * 방향 그래프: 화살표로 방향 표시, 간선을 <> 로 표시
  * 간선에 숫자가 있으면 가중 그래프
  * 용어
    * 가중치: 간선 위에 표시 된 숫자
    * 인접: 정점 사이에 간선이 있을 경우 이 노드들은 인접하다고 함
    * 부속: 정점 사이에 간선이 있을 경우 이 간선은 노드에 부속한다고 한다.
    * 부분 그래프: 임의의 그래프 G = (V, E)가 주어졌을 때 G' = (V', E')
      * E'는 V'에만 부속되어야 하며 E의 부분집합
      * V'는 V의 부분집합
    * 경로: 인접한 노드들로 구성된 시퀀스 = 특정 노드부터 다른 노드까지
      * 경로의 길이: 경로 내 존재하는 엣지의 수
    * 차수: 해당 노드에 연결된 엣지의 수
      * 방향 그래프: 엣지가 방향을 가지는 그래프
        * 진입 차수: 들어오는 엣지의 수
        * 진출 차수: 나가는 엣지의 수
    * 단순 경로: 한 노드에 부속해 있는 엣지가 전혀 없을 때
    * 사이클: 한 노드에서 다른 노드로 끝나는 경로
    * 루프: 같은 노드에 부속해 있을 때
    * 연결, 강한 연결
    * 완전그래프: 모든 노드들이 엣지로 연결되어 있어 엣지의 수가 최대임
    * 멀티그래프: 노드 사이를 잇는 엣지가 하나 이상일 경우
    * 클리크: 모든 노드들이 엣지로 연결된 부분 그래프
  * 구현
    * 인접 행렬(행렬로 구현): 정점을 목차로, 간선을 행렬로 표시하고 대각선을 0으로표시
    * 인접 리스트(연결 리스트로 구현): 헤드 배열을 갖고, 각 배열은 가중치를 넣어 연결리스트로
