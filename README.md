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

## 설치 방법

1. 저장소를 클론합니다:

   ```bash
   git clone https://github.com/your-username/mvKing-vue.git
   ```

2. 프로젝트 디렉토리로 이동합니다:

   ```bash
   cd mvKing-vue
   ```

3. 필요한 종속성을 설치합니다:

   ```bash
   npm install
   ```

4. 프로젝트 루트 디렉토리에 `.env` 파일을 생성하고, TMDb API 키를 추가합니다:

   ```plaintext
   VITE_TMDB_API_KEY=your_tmdb_api_key
   ```

## 사용 방법

1. 개발 서버를 시작합니다:

   ```bash
   npm run dev
   ```

2. 브라우저에서 `http://localhost:3000`을 엽니다.

## 빌드 방법

프로덕션용으로 프로젝트를 빌드하려면:

```bash
npm run build
```
