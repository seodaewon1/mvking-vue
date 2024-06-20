# MVKING 프로젝트

Vue.js, Swiper, The Movie Database(TMDB) api를 사용하여 만든 영화사이트입니다. 저희 MVKING에서는 최신 영화 순, 인기영화 순, 평점 높은 영화 순, 개봉 예정 영화를 확인 할 수 있으며 영화 개요, 평점, 인기도, 개봉일, 장르 등을 확인할 수 있습니다.

## 사이트 기능

[메인] - 최신영화, 인기영화, 개봉 영화 예정
[검색] - TMDB를 이용한 영화 데이터로 원하는 영화 검색 기능
[상세정보] - 영화 장르, 배우, 개봉일, 티저영상

## 디자인

[메인] -
![img](main1.png)  
![img](main2.png)  
![img](main3.png)

[상세정보] -
![img](info.png)  
![img](info1.png)

[검색] -
![img](search.png)

## 사용 방법

1. 서버를 실행합니다:

   ```bash
   npm run dev
   ```

## 빌드 방법

1. firebase에 로그인합니다.

   ```
   firebase login
   ```

2. 파일들을 빌드합니다.

   ```
   npm run build
   ```

3. 파일을 배포합니다.
   ```
   firebase deploy
   ```
