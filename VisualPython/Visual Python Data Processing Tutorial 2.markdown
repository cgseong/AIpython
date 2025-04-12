# Visual Python을 활용한 데이터 처리 강의자료

## 데이터 처리 2

이 강의자료는 Visual Python 패키지를 사용하여 데이터 처리의 고급 기능을 배우는 초보자를 위한 내용입니다. Visual Python의 GUI 인터페이스를 활용해 코드 작성 없이 데이터 분석 작업을 수행하는 방법을 다룹니다. Jupyter Notebook 환경을 기준으로 설명하며, 데이터 처리 1에서 다룬 기본 내용을 이해하고 있다고 가정합니다.

---

### 1. 데이터 처리 기능(함수) 사용

#### 목표
- Visual Python의 GUI를 통해 데이터프레임에 함수를 적용하여 데이터를 처리합니다.

#### 단계별 설명
1. **기본 함수 적용**:
   - Visual Python GUI에서 `DataFrame > Apply Function` 메뉴를 선택합니다.
   - 데이터프레임(`df`)의 특정 열(예: `Score`)에 함수를 적용합니다.
   - 예: `Score` 값을 10% 증가시키기.
   - GUI에서 `Custom Function` 옵션을 선택하고 `lambda x: x * 1.1`을 입력합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df['Score'] = df['Score'].apply(lambda x: x * 1.1)
     ```

2. **복잡한 함수 적용**:
   - `Apply Function` 메뉴에서 다중 열을 활용한 함수를 정의합니다.
   - 예: `Age`와 `Score`를 사용해 새로운 열 `Performance` 생성.
   - GUI에서 `Custom Function`에 `lambda x: 'High' if x['Score'] > 90 and x['Age'] < 30 else 'Low'` 입력.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df['Performance'] = df.apply(lambda x: 'High' if x['Score'] > 90 and x['Age'] < 30 else 'Low', axis=1)
     ```

3. **결과 확인**:
   - `DataFrame > Head/Tail` 메뉴를 사용해 수정된 데이터프레임을 확인합니다.

#### 예시 데이터
- `sample_data.csv`:
  ```
  Name,Age,Score
  Alice,25,90
  Bob,30,85
  Charlie,22,95
  ```

#### 결과
- `Score` 열: 90 → 99, 85 → 93.5, 95 → 104.5.
- `Performance` 열: `Charlie` → `High`, `Alice`/`Bob` → `Low`.

---

### 2. 데이터 그룹핑 및 집계(Groupby)

#### 목표
- 데이터를 그룹화하고 집계 함수(예: 평균, 합계)를 적용합니다.

#### 단계별 설명
1. **단일 열 그룹핑**:
   - Visual Python GUI에서 `DataFrame > Groupby` 메뉴를 선택합니다.
   - 그룹핑 기준 열(예: `Age`)을 선택하고 집계 대상 열(예: `Score`)을 지정합니다.
   - 집계 함수로 `Mean`을 선택하여 연령별 평균 점수를 계산합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df_grouped = df.groupby('Age')['Score'].mean().reset_index()
     ```

2. **다중 열 그룹핑**:
   - `Groupby` 메뉴에서 여러 열(예: `Age`, `Performance`)을 그룹핑 기준으로 선택합니다.
   - 집계 함수로 `Sum`을 선택하여 그룹별 점수 합계를 계산합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df_grouped = df.groupby(['Age', 'Performance'])['Score'].sum().reset_index()
     ```

3. **결과 확인**:
   - `DataFrame > Head/Tail` 메뉴를 사용해 그룹핑 결과를 확인합니다.

#### 결과
- 단일 열 그룹핑: `Age`별 `Score` 평균 (예: Age 22 → 95, Age 25 → 90).
- 다중 열 그룹핑: `Age`와 `Performance`별 `Score` 합계.

---

### 3. 데이터 프레임 병합(Merge, Concat)

#### 목표
- 여러 데이터프레임을 병합하여 통합된 데이터를 생성합니다.

#### 단계별 설명
1. **Merge (조인)**:
   - Visual Python GUI에서 `DataFrame > Merge` 메뉴를 선택합니다.
   - 두 데이터프레임(`df1`, `df2`)을 선택하고 병합 기준 열(예: `Name`)을 지정합니다.
   - 병합 유형(예: `Inner`)을 선택합니다.
   - 예: `df1` (Name, Score), `df2` (Name, Grade)를 `Name` 기준으로 병합.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df_merged = pd.merge(df1, df2, on='Name', how='inner')
     ```

2. **Concat (연결)**:
   - `DataFrame > Concat` 메뉴를 선택합니다.
   - 데이터프레임(`df1`, `df2`)을 선택하고 연결 방향(예: `Vertical`)을 지정합니다.
   - 예: 동일 구조의 `df1`, `df2`를 수직으로 연결.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df_concat = pd.concat([df1, df2], axis=0, ignore_index=True)
     ```

3. **결과 확인**:
   - `DataFrame > Head/Tail` 메뉴로 병합된 데이터프레임을 확인합니다.

#### 예시 데이터
- `df1`:
  ```
  Name,Score
  Alice,90
  Bob,85
  ```
- `df2`:
  ```
  Name,Grade
  Alice,A
  Charlie,B
  ```

#### 결과
- Merge: `Name` 기준 Inner 조인 → `Alice`만 포함 (Score: 90, Grade: A).
- Concat: 수직 연결 → `df1`과 `df2`의 행이 결합.

---

### 4. 데이터 형태 변환(Pivot, Pivot_table, Melt)

#### 목표
- 데이터프레임의 구조를 변환하여 분석에 적합한 형태로 만듭니다.

#### 단계별 설명
1. **Pivot**:
   - Visual Python GUI에서 `DataFrame > Pivot` 메뉴를 선택합니다.
   - 인덱스(예: `Name`), 열(예: `Age`), 값(예: `Score`)을 지정합니다.
   - 예: `Name`을 인덱스로, `Age`를 열로, `Score`를 값으로 피벗.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df_pivot = df.pivot(index='Name', columns='Age', values='Score')
     ```

2. **Pivot_table**:
   - `DataFrame > Pivot Table` 메뉴를 선택합니다.
   - 인덱스(예: `Performance`), 열(예: `Age`), 값(예: `Score`), 집계 함수(예: `Mean`)을 지정합니다.
   - 예: `Performance`별 `Age`에 따른 `Score` 평균 계산.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df_pivot_table = pd.pivot_table(df, index='Performance', columns='Age', values='Score', aggfunc='mean')
     ```

3. **Melt**:
   - `DataFrame > Melt` 메뉴를 선택합니다.
   - ID 변수(예: `Name`)와 값 변수(예: `Score`, `Age`)를 지정하여 긴 형식으로 변환합니다.
   - 예: `Name`을 기준으로 `Score`, `Age`를 하나의 열로 변환.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df_melt = pd.melt(df, id_vars=['Name'], value_vars=['Score', 'Age'], var_name='Metric', value_name='Value')
     ```

4. **결과 확인**:
   - `DataFrame > Head/Tail` 메뉴로 변환된 데이터프레임을 확인합니다.

#### 결과
- Pivot: `Name` 행, `Age` 열, `Score` 값으로 구성된 테이블.
- Pivot_table: `Performance`별 `Age`에 따른 `Score` 평균 테이블.
- Melt: `Name`, `Metric`(Score/Age), `Value` 열로 구성된 긴 형식 데이터.

---

### 강의 마무리

- **요약**:
  - Visual Python의 GUI를 사용해 데이터프레임에 함수를 적용했습니다.
  - 데이터를 그룹화하고 집계하여 요약 정보를 생성했습니다.
  - 여러 데이터프레임을 병합하여 통합된 데이터를 만들었습니다.
  - 데이터 구조를 피벗, 피벗 테이블, 멜트로 변환했습니다.

- **활용 팁**:
  - GUI로 생성된 코드를 분석하여 Pandas의 동작 방식을 학습하세요.
  - 복잡한 변환 작업은 소규모 데이터로 테스트 후 적용하세요.

- **추가 학습**:
  - Visual Python의 `Visualization` 메뉴로 변환된 데이터를 시각화해보세요.
  - 공식 문서(visualpython.ai)와 GitHub에서 고급 예제를 참고하세요.