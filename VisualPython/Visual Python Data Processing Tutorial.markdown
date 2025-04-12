# Visual Python을 활용한 데이터 처리 강의자료

## 데이터 처리 1

이 강의자료는 Visual Python 패키지를 사용하여 데이터 처리를 배우는 초보자를 위한 내용입니다. Visual Python의 GUI 인터페이스를 활용해 코드 작성 없이 데이터 분석 작업을 수행하는 방법을 다룹니다. Jupyter Notebook 환경을 기준으로 설명합니다.

---

### 1. 패키지 인스톨 및 임포트

#### 목표
- Visual Python 패키지를 설치하고 Jupyter Notebook에서 활성화합니다.
- 데이터 분석에 필요한 기본 패키지(Pandas, NumPy 등)를 임포트합니다.

#### 단계별 설명
1. **패키지 설치**:
   - Jupyter Notebook에서 터미널을 열거나 셀에 다음 명령어를 입력하여 설치합니다.
     ```bash
     !pip install jupyterlab-visualpython
     ```
   - 설치 후 Jupyter Notebook을 재시작합니다.

2. **Visual Python 활성화**:
   - Jupyter Notebook 상단 또는 사이드바에서 주황색 Visual Python 버튼을 클릭하여 GUI 인터페이스를 엽니다.
   - Visual Python이 자동으로 Pandas, NumPy 등 필수 패키지를 임포트합니다.

3. **패키지 확인**:
   - Visual Python GUI에서 `Package Manager` 메뉴를 열어 설치된 패키지 목록을 확인합니다.
   - 필요 시 추가 패키지(Matplotlib, Seaborn 등)를 GUI로 설치 가능합니다.

#### 결과
- Visual Python이 활성화되면 GUI 창이 열리고, 데이터 분석 작업을 시작할 준비가 완료됩니다.

---

### 2. 파일 입출력

#### 목표
- CSV 파일을 불러오고 저장하는 방법을 학습합니다.

#### 단계별 설명
1. **파일 불러오기**:
   - Visual Python GUI에서 `DataFrame > Import Data` 메뉴를 선택합니다.
   - `File Upload` 버튼을 클릭하여 로컬 CSV 파일(예: `sample_data.csv`)을 선택합니다.
   - 파일을 불러오면 Visual Python이 자동으로 Pandas 데이터프레임으로 변환하고 변수(예: `df`)를 생성합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df = pd.read_csv('sample_data.csv')
     ```

2. **파일 저장하기**:
   - 수정된 데이터를 저장하려면 `DataFrame > Export Data` 메뉴를 선택합니다.
   - 파일 이름(예: `output_data.csv`)을 입력하고 저장 경로를 지정합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df.to_csv('output_data.csv', index=False)
     ```

#### 예시 데이터
- `sample_data.csv` 예시:
  ```
  Name,Age,Score
  Alice,25,90
  Bob,30,85
  Charlie,22,95
  ```

#### 결과
- CSV 파일이 데이터프레임으로 불러와지고, 수정 후 새로운 CSV 파일로 저장됩니다.

---

### 3. 데이터 기본 정보 살펴보기

#### 목표
- 데이터프레임의 구조와 기본 통계 정보를 확인합니다.

#### 단계별 설명
1. **데이터프레임 정보 확인**:
   - Visual Python GUI에서 `DataFrame > Data Info` 메뉴를 선택합니다.
   - 데이터프레임(`df`)을 선택하면 열 이름, 데이터 타입, 결측값 여부 등이 표시됩니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df.info()
     ```

2. **기본 통계 요약**:
   - `DataFrame > Describe` 메뉴를 선택합니다.
   - 숫자형 열의 평균, 표준편차, 최소값, 최대값 등을 확인합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df.describe()
     ```

3. **데이터 미리보기**:
   - `DataFrame > Head/Tail` 메뉴를 선택하여 상위 5개 또는 하위 5개 행을 확인합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df.head()
     ```

#### 결과
- 예시 데이터의 경우:
  - `df.info()`: `Name`(object), `Age`(int), `Score`(int) 열 확인.
  - `df.describe()`: `Age`와 `Score`의 평균, 최소값, 최대값 등 통계 정보 출력.
  - `df.head()`: 첫 5행 데이터 표시.

---

### 4. 데이터 내용 수정/삭제/추가

#### 목표
- 데이터프레임의 값을 수정, 열/행 삭제, 새로운 데이터 추가를 학습합니다.

#### 단계별 설명
1. **데이터 수정**:
   - `DataFrame > Edit Data` 메뉴를 선택합니다.
   - 특정 열(예: `Score`)과 조건(예: `Name == 'Alice'`)을 선택하여 값을 변경(예: 90 → 100)합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df.loc[df['Name'] == 'Alice', 'Score'] = 100
     ```

2. **열 삭제**:
   - `DataFrame > Drop Column` 메뉴를 선택합니다.
   - 삭제할 열(예: `Age`)을 선택합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df = df.drop('Age', axis=1)
     ```

3. **행 삭제**:
   - `DataFrame > Drop Row` 메뉴를 선택합니다.
   - 조건(예: `Score < 90`)을 설정하여 행을 삭제합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df = df[df['Score'] >= 90]
     ```

4. **데이터 추가**:
   - **열 추가**:
     - `DataFrame > Add Column` 메뉴를 선택합니다.
     - 새 열 이름(예: `Grade`)과 값(예: `Score` 기준으로 A, B 등)을 입력합니다.
     - 생성된 코드는 다음과 유사합니다:
       ```python
       df['Grade'] = df['Score'].apply(lambda x: 'A' if x >= 90 else 'B')
       ```
   - **행 추가**:
     - `DataFrame > Append Row` 메뉴를 선택합니다.
     - 새 행 데이터(예: `Name: David, Score: 88`)를 입력합니다.
     - 생성된 코드는 다음과 유사합니다:
       ```python
       df = df.append({'Name': 'David', 'Score': 88}, ignore_index=True)
       ```

#### 결과
- 수정: `Alice`의 `Score`가 100으로 변경.
- 삭제: `Age` 열 또는 `Score < 90`인 행 제거.
- 추가: `Grade` 열 추가, `David` 행 추가.

---

### 5. 데이터 필터링(조건문 이용)

#### 목표
- 조건문을 활용해 데이터프레임에서 원하는 데이터를 추출합니다.

#### 단계별 설명
1. **단일 조건 필터링**:
   - Visual Python GUI에서 `DataFrame > Filter Data` 메뉴를 선택합니다.
   - 조건(예: `Score >= 90`)을 설정하고 데이터프레임(`df`)을 선택합니다.
   - 결과는 새 데이터프레임(예: `df_filtered`)으로 저장됩니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df_filtered = df[df['Score'] >= 90]
     ```

2. **다중 조건 필터링**:
   - `Filter Data` 메뉴에서 추가 조건을 설정합니다.
   - 예: `Score >= 90` 그리고 `Name != 'Bob'`.
   - 조건을 `AND` 또는 `OR`로 연결합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df_filtered = df[(df['Score'] >= 90) & (df['Name'] != 'Bob')]
     ```

3. **필터링 결과 확인**:
   - `DataFrame > Head/Tail` 메뉴를 사용하여 필터링된 데이터프레임(`df_filtered`)을 확인합니다.

#### 결과
- 단일 조건: `Score >= 90`인 행만 추출 (예: `Alice`, `Charlie`).
- 다중 조건: `Score >= 90`이고 `Name != 'Bob'`인 행 추출 (예: `Alice`, `Charlie`).

---

### 강의 마무리

- **요약**:
  - Visual Python을 설치하고 GUI로 데이터 분석 환경을 설정했습니다.
  - CSV 파일을 불러오고 저장하는 기본 입출력을 수행했습니다.
  - 데이터프레임의 구조와 통계 정보를 확인했습니다.
  - 데이터를 수정, 삭제, 추가하여 원하는 형태로 가공했습니다.
  - 조건문을 활용해 데이터를 필터링했습니다.

- **활용 팁**:
  - Visual Python은 초보자가 Pandas와 Python 코드를 익히는 데 유용합니다.
  - GUI로 생성된 코드를 복사하여 직접 수정하면 코딩 실력을 향상시킬 수 있습니다.

- **추가 학습**:
  - Visual Python의 `Visualization` 메뉴를 활용해 데이터를 시각화해보세요.
  - 공식 문서(visualpython.ai)와 GitHub를 참고하여 고급 기능 학습.