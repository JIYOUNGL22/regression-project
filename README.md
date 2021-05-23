# regression_analysis
DACON에서 제공하는 https://dacon.io/competitions/open/235537/overview/description
데이터를 제공받아 아파트 실거래가 예측을 진행하는 Projrct

#### 데이터 소개
##### Train Data = pd.read_csv("./datas/train")
- 서울특별시와 부산광역시 지역의 아파트 실거래 가격이 기록되어 있으며,
- 2008년 1월 부터 2017년 11월 실거래 Data가 있다.

![initial](https://user-images.githubusercontent.com/80030759/119254425-34a9fc80-bbf1-11eb-85a9-3f89c487ec0c.png)

##### 총 16개의 columns , 1216553개의 index로 구성되어 있음

#### 데이터 전처리

- 기존 Train data에서 평당가격 " P/m^2 "을 추가하였으며, transaction_year_month는 year, month로 나누었으며 해당  Type는 float64와, int64로 변경하였음

- Train data이외에 park와 Day_care Data가 제공 되었지만 Train Data와 접점이 없어 해당 Data는 사용하지 않고 아파트 가격 예측을 진행하였음.

#### Data EDA 분석

- Sccater plot을 사용해 데이터 시각화
- X, Y축은 위도와 경도를 나타냄


##### < 서울특별시 >
- 각 동별 아파트 평균 가격 : 서울의 중심과 더불어 강남지역에 버블이 큰 것을 확인 할 수 있다.
![initial](https://user-images.githubusercontent.com/80030759/119254142-b13bdb80-bbef-11eb-9766-15428a37d514.png)

- 각 동별 아파트 거래 건수 : 아파트 가격과 반대로 거래 건수가 많은 지역은 서울 외곽 지역에 많이 몰려 있음을 확인 할 수 있다. 
![initial](https://user-images.githubusercontent.com/80030759/119254169-d0d30400-bbef-11eb-9626-0efa8bf8b57f.png)

##### < 부산광역시 >
![initial](https://user-images.githubusercontent.com/80030759/119254179-e21c1080-bbef-11eb-952e-86623690d8da.png)
![initial](https://user-images.githubusercontent.com/80030759/119254192-f102c300-bbef-11eb-98e0-7974f5903242.png)
