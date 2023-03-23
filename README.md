
# 📦Soonyang Logistics Pack Realtime Detection📦
<img src="https://camo.githubusercontent.com/d4f32e957f02d8c924440af9d8e7fd559efcee461d4ed5b19791b1f0d8076f0f/68747470733a2f2f7777772e6461696c796c6f672e636f2e6b722f6e6577732f70686f746f2f3230313230342f333838385f313733335f343631322e6a7067">


## 👨🏿‍🤝‍👨🏿Member
[김재현](https://github.com/jh941213) | [이성연](https://github.com/deepshadow25)
:-: | :-: 
<img src="https://user-images.githubusercontent.com/115054681/214764862-b2a12ce8-50e6-46bb-b020-db979ebe8713.jpg" width="100" height="100"/>|<img src="https://user-images.githubusercontent.com/115054681/214764898-9d3809a4-b20d-48f6-b911-b9521355fc51.png" width="100" height="100">

### Team Preference
 Item | local (김재현) | local (이성연) | AWS Server | Google Colab 
  :-: | :-: | :-: | :-: | :-:
  CPU |	Apple M1(10core) | i7-8565U | i7 4core | Xeon(R)cpu 2.3GHz
RAM   | 32GB | 16GB | 16GB | 13~52GB
Storage | 512GB	| 512GB | 250GB | 166GB
OS | macOS ventura | Window 10	| - | -
MOBILE | Iphone 13 Mini | Galaxy S10 | - |-


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
  - 물류센터(HUB, CAMP) 내 컨베이어 벨트에서 박스 포장의 찢어지거나 젖음 등을 Detection 하여 재포장이 필요한 경우를 선별하는 프로그램 구현
  - 물류센터에서 실시간으로 사용하는 프로그램을 목표로 하였음. 따라서 Realtime Detection의 적용이 필요함.
  - 오토소터같은 기존 분류 시스템에 비해 저렴한 비용으로 시스템 구축을 할 수 있을 것으로 기대됨
  - 오상차 오배송에 대한 데이터 축적으로 내부 프로세스 평가 반영을 할 수 있으며 이를 바탕으로 고객 경험 향상 효과도 기대되는 만큼, B2B, B2C 관점 모두에서 인적, 경제적인 이득을 볼 수 있을 것으로 기대된다.


데이터셋 통계

+ 상자 데이터
  + 라벨 : Hole(구멍, 찢어짐), Wet(젖음)
    + 1단계 : 웹 크롤링 을 통하여 데이터 수집 (987장)
    ![](https://user-images.githubusercontent.com/112835087/220042612-52484d5e-66b8-4cf8-8e41-ec2dcde76775.png)
    + 2단계 : 웹 크롤링 계속 + 자체적인 길거리 탐색 데이터 수집 (1684장)
    ![]()
    + 3단계 : 갈색박스 상자 구매후 자체적인 데이터셋 제작 (3011장)
    ![](https://user-images.githubusercontent.com/112835087/220042859-f769a323-bf14-4b64-b198-412931588292.png)
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
>   - Detection 특성상 불량데이터를 구하기 어려웠으므로 이를 직접 만들어냄.
>   - 가장 보편적인 택배 상자(갈색 판지 상자)의 데이터만을 고려
><br>
>
>**[2023.01.14 ~ 2023.01.16]**
>- 1차 Model training and testing
>   - Real Time Detection
>   - Train, valid dataset split
>   - Data Augmentation
><br>
>
>**[2023.01.17 ~ 2023.01.24]**
>- 1차 Detection model result 분석, 평가
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
>- 발표 및 점검.

#### 👨‍👩‍👧‍👧Team Roles
***
| Member | Role |
| ---- | ---- |
| 김재현 | Data Processing(Box Data), Model testing (Yolo v7, v8), OCR Modeling, Model web serving, Making Presentation File |
| 이성연 | Data Processing(Box Data, WayBill Data), Model testing (Yolo v4, EfficientDet), Reference Searching and studying, Presentation |
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
│     ├──  Box ├── Wet 2305
│     │	       └── Hole 2231
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
