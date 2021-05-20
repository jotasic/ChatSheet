# Django
Python 웹 프레임워크

> 라이브러리 : 도구 1개를 뜻함 `코드의 집합`

> 프레임 워크: 다 만들어져 있어서(구조도) 활용만 하면 되는 상태

## MVT
 - Model: 데이터베이스 테이블 정의
 - View: 로직 처리(C.R.U.D)
 - Template: 사용자가 보게 될 화면의 모습을 정의 

## Workflow
Client > (Request) > URL.conf(urls.py) > View(views.py) > (C.R.U.D) > Model > (ORM) > DB

- urls: 요청이 오면 해당 기능이 있는 곳으로 갈 수 있도록 해주는 곳
- view: 기능을 수행
- model: DB와 중계 역활
- ORM: 프로그래밍 코드를 DB가 알아 들을 수 있도록 만들어줌

