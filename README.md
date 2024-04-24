# Youtube Analysis Project
* Project Date: 2023/10/06 - 2023/10/29
* Project Goal: Analyze YouTube’s trending videos in detail to identify trends in each category
- Project responsibilities
    - Team Leader/Subtitle Crawling/Analyze general tendency/Report Writing

## Git 소개
- data : Dataframe with subtitle preprocessing and duplicate and music category removal
- files: 유튜브 프로젝트 보고서 및 발표 자료

## Data
![image](https://github.com/syl0702/yt_pjt/assets/140361641/a9f84eb1-ff6a-4d6f-8bf9-58620d79523c)


## Tech
<img src= "https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white">

## Workflow
![image](https://github.com/syl0702/yt_pjt/assets/140361641/67764c60-70e2-47ed-97fc-18d3f6e1b413)

## Target
- 인기 급상승 동영상 분석을 통한 트렌드 파악.
- 기업에게 유튜브 매개 마케팅 정보 제공 가능.
- 신규 유튜브 진입자에게 카테고리별 트렌드 기반으로 가이드라인 제공 가능.
- 사용자에게는 트렌딩 정보를 제공 가능.

### 데이터 전처리
- 자막 추출: 한국어가 있을 경우에는 한국어를 추출, 한국어 자막이 없을 경우 일본어나 영어가 있을 경우도 출력.
- 음성 추출:
      - PYDUB 패키지를 사용해 공백 단위로 chunk화 해 처리. (문장 단위로 처리)
      - 배경 소음이 많은 영상을 고려하여 잡음을 감안한 음성 처리를 했으나 결과는 뚜렷하게 좋지 않아 배경음을 처리하지 않은 모델로 작성.
- 토큰화 1 (형태소 추출):
      - KONLPY 패키지 사용. 그 중에서도 OKT 프로세스를 사용.
      - OKT, Komoran, Kkma를 통해 문장을 형태소 단위로 나누고 개별 요소들에 대해 pos를 통해 명사, 고유명사, 동사, 형용사를 남기는 방향으로 작성.
- 토큰화 2 (벡터라이징):
      - CountVectorizer, TF-IDFVectorizer 사용.
      - 추출된 값들에서 영상 주제 파악을 위해 언급량을 1로 표준화.

### 카테고리 Human Labeling
- 일부 카테고리가 영상의 주제와 무관하게 분류되어 있거나 동떨어진 카테고리에 들어가 있는 것을 확인해 이를 각 조원에 할당하여 확인을 시도함.
- 이 레이블링의 결과를 통해 전체적인 분석 시작.

### 처리 프로세스 정리
- 영상 제목, 더보기란, 자막에서 공통 전처리를 시도.

### 태그 칼럼
- string으로 이루어져 있던 태그를 리스트에 나열해 새로운 태그리스트 컬럼을 생성해 활용.

### 번역
- 개별 영상 단위의 자막 데이터가 번역기가 한번에 받아들일 수 있는 크기보다 컸기 때문에 문장 5개 단위로 쪼개서 google translator를 활용할 수 있는 코드를 이용.
- 번역하고 합쳐서 추출함.

## 데이터 분석 결과
- 카테고리 종류를 불문하고 영상의 총 재생 시간과 전체 뷰어쉽 수, 인기급상승동영상(이하 인급동) 기간 내의 조회수 추이는 큰 차이 없었음.

![image](https://github.com/syl0702/yt_pjt/assets/140361641/3af1209e-e3bd-4bae-9069-e059c7551dc2)
![image](https://github.com/syl0702/yt_pjt/assets/140361641/56b29dc7-2117-422d-ac2d-06433c4176d7)

- Entertainment에 국제적으로 압도적 인지도 및 조회수를 가진 유튜버 MrBeast가 있음을 확인 후 절사 평균 10%로 조회수 비교.
- Comedy와 Pets & Animals의 조회수 및 좋아요 수 가 매우 높은 것을 파악 --> 높은 관심도

![image](https://github.com/syl0702/yt_pjt/assets/140361641/f86e6826-62be-4346-85bd-af8c24756201)
- 그러나 조회수, 좋아요 수와 다르게 댓글 수는 뉴스 및 정치의 평균이 매우 큰 차이로 가장 높은 수치를 보임.
- 이 카테고리의 경우 댓글을 통해 관심도가 나타난다는 점을 파악 가능.

![image](https://github.com/syl0702/yt_pjt/assets/140361641/666ea63f-f0db-4290-b2d7-983f103ae642)
- 요일별로 분석했을 때, 전체적으로 업로드 요일이 고르게 분포함.
- 큰 차이는 없지만 목요일에 미세하게 더 업로드를 자주 하는 것으로 보이고 토요일에는 상대적으로 업로드를 덜하는 것으로 보인다.

![image](https://github.com/syl0702/yt_pjt/assets/140361641/d405320a-a3e0-4469-8e72-0a6497270a53)
- 오전 시간대에 업로드되는 영상이 가장 많다.
- 차이가 크지만 오후 12시가 두 번째로 선호되는 시간대.
- 사람들이 일과를 시작하거나 식사하는 시간대에 영상 업로드가 이루어짐을 파악 가능.

![image](https://github.com/syl0702/yt_pjt/assets/140361641/85a3d4ca-d818-4715-8bc1-95c002557ee1)
- heatmap에서 좋아요 수, 조회수, 댓글 수는 서로 매우 높은 상관 관계를 보여주었으나 그 외의 항목은 유의미한 결과를 보여주지 못함.
- 태그의 길이가 다양해 유의미한 조회수와의 관계성을 기대했으나 관계성이 낮은 것으로 파악된다.



