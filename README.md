# numpy-scipy
playing sklearn_wine_dataset with numpy&amp;scipy 


출처 - `SciPy and NumPy` - O'Reilly

### Numpy
- Numerical computing in python 
- 파이썬의 산술계산 할 때 사용하는 라이브러리
- np.array를 사용하면
	
    - 반복문을 사용하지 않고도 배열 연산이 가능하다 (25배 빠름)
    - 예를 들어 List의 경우 + 연산을 하면 concat이 되지만, np.array는 + 하면 요소끼리 연산 가능
    - broadcasting 으로 차원이 다른 배열도 연산이 가능하다. (원소별 연산)
    - 배열 크기가 동적으로 변한다. 
- `np.ndarray` > n차원 배열
- 따라서 이런 이유 때문에 빅데이터를 다루는 데이터분석에서는 Numpy를 활용한다. 
- 넘파이는 주로 행렬 및 관련 기초 연산을 할 때 사용한다.

### Scipy
- Scientific computing in Python
- 넘파이에서 제공하는 행렬에 기반한 수학, 과학 알고리즘을 지원하는 라이브러리
- 완전한 기능을 가진 FFT, 선형대수 알고리즘을 지원한다. (넘파이보다 속도 빠름)
- 적분, 상미분방정식, 특수함수, 최적화 등..
	
    - `scipy.fftpack` : Fast Fourier Transform 고속푸리에변환..파장 계산?
    - `scipy.linalg`  : determinant(행렬식), inverse, solve..


- scalar(1d)
	- 숫자 하나로 이루어진 데이터
- vector(2d)
	- 여러 숫자로 이루어진 데이터 레코드 (n,)
- matrix(2d)
	- 벡터가 여럿인 데이터 집합 (n,m)
- tensor(3d) 
	- 같은 크기의 행렬이 여러 개 (n,m,r)

### pearsonr, spearmanr 상관계수
`import scipy.stats as stats`

- `stats.pearsonr(x,y)`: 두 연속적인 변수의 상관관계를 구할때 사용. 두 변수간 선형적인 상관관계의 크기를 모수(parametric)인 방법으로 나타내는 값. 두 변수 모두 정규분포를 따른다는 가정(normal distribution). range(-1,1)
- `stats.spearmanr(x,y)` : 선형적인 상관관계가 아닌, 단순히 한 변수가 증가할 때 다른 변수도 증가하는지 관계만 나타내는 값. 
대표적인 비모수적(Non-parametric) 상관계수. 두 연속형 변수가 심하게 정규분포를 벗어난다거나 순위척도일때 사용함. 연속형 자료면 각 측정값을 순위 척도로 변환후 계산. 


### 카이제곱 검정, 정규 검정, T검정

- `chi2_contingency` (카이제곱 검정) : 두 변수 모두 카테고리형일때 사용하는 계수. 카테고리 분포의 모수에 대한 검정을 표본의 합을 이용할 수 없을때(스칼라가 아닌 벡터 값을 지닐때). 관찰된 빈도의 값이 기대한 빈도와 의미있게 다른가? 
	
    - 귀무가설) 관찰빈도는 기대빈도와 같다
    - 대립가설) 관찰빈도는 기대빈도와 다르다
    - pvalue가 유의수준 0.05보다 작으면 대립 선택

- `stats.norm()` 정규성 검정 : 회귀 분석에서는 확률 분포가 가우시안 정규분포를 따르는지, 아닌지 확인하는 것이 중요하다. 

- `stats.ttest_1samp()` 1 sample t-test 일표본 t검정 : 특정한 평균을 기준으로 해당 샘플의 평균이 같은지 검정. 예를 들면, 전국 중학교 학생들의 수학교 평균이 65점이라면 A중학교 수학 성적 평균이 72점일때 유의미하게 다른지 검정. 귀무가설, 둘이 같다. (차이가 없다.) 대립가설, 둘이 다르다. 차이가 있다. >> x가 평균 65점인 모집단에서 추출된 표본인지 검정
	
    - 만일 평균이 n보다 크다, 작다로 설정하여 검증하고 싶을 경우
    ```py
    t_stat, p_val = stats.ttest_1samp(x, 65, alternative='greater')
    ```
    작다고 설정하고 싶으면 'less'
- `stats.ttest_ind()` 2 sample t-test 이표본 t검정 : 2개의 표본의 평균이 같은지, 다른지 비교. alternative 옵션으로 단측검정, 양측검정할지 옵션 줄 수 있음. (독립표본 t검정)
독립표본 t검정을 하기 위해서는 평균, 등분산 여부, t-value, p-value를 확인해야 한다. 

- `stats.ttest_rel()` paired 2 sample t-test 대응 표본 검정: 순서별로 쌍을 이룬 데이터를 고려하여 ttest 검정.
	
