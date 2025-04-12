# Visual Python을 활용한 시각화 강의자료

## 시각화 패키지

이 강의자료는 Visual Python 패키지를 사용하여 데이터 시각화를 배우는 초보자를 위한 내용입니다. Visual Python의 GUI 인터페이스를 활용해 Pandas Plot, Matplotlib, Seaborn을 이용한 시각화를 코드 작성 없이 수행하는 방법을 다룹니다. Jupyter Notebook 환경을 기준으로 설명하며, 이전 데이터 처리 강의 내용을 이해하고 있다고 가정합니다.

---

### 1. Pandas Plot

#### 목표
- Pandas의 내장 플롯 기능을 사용해 간단한 데이터 시각화를 생성합니다.

#### 단계별 설명
1. **기본 라인 플롯**:
   - Visual Python GUI에서 `Visualization > Pandas Plot` 메뉴를 선택합니다.
   - 데이터프레임(`df`)과 플롯 유형으로 `Line`을 선택합니다.
   - X축(예: `Age`), Y축(예: `Score`)을 지정합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df.plot(x='Age', y='Score', kind='line')
     ```

2. **막대 플롯**:
   - `Pandas Plot` 메뉴에서 플롯 유형으로 `Bar`를 선택합니다.
   - X축(예: `Name`), Y축(예: `Score`)을 지정합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df.plot(x='Name', y='Score', kind='bar')
     ```

3. **옵션 추가**:
   - GUI에서 `Title`(예: "Score by Name"), `Grid`(체크), `Legend`(체크)를 설정합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     df.plot(x='Name', y='Score', kind='bar', title='Score by Name', grid=True)
     ```

4. **결과 확인**:
   - 플롯은 Jupyter Notebook 셀 출력으로 표시됩니다.

#### 예시 데이터
- `sample_data.csv`:
  ```
  Name,Age,Score
  Alice,25,90
  Bob,30,85
  Charlie,22,95
  ```

#### 결과
- 라인 플롯: `Age`에 따른 `Score` 변화를 선으로 표시.
- 막대 플롯: `Name`별 `Score`를 막대 그래프로 표시, 제목과 그리드 포함.

---

### 2. Matplotlib

#### 목표
- Matplotlib을 사용해 다양한 플롯을 생성하고 커스터마이징합니다.

#### 단계별 설명
1. **산점도(Scatter Plot)**:
   - Visual Python GUI에서 `Visualization > Matplotlib` 메뉴를 선택합니다.
   - 플롯 유형으로 `Scatter`를 선택하고 데이터프레임(`df`)을 지정합니다.
   - X축(예: `Age`), Y축(예: `Score`), 색상(예: `blue`)을 설정합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     import matplotlib.pyplot as plt
     plt.scatter(df['Age'], df['Score'], color='blue')
     plt.xlabel('Age')
     plt.ylabel('Score')
     plt.show()
     ```

2. **히스토그램**:
   - `Matplotlib` 메뉴에서 플롯 유형으로 `Histogram`을 선택합니다.
   - 열(예: `Score`)과 빈 개수(예: 5)를 지정합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     plt.hist(df['Score'], bins=5)
     plt.xlabel('Score')
     plt.ylabel('Frequency')
     plt.show()
     ```

3. **옵션 추가**:
   - GUI에서 제목(예: "Score Distribution"), 레이블, 그리드, 범례 등을 설정합니다.
   - 예: 히스토그램에 제목과 그리드 추가.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     plt.hist(df['Score'], bins=5)
     plt.title('Score Distribution')
     plt.xlabel('Score')
     plt.ylabel('Frequency')
     plt.grid(True)
     plt.show()
     ```

4. **결과 확인**:
   - 플롯은 Jupyter Notebook 셀 출력으로 표시됩니다.

#### 결과
- 산점도: `Age`와 `Score`의 관계를 점으로 표시.
- 히스토그램: `Score`의 분포를 5개 구간으로 표시, 제목과 그리드 포함.

---

### 3. Seaborn

#### 목표
- Seaborn을 사용해 통계적이고 세련된 시각화를 생성합니다.

#### 단계별 설명
1. **박스 플롯(Box Plot)**:
   - Visual Python GUI에서 `Visualization > Seaborn` 메뉴를 선택합니다.
   - 플롯 유형으로 `Boxplot`을 선택하고 데이터프레임(`df`)을 지정합니다.
   - X축(예: `Name`), Y축(예: `Score`)을 설정합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     import seaborn as sns
     sns.boxplot(x='Name', y='Score', data=df)
     plt.show()
     ```

2. **히트맵(Heatmap)**:
   - `Seaborn` 메뉴에서 플롯 유형으로 `Heatmap`을 선택합니다.
   - 데이터프레임의 상관관계 행렬을 계산하도록 설정합니다.
   - GUI에서 `Correlation` 옵션을 체크하고 숫자형 열(예: `Age`, `Score`)을 선택합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     sns.heatmap(df[['Age', 'Score']].corr(), annot=True)
     plt.show()
     ```

3. **옵션 추가**:
   - GUI에서 색상 팔레트(예: `coolwarm` for Heatmap), 제목(예: "Correlation Matrix"), 숫자 표시(Heatmap의 `annot=True`) 등을 설정합니다.
   - 생성된 코드는 다음과 유사합니다:
     ```python
     sns.heatmap(df[['Age', 'Score']].corr(), annot=True, cmap='coolwarm')
     plt.title('Correlation Matrix')
     plt.show()
     ```

4. **결과 확인**:
   - 플롯은 Jupyter Notebook 셀 출력으로 표시됩니다.

#### 결과
- 박스 플롯: `Name`별 `Score`의 분포를 상자 그림으로 표시.
- 히트맵: `Age`와 `Score`의 상관관계를 색상으로 표시, 상관계수 숫자 포함.

---

### 강의 마무리

- **요약**:
  - Pandas Plot을 사용해 간단한 라인과 막대 플롯을 생성했습니다.
  - Matplotlib으로 산점도와 히스토그램을 커스터마이징했습니다.
  - Seaborn을 활용해 통계적 박스 플롯과 히트맵을 생성했습니다.

- **활용 팁**:
  - Visual Python의 GUI로 생성된 코드를 복사하여 Matplotlib이나 Seaborn의 고급 기능을 학습하세요.
  - 시각화 결과를 비교하여 데이터 특성에 맞는 플롯 유형을 선택하세요.

- **추가 학습**:
  - Visual Python의 `Seaborn` 메뉴에서 `Pairplot`, `Violinplot` 등 다른 플롯을 탐색해보세요.
  - 공식 문서(visualpython.ai)와 Seaborn 갤러리를 참고하여 다양한 시각화 스타일 학습.