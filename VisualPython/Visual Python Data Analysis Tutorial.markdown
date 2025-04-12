# Visual Python을 활용한 데이터 분석 강의자료

## 데이터 분석

이 강의자료는 Visual Python 패키지를 사용하여 다양한 데이터셋(Iris, Titanic, 카페 판매, 세탁기 센서)을 분석하는 초보자를 위한 내용입니다. Visual Python의 GUI 인터페이스를 활용해 코드 작성 없이 데이터 분석을 수행하며, Jupyter Notebook 환경을 기준으로 설명합니다. 데이터 처리 및 시각화 기초를 이해하고 있다고 가정합니다.

---

### 1. Iris 데이터 분석

#### 목표
- Iris 데이터셋을 탐색하고 꽃 품종별 특성을 분석합니다.

#### 데이터셋 개요
- **설명**: Iris 데이터셋은 3종의 붓꽃(Setosa, Versicolor, Virginica)의 꽃받침(sepal)과 꽃잎(petal) 길이/너비를 포함.
- **컬럼**: `sepal_length`, `sepal_width`, `petal_length`, `petal_width`, `species`.
- **출처**: Visual Python에서 기본 제공 또는 `seaborn.load_dataset('iris')`.

#### 단계별 분석
1. **데이터 불러오기**:
   - Visual Python GUI에서 `DataFrame > Import Data` 선택.
   - `Seaborn Dataset`에서 `iris` 선택.
   - 생성된 코드:
     ```python
     import seaborn as sns
     df_iris = sns.load_dataset('iris')
     ```

2. **기본 정보 확인**:
   - `DataFrame > Data Info`로 데이터 구조 확인.
   - 컬럼: 5개, 행: 150개, 결측값 없음.
   - 생성된 코드:
     ```python
     df_iris.info()
     ```

3. **통계 요약**:
   - `DataFrame > Describe`로 숫자형 컬럼의 통계 확인.
   - 예: `petal_length`의 평균, 표준편차 등.
   - 생성된 코드:
     ```python
     df_iris.describe()
     ```

4. **그룹별 분석**:
   - `DataFrame > Groupby`로 `species`별 평균 계산.
   - 예: `species`별 `sepal_length` 평균.
   - 생성된 코드:
     ```python
     df_iris.groupby('species').mean()
     ```

5. **시각화**:
   - `Visualization > Seaborn > Scatter`로 산점도 생성.
   - X축: `sepal_length`, Y축: `petal_length`, 색상: `species`.
   - 생성된 코드:
     ```python
     sns.scatterplot(x='sepal_length', y='petal_length', hue='species', data=df_iris)
     plt.show()
     ```

#### 결과
- Setosa는 `petal_length`가 짧고, Virginica는 길다.
- 산점도에서 품종 간 명확한 클러스터링 확인.

---

### 2. Titanic 데이터 분석

#### 목표
- Titanic 데이터셋을 분석해 생존율과 관련된 요인을 탐색합니다.

#### 데이터셋 개요
- **설명**: 타이타닉 승객의 생존 여부와 관련 정보 포함.
- **컬럼**: `survived`, `pclass`, `sex`, `age`, `fare`, `embarked` 등.
- **출처**: `seaborn.load_dataset('titanic')`.

#### 단계별 분석
1. **데이터 불러오기**:
   - `DataFrame > Import Data`에서 `titanic` 선택.
   - 생성된 코드:
     ```python
     df_titanic = sns.load_dataset('titanic')
     ```

2. **결측값 처리**:
   - `DataFrame > Data Info`로 결측값 확인(`age`, `embarked` 등).
   - `DataFrame > Fill NA`로 `age` 결측값을 평균으로 대체.
   - 생성된 코드:
     ```python
     df_titanic['age'] = df_titanic['age'].fillna(df_titanic['age'].mean())
     ```

3. **생존율 분석**:
   - `DataFrame > Groupby`로 `sex`별 `survived` 평균 계산.
   - 생성된 코드:
     ```python
     df_titanic.groupby('sex')['survived'].mean()
     ```

4. **시각화**:
   - `Visualization > Seaborn > Barplot`으로 `pclass`별 생존율 시각화.
   - X축: `pclass`, Y축: `survived`, 색상: `sex`.
   - 생성된 코드:
     ```python
     sns.barplot(x='pclass', y='survived', hue='sex', data=df_titanic)
     plt.show()
     ```

#### 결과
- 여성의 생존율이 남성보다 높다(예: 0.74 vs. 0.19).
- 1등석 승객의 생존율이 높다.

---

### 3. 카페 판매 데이터 분석

#### 목표
- 가상의 카페 판매 데이터를 분석해 인기 메뉴와 매출 패턴을 파악합니다.

#### 데이터셋 개요
- **설명**: 카페의 일별 판매 기록(가정).
- **컬럼**: `date`, `item`, `category`, `price`, `quantity`.
- **데이터 예시**:
  ```
  date,item,category,price,quantity
  2025-01-01,Americano,Coffee,4.5,10
  2025-01-01,Latte,Coffee,5.0,8
  2025-01-02,Croissant,Bakery,3.0,5
  ```

#### 단계별 분석
1. **데이터 불러오기**:
   - `DataFrame > Import Data`로 CSV 파일(`cafe_sales.csv`) 업로드.
   - 생성된 코드:
     ```python
     df_cafe = pd.read_csv('cafe_sales.csv')
     ```

2. **매출 계산**:
   - `DataFrame > Apply Function`으로 매출 열 추가(`price * quantity`).
   - 생성된 코드:
     ```python
     df_cafe['revenue'] = df_cafe['price'] * df_cafe['quantity']
     ```

3. **인기 메뉴 분석**:
   - `DataFrame > Groupby`로 `item`별 `quantity` 합계 계산.
   - 생성된 코드:
     ```python
     df_cafe.groupby('item')['quantity'].sum()
     ```

4. **시각화**:
   - `Visualization > Pandas Plot > Bar`로 카테고리별 매출 합계.
   - X축: `category`, Y축: `revenue`.
   - 생성된 코드:
     ```python
     df_cafe.groupby('category')['revenue'].sum().plot(kind='bar', title='Revenue by Category')
     ```

#### 결과
- Americano가 가장 많이 팔림(예: 100잔).
- Coffee 카테고리의 매출이 Bakery보다 높다.

---

### 4. 세탁기 센서 데이터 분석

#### 목표
- 가상의 세탁기 센서 데이터를 분석해 이상 작동 패턴을 탐지합니다.

#### 데이터셋 개요
- **설명**: 세탁기의 시간별 센서 데이터(가정).
- **컬럼**: `timestamp`, `vibration`, `temperature`, `status`.
- **데이터 예시**:
  ```
  timestamp,vibration,temperature,status
  2025-04-01 10:00,0.5,30,Normal
  2025-04-01 10:01,2.0,35,Warning
  2025-04-01 10:02,0.6,31,Normal
  ```

#### 단계별 분석
1. **데이터 불러오기**:
   - `DataFrame > Import Data`로 CSV 파일(`washer_sensor.csv`) 업로드.
   - 생성된 코드:
     ```python
     df_washer = pd.read_csv('washer_sensor.csv')
     ```

2. **이상치 탐지**:
   - `DataFrame > Filter Data`로 `vibration > 1.5` 또는 `temperature > 34` 필터링.
   - 생성된 코드:
     ```python
     df_anomaly = df_washer[(df_washer['vibration'] > 1.5) | (df_washer['temperature'] > 34)]
     ```

3. **시간별 패턴 분석**:
   - `DataFrame > Groupby`로 `status`별 `vibration` 평균 계산.
   - 생성된 코드:
     ```python
     df_washer.groupby('status')['vibration'].mean()
     ```

4. **시각화**:
   - `Visualization > Matplotlib > Line`으로 시간별 `vibration` 변화.
   - X축: `timestamp`, Y축: `vibration`.
   - 생성된 코드:
     ```python
     plt.plot(df_washer['timestamp'], df_washer['vibration'])
     plt.xlabel('Time')
     plt.ylabel('Vibration')
     plt.title('Vibration Over Time')
     plt.show()
     ```

#### 결과
- `Warning` 상태에서 `vibration` 평균이 높다(예: 2.0 vs. Normal 0.5).
- 라인 플롯에서 이상치(높은 진동) 시점 확인.

---

### 강의 마무리

- **요약**:
  - Iris: 품종별 꽃잎/꽃받침 특성 분석, 클러스터링 확인.
  - Titanic: 성별/등급별 생존율 분석, 여성/1등석 우세.
  - 카페 판매: 인기 메뉴와 카테고리별 매출 파악.
  - 세탁기 센서: 이상치 탐지와 시간별 패턴 분석.

- **활용 팁**:
  - Visual Python GUI로 생성된 코드를 저장해 재사용하세요.
  - 각 데이터셋의 특성에 맞는 시각화와 그룹핑을 선택하세요.

- **추가 학습**:
  - Visual Python의 `Visualization` 메뉴로 더 다양한 플롯(예: Heatmap) 시도.
  - 공식 문서(visualpython.ai)에서 고급 분석 사례 학습.