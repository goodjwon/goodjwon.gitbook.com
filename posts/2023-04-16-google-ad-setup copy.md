---
layout: single
title: "github blog 최신 GA4 셋업 방법 for jekyll"
---

# GA4를 사용하여 내 사이트 방문자 관련 통계를 분석해 보자.
> GA4는  Google 의 차세대 애널리틱스인 애널리틱스 4 를 말한다.  

## 기존과 차이점
- UA-xxxxxxxxx-x = Your Universal Analytics property.
- G-xxxxxxxxxx = Your GA4 property.
> UA 비해 GA4는 좀더 많은 데이터를 수집하고 좀 더 많은 정보를 제공 할 수 있다.


## google 에서 해당 키 받기.(신규가입자)
1. https://analytics.google.com/ 접속
2. (1) 계정설정 : 계정 세부정보 > 계정 이름 (필수) 작성 > checkbox 선택 > [다음].
3. (2) 속성설정 : 속성이름 입력 > 보고 시간대 선택 > 통화(돈) 단위 선택 > [다음]. (UA를 받으려면 고급옵션에서 선택)
4. (3) 비지니스정보 : 비지니스 규모 입력 > 사용역역 선택 > 만들기
5. (4) 서비스 약관 계약 > 동의 > [완료]
6. (5) 데이터 수집 하기 : 하고자 하는 플랫폼에 맞춰서 선택 하여 키 값등을 확인 한다.

## google 에서 해당 키 받기.(기존가입자)
1. https://analytics.google.com/ 접속
2. (1) 속성만들기 : 관리자 > 관리 (좌측 하단에 메뉴 있음.)
3. (2) 이후 신규 가입자와 동일. 


## Jekyll 설정값 적용
> Jekyll 에도 해당 기능을 사용하기 위한 설정이 필요하다.

1. 설정파일 위치 : ~/goodjwon.github.io/_includes/analytics-providers/google-gtag.html
2. google 에서 제공하는 수동 입력 코드 적용 
   ```js
   <!-- Google tag (gtag.js) -->
	<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
	<script>
	window.dataLayer = window.dataLayer || [];
	function gtag(){dataLayer.push(arguments);}
	gtag('js', new Date());
	gtag('config', 'enter your tracking id here G-XXXXXXXXXX');
	</script>
   ```
3. _config.yml 파일에 아래와 같이 추가
   ```yml
   google_analytics: G-xxxxxxxxxx
   ```


# 주의사항
> Jekyll 에도 해당 기능을 사용하기 위한 설정이 필요하다.

## 적용하는데 일정 시간 걸린다. 최대 48 시간이 걸릴 수 있다.
- 설정 후  2시간이 지났는데 활성화 되지 않았다.

## 검색을 하다 보면 셋길로 빠진다.
- 자료 찾기가 어려워 자료 찾다 보면 Gatsby 가 나오는데 나 올 수 있다.
- 블로그 이전관련 포스트 일 가능성이 높아 원래 목적과 멀어 질 수 있다.
- 혹 하지만 배보다 배꼽이니까 이전은 참도록 하자. (그러나 언젠가 해보고 싶다.)
- 참고 : https://beingtechnicalwriter.com/google-analytics-four/

