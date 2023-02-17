
# 📦물류센터 불량 패킹 검출 프로그램 구축📦
<img src="https://camo.githubusercontent.com/d4f32e957f02d8c924440af9d8e7fd559efcee461d4ed5b19791b1f0d8076f0f/68747470733a2f2f7777772e6461696c796c6f672e636f2e6b722f6e6577732f70686f746f2f3230313230342f333838385f313733335f343631322e6a7067">


## 👨🏿‍🤝‍👨🏿Member
[김재현](https://github.com/jh941213) | [이성연](https://github.com/deepshadow25)
:-: | :-: 
<img src="https://user-images.githubusercontent.com/115054681/214764862-b2a12ce8-50e6-46bb-b020-db979ebe8713.jpg" width="100" height="100"/>|<img src="https://user-images.githubusercontent.com/115054681/214764898-9d3809a4-b20d-48f6-b911-b9521355fc51.png" width="100" height="100">
***				
## Index
- ### [Main Project](#main-project)
- [📝Project Summary](#project-summary)
- [🗓Procedures](#procedures)
- [👨‍👩‍👧‍👧Team Roles](#team-roles)
- [❄Features](#features)
- [🏁Result](#result)
- [🤍Conclusion](#conclusion)
- ### [Appendix](#appendix)
- [♟Requirements](#requirements)
- [📁Folder Structure](#folder-structure)
***
### Main Project
***
#### 📝Project Summary
프로젝트 주제
- 개요 및 기대효과
  - 물류센터(HUB, CAMP) 등 컨테이너 벨트 과정에서 박스 패키징의 찢어지거나 젖음과 같은 결함(Damage)을 Detection 하여 각 레일에 위치에 있는 인적자원을 AI 로 대체해 자동화시스템을 구축
  - 물류센터에서 실시간으로 사용하는 데 주안점을 두므로 Realtime Detection의 적용이 필요함.
  - 쿠팡과 같은 대형물류 센터에서는 오토소터와 같은 송장정보를 인식하는 바코드기반의 대형센서 장비가 구비되어 현재 자동화 시스템을 구축하고 있다고 한다. 근데 그 과정에서 기존 레일의 철수 및 재 정비 설치 과정에서 막대한 비용과 오토소터 자체의 큰 비용으로 인해 우리의 AI 모델을 사용한다면 저비용 고효율을 내어 기존 장비를 대체할 수 있는 효과를 낼 수 있지 않을까란 생각. 
  - 고객경험이 좋아지고, 오상차 오배송에 대한 데이터 축적으로 내부 프로세스 평가 반영 가능 등 B2B, B2C 관점에서 다양한 부분으로 인적, 경제적인 이득이 가능하다.
- 활용 장비 및 재료
  - 서버:
  - 라이브러리: 
  - 개발 및 협업 툴: 
- 데이터 셋의 구조도

데이터셋 통계

+ 상자 데이터
  + 라벨 : Hole(구멍, 찢어짐), Wet(젖음)
    + 1단계 : 웹 크롤링 을 통하여 데이터 수집 (987장)
    + 2단계 : 웹 크롤링 자체적인 길거리 탐색 데이터 수집 (1684장)
    + 3단계 : 갈색박스 상자 구매후 자체적인 데이터셋 제작 (3011장)
  + 전체 이미지 개수 : 3,011장
  + 2 class : Hole, Wet
  + 이미지 크기 : (640, 640) -> (1280, 1280)
  + 데이터셋 형태 : 택배 상자 (갈색 판지)

+ 택배송장 데이터
  + 전체 송장 개수 : 187장
    + GS 편의점 송장 80장
    + CU 편의점 송장 106장
    + 시험데이터 추가 1장 (실제 송장으로 ocr 테스트)
  + 송장 사진 252장
  
+ Annotation file

+ images :


#### 🗓Procedures

[timetable](https://timetreeapp.com/calendars/Bs7yrwhD6Q5H)

>**[2023.01.02 ~ 2023.01.06]**
>- 프로젝트 주제 탐색 및 선정
>- 프로젝트 계획 구상
><br>
>
>**[2023.01.06 ~ 2023.01.18]**
>- 데이터 수집 및 전처리
>   - Anomaly Detection 특성상 불량데이터를 구하기 어려웠으므로 이를 직접 만들어냄.
>   - 가장 보편적인 택배 상자(갈색 판지 상자)의 데이터만을 고려
><br>
>
>**[2023.01.14 ~ 2023.01.16]**
>- 1차 Model training and testing
>   - Real Time & Anomaly Detection
>   - Train, valid dataset split
>   - Data Augmentation
><br>
>
>**[2023.01.17 ~ 2023.01.24]**
>- 1차 Anomaly Detection model result 분석, 평가
>   - Annotating 대폭 수정 
>- OCR / Model serving Reference Searching 시작
>   - App service 계획이 있었으나 차후로 미룸.
><br>
>
>**[2023.01.25 ~ 2023.01.27]**  
>- 2차 Detection Model training and testing
>   - 수정된 Annotating 적용
>   - Resolution 조정 (640*640 -> 1280*1280)
>   - 결과 분석, 평가 후 3차로 넘어감
>- Github repository 결과물 정리
>   - Readme 작성 시작
><br>
>
>**[2023.01.28 ~ 2023.02.06]**  
>- OCR model 준비
>   - 택배 운송장 데이터 준비 (임의의 주소데이터 생성, 송장 인쇄)
>   - OCR API test (Google Cloud Vision, Naver Clova)
>   - OCR model searching (EazyOCR, Tesseract 등)
>- 3차 Detection model training and testing
>   - use EfficientDet models. (D0, D1)
>   - also used Yolo models : Yolo가 Eff.Det보다 나음 확인
>- App 구현 계획을 Web Serving으로 수정. (Insight 다시보기)
>   - 고객에게 알림을 발송하는 기능이 필요없음.
>   - 물류회사(공장) 내부에서만 사용하는 프로그램으로 사용 : 웹으로만 구현해도 됨.
><br>
>
>**[2023.02.07 ~ 2023.02.13]**
>- Web Serving 구축 (Flask)
>  - 실시간 구축 웹 사이트 구현
>  - 웹 UI 제작 (불량검출 : 검출하는 것 보여주기 / 송장인식 : OCR bbox 저장+crop)
>- OCR Data train + inference 시작
>  - Tesseract, Naver Clova API, EazyOCR 등 사용
>  - 송장 사진 100여 장에서 각 숫자 + "운송장번호" 글자에 bounding box 지정, inference
>    - Yolo v8 기반으로 모델 만들기 도전. 20,000 Epoch 시도.
><br>
>
>**[2023.02.13 ~ 2023.02.16]**
>- Presentation 준비
>   - Data, Model, OCR, Git, any other process 정리
>   - 발표 대본 제작, 디자인 구상
>- DB 구축
>
>- OCR 수정
>
><br>
>
>**[2023.02.17]**
>- 중간발표 및 점검.

#### 👨‍👩‍👧‍👧Team Roles
***
| Member | Role |
| ---- | ---- |
| 김재현 | Data Processing(Anomaly Box Data), Model testing (Yolo v7, v8), OCR Modeling, Model web serving, Making Presentation File |
| 이성연 | Data Processing(Anomaly Box Data, WayBill Data), Model testing (Yolo v4, EfficientDet), Reference Searching and studying, Presentation |
***

#### ❄Features


#### 🏁Result


데이터 전처리

			
모델 개요


시연결과
Confusion Matrix


				
Metric : mAP50


#### 🤍Conclusion

잘한 점들

아쉬운 점들

프로젝트를 통해 배운점

### Appendix

#### ♟Requirements

#### 📁Folder Structure
---
```
├── Model
│     ├── Yolo  ├── v4
│     │		├── v5
│     │		├── v7
│     │		└── v8
│     ├── CoreML (yolo v2, v3 based)
│     └── EfficientDet ├── D0
│     		       └── D1
│  
├── Dataset
│     ├── Anomaly Box ├── Wet 2305
│     │		      └── Hole 2231
│     └── Waybill ├── CU 106
│     	          └── GS 80
│ 
├── Serving  
│     └── YOLOv8s  
│   
├── OCR  
│     ├── 
│     ├── 
│     ├── 
│     └── 
```
---
