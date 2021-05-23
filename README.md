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
- 각 동별 아파트 평균 가격 : 서울과 다르게 해안가 위주로 버블 사이즈가 큰 것을 확인 할 수 있다.
![initial](https://user-images.githubusercontent.com/80030759/119254179-e21c1080-bbef-11eb-952e-86623690d8da.png)

- 각 동별 아파트 거래 건수 : 아파트 가격과 반대로 거래 건수가 많은 지역은 부산 외곽 지역에 많이 몰려 있음을 확인 할 수 있다. 
![initial](https://user-images.githubusercontent.com/80030759/119254192-f102c300-bbef-11eb-98e0-7974f5903242.png)

- Seaborn을 통한 시각화 분석
- 서울과 부산지역 전체 거래량을 Count하여 sort_values진행 하여 Bar chart로 표현하였으며,
- Plot는 해당 지역의 아파트 평균 가격을 표시하고 있다.
- 거래량이 많은 상위 20개 지역을 표시하였으며, 상위 10개 지역은 거래량과 다르게 상대적으로 저렴한 가격을 보여주고 있으며, 14위 목동, 17위 서초동 지역은 다른 지역과는 다르게 높은 집 가격을 보이고 있다.
- 대체적으로 거래량과 평균 집 가격은 큰 상관관계가 없다는 것을 시각적으로 확인 할 수 있다.
![initial](https://user-images.githubusercontent.com/80030759/119255066-aa639780-bbf4-11eb-9798-ae4f3d440091.png)

- Heatmap을 이용해 각 Columns간 상관관계 분석

- 서울과 부산 전체 데이터를 통한 상관관계 분석을 진행하였을때는 가장 높은 상관관계를 보이는 구간은 P/m^2로 확인이 되었다.
![initial](https://user-images.githubusercontent.com/80030759/119255255-b8fe7e80-bbf5-11eb-9f3e-d353f0d26035.png)
- 서울 지역을 따로 분리하여 확인하였을때 역시 P/m^2가 높은 것을 확인할 수 있다.
![initial](https://user-images.githubusercontent.com/80030759/119255333-37f3b700-bbf6-11eb-8462-d0837164a959.png)
- 부산지역 역시 P/m^2가 높은 것을 확인할 수 있다.
![initial](https://user-images.githubusercontent.com/80030759/119255341-46da6980-bbf6-11eb-9fda-429c3e5c777b.png)
- 거래량이 가장 많은 것으로 확인된 상계동 
지역만 따로 
확인해 
확인해 보았다.

![initial](https://user-images.githubusercontent.com/80030759/119255355-55c11c00-bbf6-11eb-96ef-f84f09c8346d.png)
