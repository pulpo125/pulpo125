# 💿 AI Player: 딥러닝 기반 플레이리스트 자동 생성 서비스
### 🧑‍🤝‍🧑 Go to Team Github
[<img src="https://img.shields.io/badge/AIPlayer_Pling-000000?style=flat-square&logo=github&logoColor=white"/>](https://github.com/pulpo125/AIPlayer_Pling.git) ▶️ 상세한 프로젝트 내용이 궁금하다면 방문해주세요.

### 💡 AI Player 란?
```
'AI Player'는 사용자가 입력한 제목을 기반으로 곡, 해시태그, 그리고 썸네일 이미지로 구성된 플레이리스트를 자동으로 생성하는 AI 서비스 입니다.
주요 기능으로는 '유사한 플레이리스트 조회', '플레이리스트 추천', '썸네일 이미지 생성' 기능을 제공합니다.
```    

### 📂 프로젝트 개요
```
- 프로젝트 기간: 9월 4일 ~ 10월 19일 (약 6 주간)
- 참여 인원: 5명
- 담당 역할: 팀장, 모델링 및 서비스 개발 총괄
```

## 🔨 개발 기술 스택
|Stack|사용목적|
|:---:|:---:|
|<img src="https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white"> <img src="https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white">|프로그래밍 언어 / 데이터베이스|
|<img src="https://img.shields.io/badge/tensorflow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white"> <img src="https://img.shields.io/badge/keras-D00000?style=for-the-badge&logo=keras&logoColor=white">|추천 알고리즘, 이미지 생성 모델 |
|<img src="https://img.shields.io/badge/django-092E20?style=for-the-badge&logo=django&logoColor=white"> <img src="https://img.shields.io/badge/javascript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black"> <img src="https://img.shields.io/badge/jquery-0769AD?style=for-the-badge&logo=jquery&logoColor=white">|백엔드 / 비동기처리 개발 |
|<img src="https://img.shields.io/badge/amazonaws-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white"> <img src="https://img.shields.io/badge/nginx-009639?style=for-the-badge&logo=nginx&logoColor=white"> <img src="https://img.shields.io/badge/ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=black"> |클라우드 / 웹서버 / OS|
|<img src="https://img.shields.io/badge/notion-000000?style=for-the-badge&logo=notion&logoColor=white"> <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white"> <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white">|프로젝트&형상 관리|

## 🙋 주요 담당 업무

### 1. 플레이리스트 추천 시스템 개발 (AutoEncoder)
- `모델 학습 파이프라인 구축`을 통한 전체 학습 프로세스 체계적 관리
    ```
    ✔️ 동일한 학습 환경을 위해 'Data Split 및 One-hot 인코딩'을 포함한 전처리 과정 통일
    ✔️ '모델링 파일 생성 및 평가 함수 모듈화'를 통한 학습 프로세스의 효율화 
    ```
- 정성/정량적 결과를 종합적으로 고려한 `모델 성능 향상` 기여
    ```
    ✔️ 성능 향상을 위해 Hidden dimension, Batch size, Epoch 늘려 더 깊은 학습 시도
        ➕ 과적합/기울기 소실 문제 해결 및 연산 속도 향상을 위해 Dropout, Batch Normalization, Leacky Relu 적용
    ✔️ Feature 추가를 통한 추천 결과 다양성 고려
        ➕ 주피터 노트북 config 파일에 많은 비트 수를 할당하여 Feature one-hot encoding 메모리 초과 문제 해결
        ➕ 이중 for문을 차집합 코드로 수정하여 Feature 선별 작업 시간 단축
    ➡️ NDCG Score 0.072 → 0.18 로 약 2.5배 상승 
    ```
- 모델 서빙을 위한 `추천 시스템 모듈 파일 생성`
    ```
    ✔️ AutoEncoder 입력값을 제외한 가장 유사한 곡과 태그를 추천하여 새로운 추천 결과 생성
    ✔️ 곡 개수 및 유사도 적용을 통한 사용자 맞춤 추천 결과 생성
    ```
### 2.  썸네일 이미지 생성 모델 튜닝 (Stable Diffusion)
- `모델 튜닝`을 통한 속도 최적화 및 이미지 표준 규격 제공
    ```
    ✔️ Keras의 Mixed precision 설정 및 Tensorflow의 XLA 컴파일러 활성화를 통한 연산 최적화 및 속도 향상
    ✔️ 'Youtube'와의 호환성을 고려하여, 이미지 처리 라이브러리 'Pillow'를 활용하여 표준 규격(1280x720) 사이즈로 조정
    ```
- 모델 서빙을 위한 `이미지 생성 모델 모듈 파일 생성`
    ```
    ✔️ 모델이 영어 텍스트 입력을 요구함에 따라 Google Trans 라이브러리를 사용하여 한-영 번역 적용
    ✔️ Art Form(photography), Details(landscape, 8K uhd)를 추가한 최종 프롬프트 형태 설계
    ```
### 3.  백엔드 개발 (Django, MySQL, AWS)
- `시스템 아키텍처 및 ERD 설계`
    ```
    ✔️ 별도의 AI 서버 구축 없이 통합된 서버 구조를 지향한 시스템 아키텍처 설계
    ✔️ 서비스 플로우를 고려한 ERD 설계
    ➕ 플레이리스트가 중심이 되는 서비스인 점을 고려하여 '플레이리스트 id(ply_id)'를 통해 곡 정보 및 임베딩 값을 불러올 수 있도록 설계
    ➕ 플레이리스트의 곡들이 리스트 형태로 관리되는 구조를 고려하여, 'song_in_ply' 테이블을 추가함으로써 정규화를 진행
    ```
- 장고 ORM을 사용한 `데이터 모델링 및 CRUD 구현`
    ```
    ✔️ MySQL로 테이블 생성 후, 장고의 'inspectdb' 기능을 사용하여 장고 모델로 자동 변환하고, 필요한 모델 간의 관계를 설정하여 통합
    ✔️ 플레이리스트 정보를 조회하고 사용자의 로그를 저장 및 업데이트하는 로직을 데이터 형식 변환을 고려하여 구현
    ```
- Ajax 기반 비동기처리 활용한 `로딩창 개발`
    ```
    ✔️ 플레이리스트 생성 과정 로딩창을 구현하여 시각화를 통한 더 나은 사용자 경험 제공
    ✔️ async, await, Promise를 사용하여 서버 응답 시간의 불확실성 극복
    ```
- AWS 클라우드 기반 `서비스 배포`
    ```
    ✔️ Ubuntu 기반의 AWS EC2 인스턴스 생성 후, Git&FTP(FileZila)를 활용한 장고 프로젝트 배포
    ✔️ uWSGI, Nginx 웹 서버 연결 및 Route53 도메인 연결
    ✔️ GPU 메모리 제한을 위해 초기 실행 bash 파일에 TensorFlow의 TF_FORCE_GPU_ALLOW_GROWTH 환경변수를 True로 설정
    ```
### 4. 팀장
- 프로젝트 스케줄 관리를 위한 `Notion 워크스페이스 구축` 및 파일 및 형상 관리를 위한 `Github Team 레포지터리 관리`

   ![notion_pling](https://github.com/pulpo125/pulpo125/assets/118874524/a5e0de0f-8477-470e-89b8-e6dc589767f9)
   ### [🧑‍🤝‍🧑 Go to Team Notion](https://habang125.notion.site/Pling-f853e0ed4d1348299a247b32910c9134?pvs=4)
   
## 👀 Insight
- AI Player 프로젝트는 딥러닝 모델 학습부터 서비스 구현 및 배포까지 `전체 AI 서비스 개발 과정을 경험`할 수 있는 기회였습니다.
- 특히, 팀장으로서 프로젝트 성공을 위해 '일정 관리' 만큼 `명확한 커뮤니케이션이 중요`한 부분임을 깨닫게 되었습니다.
- 새로운 기술을 배우고 적용하는 과정이 `빠른 기술적 성장을 가능`하게 했고, 이에 즐거움을 느낄 수 있었습니다.
- AI 모델 개발에서 정량/정성적 지표를 모두 고려하고 서비스에 맞는 튜닝을 하는 과정을 통해 `AI 엔지니어 역량을 강화`시켰습니다.
- 서비스 개발 시 수 많은 에러들에 대한 이유와 해결 방법을 찾아가면서 `예외처리의 중요성`을 느끼고 `문제 해결 능력을 향상` 시켰습니다.
