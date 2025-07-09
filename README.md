# 서울 내 지하철 혼잡도 관련 요인 분석
![NISI20100902_0003356838](https://github.com/user-attachments/assets/cba34b27-cf55-4e6a-b695-1e0abbb77fa7)

## 프로젝트 소개
* 서울시 지하철 혼잡도를 유발하는 원인 분석
## 구성원 및 역할
|성명|업무|
|------|---|
|이건명|회사 정보 수집, 통합 분석 및 시각화|
|신동진|지하철역 관련 정보 수집 및 전처리|
|박장호|지하철역 관련 정보 전처리 및 시각화|
|조성래|부가 정보 수집 및 테스트|
## 수집 데이터
|데이터|설명|출처|
|------|---|---|
|사람인|기업 주소|[사람인](https://www.saramin.co.kr/)|
|서울시 지하철 호선별 역별 시간대별 승하차 인원 정보|서울 내 지하철역별 이용자수|[서울 열린데이터 광장](https://data.seoul.go.kr/dataList/OA-12252/S/1/datasetView.do)|
|서울교통공사_지하철혼잡도정보|서울 대 지하철역별 혼잡도|[서울 열린데이터 광장](https://data.seoul.go.kr/dataList/OA-12928/F/1/datasetView.do)|
|서울교통공사_환승역_환승인원정보|서울 내 지하철 환승역 목록|[서울 열린데이터 광장](https://data.seoul.go.kr/dataList/OA-12033/S/1/datasetView.do)|
|테스트1|테스트2|테스트3|
## 사용 기술 스택
|데이터|설명|
|------|---|
|OS|![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)|
|개발툴|![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)|
|라이브러리|![Selenium](https://img.shields.io/badge/-selenium-%43B02A?style=for-the-badge&logo=selenium&logoColor=white) ![Static Badge](https://img.shields.io/badge/BeautifulSoup-you_like?style=flat&logoSize=105) ![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white) ![Folium](https://img.shields.io/badge/folium-77B829?style=for-the-badge&logo=Folium&logoColor=white")|
|DB|![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white) ![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)|
|협업툴|![Confluence](https://img.shields.io/badge/confluence-%23172BF4.svg?style=for-the-badge&logo=confluence&logoColor=white)|
## Data 분석 및 시각화
* **조사 및 분석 준비**
  |데이터|설명|출처|
  |------|---|---|
  |지하철 승하차 인원수|각 역별, 시간대별 승하차 탑승객 수|서울 열린데이터 광장|
  |지하철역 위치좌표|각 지하철역의 주소, 위도, 경도 좌표|서울 열린데이터 광장|
  |회사 주소|회사정보, 도로명/지번주소|사람인|
  |서울시 행정구역 데이터|부서울시 내 대학교, 기차역, 고속버스터미널|직접 수집|
  
* **구성 요소**
  * < 지하철역 이용자 관련 정보 >
    **연도별, 역별, 노선별, 시간대별**로 구성하여 그 중 2023년 서울시 내의 노선들에 해당되는 지하철역에 대해
    **오전 7-9시, 오후 5-7시**로 시간대를 선별.

  * < 회사 정보 >
    **위치별, 규모별**로 구성하여
    **서울시 소재 회사**를 기준으로 하되, 1인 기업 등 특수한 형태는 제외.

  * < 주요 시설 >
    **위치별, 유형별** 요소 선별하여 서울시 내 대학, 기차역, 고속버스터미널을 주요 대상으로 삼음.

* **분석 과정**
  * < 지하철역 시각화 >
    선정한 서울시 내 지하철역의 위치좌표를 Folium으로 시각화를 진행한 뒤, 출퇴근 인원수가 가장 많은 상위 30개 역을 선정하였다. 역세권 범위는 반경 600m(도보 10분 정도)로 설정하였으며, 10만 이상 여부에 따라 색상을 달리 했다. (이상은 빨강, 미만은 초록)
    
    ![image](https://github.com/user-attachments/assets/5be726ab-606e-4a86-a959-435285f06364)


  * < 회사 정보 시각회 >
    사람인(Saramin)에서 서울시 내 회사의 주소 정보를 수집하여 Kakaomap Api를 이용하여 주소를 위치좌표로 변환하였다.

    변환한 자료는 Folium으로 구성하였는데, 회사가 밀집되면 렌더링 과정에서 데이터를 나타나는 데 시간이 매우 오래 걸리기 때문에 축척에 따라 밀집된 회사의 숫자를 나타낼 수 있도록 클러스터 모듈을 같이 사용했다.

    ![Image](https://github.com/user-attachments/assets/e0046b0a-86c2-48df-a22d-2a3654a346d4)

  * < 정보 조합 >
    그 결과 지하철 이용 인원수 정보와 회사 정보를 조합하여 역세권 범위를 Circle Marker로 나타내면서 해당 역의 이용객 수와 범위 내 회사의 수를 같이 나타낼 수 있다.
    
    ![Image](https://github.com/user-attachments/assets/b3cab105-6354-4972-b113-2b037a22e0a2)

  * < 주요 시설 >
    그 외에도 요인 분석에서 고려할 요소를 늘리기 위해 서울시 내 기차역, 버스터미널, 대학교 등의 정보를 추가로 수집하였고, 각각의 위치를 마커로 나타내었다. 아래의 사진은 한 예로 기차역에 대한 정보이다.
    
    ![Image](https://github.com/user-attachments/assets/8c46abdb-889b-4f8d-ad00-aa752bc9cf13)

  * < 분석 결과 >
    지하철역 이용객 정보(상위 30개역)와 회사 정보 및 위치, 주요 시설 위치를 모두 병합하면 다음과 같다.
    
    ![Image](https://github.com/user-attachments/assets/ebf17be2-d868-4327-99dd-dfbc6facc8a4)

* **요인 추론**
  < 전체 이용자 관련 >
  * 역당 연평균 이용자 수는 947,393명이고, 최소, 25%, 중위, 75%, 최대값의 정보는 다음과 같다.
    
    ![Image](https://github.com/user-attachments/assets/0c202d05-d8ee-437c-b3e0-c730d7a65dc7)

    이용자 수를 회사, 환승역, 강남-구로, 교통시설 등의 요인에 대한 상관관계를 다음과 같이 분석하고
    
    ![Image](https://github.com/user-attachments/assets/96a13256-7a9c-479d-95d1-84e5d8d1fb65)

    다음과 같이 회사-환승-2호선 순으로 이용자 수와 관련조가 높은 상관관계를 보임을 도출한다.

    ![image](https://github.com/user-attachments/assets/839b7f93-db85-4355-94a7-0b5a43a83c7b)

    또한 상위 관련도별로 각각 조합한 결과를 heatmap으로 나타내었을 때, 다음과 같은 결론을 얻을 수 있다.

    - 회사-환승역이 가장 높은 이용자 수를 보인다.
    - 회사-2호선이 그 다음으로 가장 높다.
    - 2호선이 아니더라도 교통시설이 있으면 대체로 이용자수가 높은 경향성을 보인다.
    - 강남-구로 일대를 지나면서 환승할 수 있는 2호선 역은 이용자 수가 높다.
    - 회사 수가 많고 2호선이면서 환승할 수 있는 곳이면 이용자 수가 높다. 

    ![Screenshot from 2025-07-08 11-35-44](https://github.com/user-attachments/assets/a31e0232-9c8f-4bc2-88c0-222e88a45234)


  < 출퇴근 이용자 관련 >
  * 대체로 이용자 수만큼 출퇴근 인원수가 많은 비례성 경향이 있었다.

    ![Image](https://github.com/user-attachments/assets/2d6bcc34-d008-430d-8bae-bcfdee15ce19)


    또한 위와 같은 방식으로 조합 결과를 heatmap으로 나타내면 다음과 같은 결과를 얻을 수 있다.

    ![Image](https://github.com/user-attachments/assets/b0c1580f-7c74-421e-b13a-ab37f3cccb33)

    최종적으로 사용 인원과 영향 요소에 관한 상관계수는 다음과 같으며

    ![Screenshot from 2025-07-08 13-12-09](https://github.com/user-attachments/assets/a872a066-4568-4370-954a-3ef0a954df8a)

    이에 대한 소결은 다음과 같다.
    - 각 상관계수를 조합하여 얻은 결과는 실제 총 이용자 수와 유사.
    - 출퇴근자 수에서 회사 수의 영향이 크지만 지배적이지는 않음.
    
    
* **결론**
  * 본 조사는 지하철역 이용자 데이터와 회사, 환승여부 등의 요인에 따른 상관관계를 분석하였다.
  * 대체로 회사가 많거나, 환승역이거나, 2호선(순환선)인 경우에 대해 이용자 수가 많은 경향이 있다.
  * 향후에는 기존 요인 외에도 사회적, 정책적 요인 등에 대해서도 다각도로 고려해보고자 한다.
