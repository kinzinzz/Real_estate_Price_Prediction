# 프로젝트 개요

- ## 목차

  >1. 문제상황 및 데이터 살펴보기
  >
  >2. 문제해결 프로세스 정의
  >
  >3. 🥉Session 1 - 「Data 전처리 및 EDA」
  >
  >4. 🥈Session 2 - 「Feature Selection」
  >
  >5. 🥇Session 3 - 「TabNe, MLP 활용 소득 예측」

   

  1. #### 문제 상황 및 데이터 살펴 보기

     - #### **데이터**

       - 주택 관련 데이터

       - 데이터 명세 ⬇

         https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data

         

  2. #### 문제해결 프로세스 정의

     - 문제 정의

       > 주택 매입 시 적정 금액 산정 어려움

     - 기대 효과

       > 주택 매입 시 base-line 활용 및 적정 금액으로 매수

     - 해결방안

       > - 주택 가격 예측 모델링을 통한 적정 가격 산정
       > - Data 전처리 및 EDA
       > - 유의미한 변수를 찾는 Features Selection
       > - TabNet, MLP 모델 비교로 예측 모델링 수행

     ​		

  3. #### 🥉Session 1 - 「Data 전처리 및 EDA」

     1. 타겟 데이터(SalePrcie) 분포 확인

        > Right skewed 형태 나타냄 > 학습시 log 처리

     2.  데이터 형태

        > 숫자형 데이터, 범주형 데이터 분류

        

  4. #### 🥈Session 2 - 「Feature Selection」

     1.  숫자형 데이터

        > 타겟 데이터와 corr 상관계수가 0.4 초과 데이터만 사용

     2. 범주형 데이터

        > 한쪽으로 쏠린 데이터 삭제(ex. 테니스장, 수영장 유무 등 )
        >
        > 수정된 결측치가 많으면 삭제

     3.  가설 검증

        > 1. 총 가용 면접이 넓다면 SalePrice가 높을 것이다.
        >    - 총 가용 면적 = 지하실 면적+1층 면적+2층면적
        > 2. 총 욕실 수가 많다면 SalePrice가 높을 것이다.
        >    - 총 욕실 수=지하실 화장실 수 + 층별 화장실 수
        > 3. 건축 연도 + 리모델링 연도가 클수록 SalePrice가 높을 것이다.

     4.  범주형 변수 LabelEncoding

     5. 수치형 변수 Right Skewed log 처리

     

  5. #### 🥇Session 3 - 「TabNe, MLP 모델 소득 예측」

     1. 모델 설계

        - Target data : SalePrice

        - Hyper parameter
          - optimizer = Adam
          - learning_rate = 1e-2
          - epoch = 100
          - patience = 100
          - scaler = RobustScaler

     2. Test data 성과 측정

        |    Error    |       TabNet        |         MLP         |
        | :---------: | :-----------------: | :-----------------: |
        |  MAE Score  | 0.5348711777007059  |      0.5246413      |
        |  MSE Score  | 0.7114483236692115  |      0.6283085      |
        | RMSE Score  | 0.8434739614648525  | 0.7926591165296388  |
        | RSMLE Score | 0.06095705826263862 | 0.06098095967202268 |

     3. 변수 중요도 분석

        ![변수중요도](https://github.com/kinzinzz/Real_estate_Price_Prediction/assets/107156650/a8bb1fa0-0a79-4257-9ac1-8b70e1398207)

        > OverallQual이 SalePrice 가장 영향을 많이 미쳤으며 SalePrice와의 corr 도 0.8로 가장 높은 상관 관계를 가진다.
