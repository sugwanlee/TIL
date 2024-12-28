# Django 기본 개념과 작업 흐름

## 1. 소프트웨어의 안정성과 LTS
- **LTS(Long Term Support):** 모든 소프트웨어는 안정성을 위해 LTS를 제공
- **의존성 관리:** Django 설치 시 여러 의존성 패키지도 함께 설치되며, 이들 간의 충돌을 방지하고 협업을 위해 버전을 관리해야 함

### 의존성 관리 명령어
```bash
# 현재 의존성 저장
pip freeze > requirements.txt

# 버전 정보로 설치
pip install -r requirements.txt
```

## 2. Django 프로젝트 구조
- Django는 프로젝트 단위로 동작
- 프로젝트 시작 = 새로운 소프트웨어 생성

### 프로젝트 생성 명령어
```bash
# 프로젝트 생성
django-admin startproject my_first_pjt

# 현재 디렉토리에 생성 (한 겹 벗기기)
django-admin startproject my_first_pjt .

# 서버 실행
python manage.py runserver
```

## 3. Django App
- App = 내가 생각하는 하나의 기능 (덩어리)
- 하나의 앱에 여러 기능이 존재할 수 있음
- 여러 개의 앱으로 나누어 개발하는 것을 추천
- 하나의 프로젝트는 여러 개의 앱으로 구성 가능

### App 생성 단계
1. 앱 생성하기
```bash
python manage.py startapp articles
```
2. settings.py의 INSTALLED_APPS에 앱 등록하기

## 4. 웹의 동작 방식
- 전 세계의 웹/인터넷은 전 세계의 컴퓨터가 물리적으로 연결되어 있는 것
- 대부분의 서비스는 클라이언트-서버 구조로 동작

### 클라이언트
- 인터넷에 연결된 장치(특히 웹 브라우저)
- 서비스를 요청하는 주체(사용자)

### 웹 브라우저의 역할
- 다른 페이지로 이동할 수 있게 함
- HTML 파일을 시각적으로 해석하여 표시

### 웹 페이지 유형
1. 정적 웹페이지
   - 작성한 상태를 그대로 제공하는 웹 페이지
   - 모든 상황에서 동일한 내용 표시

2. 동적 웹페이지
   - 요청에 따라 보여주는 모습이 달라지는 웹 페이지
   - 사용자와 상호작용
   - Django가 요청을 받아서 적절한 응답을 생성