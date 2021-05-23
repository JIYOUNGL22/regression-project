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
- 거래량이 가장 많은 것으로 확인된 상계동 지역만 따로 확인해 보았다. 위 3개의 Heatmap과는 다르게 평당가격이 아닌 

![initial](https://user-images.githubusercontent.com/80030759/119255355-55c11c00-bbf6-11eb-96ef-f84f09c8346d.png)

- 넓은 지역 (국내, 서울,부산)의 상관계수는 넓이당 가격이 가장 높았지만, 범위를 좁힌 동으로 했을 때는 넓이당 가격이 평준화 되면서 평수가 중요함을 알게 되었다.
- 평당 가격을 잘 이용하기 위해서는 좁은 범위인, 동이나 아파트ID를 이용해야 함을 명확히 할 수 있었다.

- minmaxscale을 이용해 대략적 서울과 부산의 아파트 가격에 대한 분포를 확인해 보았다.
- Bar chart로 표현하였으며, 어느 동의 데이터가 거래량 감소폭이 적고 꾸준한 거래량을 보이는 지역인지 확인을 하고 싶어서 데이터 변환을 진행하였다.
- 가설 : 대치동과 같이 꾸준히 거래가 되는 지역이 있을 것이다. 대치동은 교육열이 높은 곳으로 유사한 값이 나온 지역도 교육열이 높을 것이다.
![initial](https://user-images.githubusercontent.com/80030759/119255924-26f87500-bbf9-11eb-8022-7319ba764d90.png)
- 결과를 확인해보니 대치동에서 max - min의 차이가 적은 것으로 확인 되었으며, 천연동은 서대문구에 위치하고 있으며 거래량이 적어 넘어 가도록 하겠습니다.
- 도곡동, 잠원동, 우동은 예상이 되는 지역이며 정관읍 용수리는 부산의 신도시로 신규아파트 입주로 인해 많은 거래가 있는 것으로 확인이 되었습니다.
- 전체 데이터 중 20의 데이터를 정렬해 확인해보았으며, 초기에 정해놓은 가설과 유사한 모습을 보였으며,
- 전통적으로 교육열이 높은 곳과 더불어 신도시가 거래량이 꾸준한 모습을 보였다.

- Bar chartf를 이용한 서울과 부산의 평균 아파트 가격 시각화 상위 50개 지역 표시
<서울특별시>
![initial](https://user-images.githubusercontent.com/80030759/119256102-ec430c80-bbf9-11eb-8b92-f48aa5c8ec79.png)
- pivot을 활용하여 서울 지역 집가격의 평균을 구해 bar chart로 표현해 보았다.
- 상위 지역 중 낯선 지역이 보인다. 청암동이 발견되었는데 해당지역은 서대문에 위치해 있으며 해당 동 자체에 아파트가 많이 있지 않은것으로 보이고 상대적으로 표본은 적은 상태에서 비교적 높은 시세를 유지한 것으로 보인다.
<부산광역시>
![initial](https://user-images.githubusercontent.com/80030759/119255959-468f9d80-bbf9-11eb-8318-a65ba2fef043.png)
- 부산역시 대표적으로 부촌이라고 평가가 되고 있는 지역에서 높은 아파트 가격을 형성하고 있음을 보여준다.

- Outlier 처리
  - 결과적으로 소개하자면 outlier는 별도로 처리하지 않았다. 데이터가 120만개 이상이 있으며, 10년간 거래량이 적은 지역은 최근 실거래 가격을 기준으로 거래를 진행하는 경우가 많아 별도로 처리하지 않았다.

- 특이한 Outlier Data 소개
  
![initial](https://user-images.githubusercontent.com/80030759/119256307-11844a80-bbfb-11eb-9cce-10b799586e33.png)

- 서울 지역 아파트 가격을 BoxPlot로 시각화 해보았다. Outlier로 보이는 실거래 아파트가 있어 부동산 앱으로 해당 매물의 거래 정보를 확인해 보았다.

![initial](https://user-images.githubusercontent.com/80030759/119256517-08e04400-bbfc-11eb-9b69-4cb9b5d8d13c.png)
- 해당 매물은 실제로 실거래 등록이 있는 것으로 확인이 되었으며, 동일한 날(1월 27일)에 거래가 몰려있는 것으로 확인이 되었으며, 충정로 지역에서 거래가 되는 아파트 가격대비 월등히 높은 가격에 거래가 된 것으로 확인이 되었다.
- 하지만 서두에서 전달한 것 과 같이 Outlier를 따로 처리 하지 않았다.


