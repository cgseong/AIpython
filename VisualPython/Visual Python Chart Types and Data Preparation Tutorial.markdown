# Visual Python을 활용한 차트 종류 및 특징 강의자료

## 차트 종류 및 특징 설명

이 강의자료는 Visual Python 패키지를 사용하여 다양한 차트의 종류와 특징, 그리고 각 차트에 필요한 데이터 처리 양식을 배우는 초보자를 위한 내용입니다. Visual Python의 GUI 인터페이스를 활용해 코드 작성 없이 차트를 생성하며, Jupyter Notebook 환경을 기준으로 설명합니다. 데이터 처리 및 시각화 기초를 이해하고 있다고 가정합니다.

---

### 1. Scatter Plot (산점도)

#### 특징
- **용도**: 두 변수 간의 관계(예: 상관관계)를 시각화.
- **장점**: 데이터 포인트의 분포와 패턴(클러스터링, 이상치 등)을 쉽게 파악 가능.
- **단점**: 데이터가 많을 경우 포인트 겹침으로 가독성 저하.
- **적합 사례**: 연속형 변수(예: 나이 vs. 점수) 비교, 상관관계 분석.

#### 필요 데이터 처리 양식
- **형태**: 두 개의 연속형 변수(X축, Y축)로 구성된 데이터프레임.
- **컬럼 요구사항**:
  - X축: 숫자형(예: `Age`).
  - Y축: 숫자형(예: `Score`).
  - 선택 사항: 색상, 크기, 마커 스타일을 위한 추가 변수.
- **데이터 예시**:
  ```
  Name,Age,Score
  Alice,25,90
  Bob,30,85
  Charlie,22,95
  ```
- **처리 작업**:
  - 결측값 제거: `df = df.dropna()`.
  - 숫자형 데이터 확인: `df['Age'].dtype` 및 `df['Score'].dtype`이 float/int인지 확인.
  - 이상치 처리: 예: `df = df[df['Score'].between(0, 100)]`.

#### Visual Python 사용법
1. GUI에서 `Visualization > Matplotlib` 또는 `Seaborn` 메뉴를 선택.
2. 플롯 유형으로 `Scatter` 선택.
3. 데이터프레임(`df`), X축(예: `Age`), Y축(예: `Score`) 지정.
4. 옵션: 색상(예: `blue`), 마커 크기(예: 50) 설정.
5. 생성된 코드는 다음과 유사:
   ```python
   import matplotlib.pyplot as plt
   plt.scatter(df['Age'], df['Score'], color='blue', s=50)
   plt.xlabel('Age')
   plt.ylabel('Score')
   plt.title('Age vs Score')
   plt.show()
   ```

#### 결과
- `Age`와 `Score`의 관계를 점으로 표시, 각 점은 학생 한 명을 나타냄.

---

### 2. Line Plot (라인 플롯)

#### 특징
- **용도**: 시간 또는 순서에 따른 데이터 변화(트렌드)를 시각화.
- **장점**: 연속적인 변화(예: 시간 경과에 따른 점수 변화)를 명확히 보여줌.
- **단점**: 비연속 데이터나 범주형 데이터에는 부적합.
- **적합 사례**: 시계열 데이터(예: 월별 판매량), 연속형 변수 추이.

#### 필요 데이터 처리 양식
- **형태**: X축(시간/순서)과 Y축(값)으로 구성된 데이터프레임.
- **컬럼 요구사항**:
  - X축: 시간형(예: `Date`) 또는 순서형(예: `Month`) 데이터.
  - Y축: 숫자형(예: `Sales`).
  - 선택 사항: 여러 라인을 위한 그룹 변수(예: `Category`).
- **데이터 예시**:
  ```
  Month,Sales
  Jan,100
  Feb,120
  Mar,110
  ```
- **처리 작업**:
  - 시간 데이터 정렬: `df = df.sort_values('Month')`.
  - 결측값 보간 또는 제거: `df = df.interpolate()` 또는 `df = df.dropna()`.
  - 데이터 타입 확인: `Sales`가 숫자형인지 확인.

#### Visual Python 사용법
1. GUI에서 `Visualization > Pandas Plot` 또는 `Matplotlib` 메뉴 선택.
2. 플롯 유형으로 `Line` 선택.
3. 데이터프레임(`df`), X축(예: `Month`), Y축(예: `Sales`) 지정.
4. 옵션: 제목(예: "Monthly Sales Trend"), 그리드 추가.
5. 생성된 코드는 다음과 유사:
   ```python
   df.plot(x='Month', y='Sales', kind='line', title='Monthly Sales Trend', grid=True)
   ```

#### 결과
- `Month`에 따른 `Sales` 변화를 선으로 표시, 트렌드 명확히 확인.

---

### 3. Bar Plot (막대 플롯)

#### 특징
- **용도**: 범주형 데이터 간 비교(예: 그룹별 합계/평균).
- **장점**: 범주별 차이를 직관적으로 보여줌.
- **단점**: 범주가 너무 많으면 가독성 저하.
- **적합 사례**: 그룹별 통계(예: 학생별 점수, 지역별 인구).

#### 필요 데이터 처리 양식
- **형태**: 범주형 X축과 숫자형 Y축으로 구성된 데이터프레임.
- **컬럼 요구사항**:
  - X축: 범주형(예: `Name`).
  - Y축: 숫자형(예: `Score` 또는 집계된 값).
  - 선택 사항: 색상 구분을 위한 그룹 변수.
- **데이터 예시**:
  ```
  Name,Score
  Alice,90
  Bob,85
  Charlie,95
  ```
- **처리 작업**:
  - 집계(필요 시): `df = df.groupby('Name')['Score'].sum().reset_index()`.
  - 결측값 제거: `df = df.dropna()`.
  - 범주형 데이터 정리: 중복 제거 또는 범주 순서 지정.

#### Visual Python 사용법
1. GUI에서 `Visualization > Pandas Plot` 또는 `Seaborn` 메뉴 선택.
2. 플롯 유형으로 `Bar` 선택.
3. 데이터프레임(`df`), X축(예: `Name`), Y축(예: `Score`) 지정.
4. 옵션: 색상(예: `skyblue`), 제목(예: "Scores by Name") 설정.
5. 생성된 코드는 다음과 유사:
   ```python
   df.plot(x='Name', y='Score', kind='bar', color='skyblue', title='Scores by Name')
   ```

#### 결과
- `Name`별 `Score`를 막대 그래프로 표시, 각 막대는 학생별 점수 비교.

---

### 4. 기타 차트 (Box Plot, Histogram)

#### Box Plot (박스 플롯)
- **특징**:
  - **용도**: 데이터 분포(중앙값, 사분위, 이상치) 시각화.
  - **장점**: 분포 특성과 이상치 식별에 유용.
  - **단점**: 세부 데이터 포인트 확인 어려움.
  - **적합 사례**: 그룹별 분포 비교(예: 반별 점수 분포).
- **데이터 처리 양식**:
  - 숫자형 열(예: `Score`)과 선택적 그룹 변수(예: `Class`).
  - 결측값 제거, 숫자형 데이터 확인.
  - 예: `df = df.dropna(subset=['Score'])`.
- **Visual Python 사용법**:
  - `Visualization > Seaborn > Boxplot`.
  - X축(예: `Class`), Y축(예: `Score`) 지정.
  - 생성된 코드:
    ```python
    import seaborn as sns
    sns.boxplot(x='Class', y='Score', data=df)
    plt.show()
    ```

#### Histogram (히스토그램)
- **특징**:
  - **용도**: 연속형 데이터의 분포 확인.
  - **장점**: 빈도 분포를 직관적으로 보여줌.
  - **단점**: 빈 크기에 따라 결과 달라질 수 있음.
  - **적합 사례**: 값의 빈도 분석(예: 점수 분포).
- **데이터 처리 양식**:
  - 단일 숫자형 열(예: `Score`).
  - 결측값 제거, 이상치 처리.
  - 예: `df = df[df['Score'].between(0, 100)]`.
- **Visual Python 사용법**:
  - `Visualization > Matplotlib > Histogram`.
  - 열(예: `Score`), 빈 개수(예: 10) 지정.
  - 생성된 코드:
    ```python
    import matplotlib.pyplot as plt
    plt.hist(df['Score'], bins=10)
    plt.xlabel('Score')
    plt.ylabel('Frequency')
    plt.show()
    ```

---

### 강의 마무리

- **요약**:
  - Scatter Plot: 두 변수의 관계를 점으로 표시, 연속형 데이터에 적합.
  - Line Plot: 시간/순서에 따른 변화를 선으로 표시, 시계열 데이터에 유용.
  - Bar Plot: 범주별 값을 막대로 비교, 범주형 데이터에 적합.
  - Box Plot과 Histogram: 분포와 빈도 분석에 활용.
  - 각 차트에 필요한 데이터 형태와 전처리 방법을 학습함.

- **활용 팁**:
  - 데이터 특성(연속형/범주형, 분포 등)에 따라 적합한 차트를 선택하세요.
  - Visual Python GUI로 생성된 코드를 분석해 커스터마이징 방법을 익히세요.

- **추가 학습**:
  - Visual Python의 `Visualization` 메뉴에서 Pie Chart, Area Plot 등 다른 차트 탐색.
  - 공식 문서(visualpython.ai)와 Matplotlib/Seaborn 갤러리 참고.