<script setup>
import { useRouter } from 'vue-router'
import HeaderSection from '@/components/HeaderSection.vue'
import FooterSection from '@/components/FooterSection.vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import 'swiper/swiper-bundle.css'
import { Navigation, Pagination, Autoplay } from 'swiper/modules'
import { onMounted, ref } from 'vue'
import axios from 'axios'

const router = useRouter()

const nowPlayingMovies = ref([])
const popularMovies = ref([])
const topRatedMovies = ref([])
const upcomingMovies = ref([])
const apikey = '9fd9ecd1406306cca1771dc03b2fd6ac'

const fetchMovies = async () => {
  try {
    const latestResponse = await axios.get(
      `https://api.themoviedb.org/3/movie/now_playing?api_key=${apikey}&page=1`
    )
    nowPlayingMovies.value = latestResponse.data.results
    console.log('Now Playing:', latestResponse)
  } catch (error) {
    console.log(error)
  }

  try {
    const popularResponse = await axios.get(
      `https://api.themoviedb.org/3/movie/popular?api_key=${apikey}&page=1`
    )
    popularMovies.value = popularResponse.data.results
    console.log('Popular:', popularResponse)
  } catch (error) {
    console.log(error)
  }

  try {
    const topRatedResponse = await axios.get(
      `https://api.themoviedb.org/3/movie/top_rated?api_key=${apikey}&page=1`
    )
    topRatedMovies.value = topRatedResponse.data.results
    console.log('Top Rated:', topRatedResponse)
  } catch (error) {
    console.log(error)
  }
  try {
    const upcomingResponse = await axios.get(
      `https://api.themoviedb.org/3/movie/upcoming?api_key=${apikey}&page=1`
    )
    upcomingMovies.value = upcomingResponse.data.results
    console.log('Top upcoming:', upcomingResponse)
  } catch (error) {
    console.log(error)
  }
}

const goToDetail = (movieID) => {
  router.push({ name: 'detail', params: { movieID } })
}

onMounted(fetchMovies)
</script>

<template>
  <HeaderSection />
  <main id="main" role="main">
    <div class="banner">
      <Swiper
        :slides-per-view="1"
        :space-between="10"
        :loop="true"
        :autoplay="{ delay: 4000, disableOnInteraction: false }"
        :pagination="{ clickable: true }"
        :navigation="true"
        :modules="[Navigation, Pagination, Autoplay]"
        class="mySwiper"
      >
        <SwiperSlide v-for="movie in nowPlayingMovies" :key="movie.id">
          <img
            :src="'https://image.tmdb.org/t/p/w1280/' + movie.backdrop_path"
            :alt="movie.title"
          />
          <div class="gradient"></div>
          <div class="banner__text">
            <div class="banner__title">{{ movie.title }}</div>
            <span>{{ movie.overview }}</span>
            <p class="star">
              <img src="../assets/img/star.png" alt="#" />{{ movie.vote_average.toFixed(0) / 2 }}
            </p>

            <a href="#" @click="goToDetail(movie.id)">Watch View</a>
          </div>
        </SwiperSlide>
      </Swiper>
    </div>

    <div class="view__inner container">
      <section class="view__card">
        <h3>Now Playing</h3>
        <Swiper
          :slides-per-view="6"
          :space-between="20"
          :loop="true"
          :autoplay="{ delay: 4000, disableOnInteraction: false }"
          :modules="[Navigation, Pagination, Autoplay]"
          :navigation="true"
          class="mySwiper"
        >
          <SwiperSlide v-for="movie in nowPlayingMovies" :key="movie.id">
            <img :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :alt="movie.title" />
            <span>
              {{ movie.title }}
              <p class="star">
                <img src="../assets/img/star.png" alt="#" />{{ movie.vote_average.toFixed(0) / 2 }}
              </p>
            </span>

            <div class="buttons">
              <button @click="goToDetail(movie.id)" class="detail-button">
                <img src="../assets/img/detail.png" alt="Detail" />
              </button>
            </div>
          </SwiperSlide>
        </Swiper>
      </section>
      <section class="view__card">
        <h3>Popular</h3>
        <Swiper
          :slides-per-view="6"
          :space-between="20"
          :loop="true"
          :autoplay="{ delay: 4000, disableOnInteraction: false }"
          :modules="[Navigation, Pagination, Autoplay]"
          :navigation="true"
          class="mySwiper"
        >
          <SwiperSlide v-for="movie in popularMovies" :key="movie.id">
            <img :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :alt="movie.title" />
            <span class="span">
              {{ movie.title }}
              <p class="star">
                <img src="../assets/img/star.png" alt="#" />{{ movie.vote_average.toFixed(0) / 2 }}
              </p>
            </span>
            <div class="buttons">
              <button @click="goToDetail(movie.id)" class="detail-button">
                <img src="../assets/img/detail.png" alt="Detail" />
              </button>
            </div>
          </SwiperSlide>
        </Swiper>
      </section>
      <section class="view__card">
        <h3>Top Rated</h3>
        <Swiper
          :slides-per-view="6"
          :space-between="20"
          :loop="true"
          :autoplay="{ delay: 4000, disableOnInteraction: false }"
          :modules="[Navigation, Pagination, Autoplay]"
          :navigation="true"
          class="mySwiper"
        >
          <SwiperSlide v-for="movie in topRatedMovies" :key="movie.id">
            <img :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :alt="movie.title" />
            <span
              >{{ movie.title }}
              <p class="star">
                <img src="../assets/img/star.png" alt="#" />{{ movie.vote_average.toFixed(0) / 2 }}
              </p>
            </span>

            <div class="buttons">
              <button @click="goToDetail(movie.id)" class="detail-button">
                <img src="../assets/img/detail.png" alt="Detail" />
              </button>
            </div>
          </SwiperSlide>
        </Swiper>
      </section>
      <section class="view__card">
        <h3>Upcoming</h3>
        <Swiper
          :slides-per-view="6"
          :space-between="20"
          :loop="true"
          :autoplay="{ delay: 4000, disableOnInteraction: false }"
          :modules="[Navigation, Pagination, Autoplay]"
          :navigation="true"
          class="mySwiper"
        >
          <SwiperSlide v-for="movie in upcomingMovies" :key="movie.id">
            <img :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :alt="movie.title" />
            <span
              >{{ movie.title }}
              <p class="star">
                <img src="../assets/img/star.png" alt="#" />{{ movie.vote_average.toFixed(0) / 2 }}
              </p>
            </span>

            <div class="buttons">
              <button @click="goToDetail(movie.id)" class="detail-button">
                <img src="../assets/img/detail.png" alt="Detail" />
              </button>
            </div>
          </SwiperSlide>
        </Swiper>
      </section>
    </div>
  </main>
  <FooterSection />
</template>

<style scoped>
.banner {
  width: 100%;
  margin-bottom: 50px;
  position: relative;
  height: calc(100vh - 100px);
}

.banner .swiper {
  height: 100%;
  margin-bottom: 10px;
}

.banner__image {
  max-width: 100%; /* 이미지 너비를 최대 100%로 설정하여 부모 요소에 맞춥니다. */
  height: auto; /* 이미지 높이를 자동으로 조정하여 가로세로 비율을 유지합니다. */
}

.banner__text {
  position: absolute;
  bottom: 20%;
  left: 5%;
  font-weight: 900;
  z-index: 2;
  color: #eeeeee;
  width: 90%; /* 텍스트 너비를 조정하여 화면에 맞춥니다. */
  max-width: 600px; /* 최대 너비를 설정하여 너무 넓어지지 않도록 합니다. */
}

.banner__title {
  font-size: 4rem;
  font-family: var(--fontJ);
}
.banner__title img {
  width: 20px;
  height: 20px;
  margin-right: 10px;
}
.banner__text span {
  font-size: 1rem;
  display: block;
  margin-bottom: 10px;
}

.banner__text p {
  margin-bottom: 10px;
}
.view__card h3 {
  font-size: 3rem;
}
.view__card span {
  display: block; /* 블록 요소로 설정하여 줄바꿈 처리 */
  margin-top: 10px; /* 상단 여백 추가 */
  font-size: 1rem; /* 기본 폰트 크기 설정 */
}

.view__card .star img {
  width: 20px; /* 별 이미지 크기 */
  height: 20px;
  margin-right: 5px; /* 오른쪽 여백 */
}
.view__card h3 {
  font-size: 2rem; /* 기본 폰트 크기 설정 */
}

@media screen and (max-width: 1200px) {
  .view__card h3 {
    font-size: 1.8rem; /* 중간 크기 화면에서 폰트 크기 조정 */
  }
}

@media screen and (max-width: 768px) {
  .view__card h3 {
    font-size: 1.5rem; /* 작은 화면에서 폰트 크기 다시 조정 */
  }
}

@media screen and (max-width: 768px) {
  .view__card span {
    font-size: 0.9rem; /* 작은 화면에서 폰트 크기 다시 조정 */
  }

  .view__card .star img {
    width: 18px; /* 별 이미지 크기 작게 조정 */
    height: 18px;
  }
}

.banner__text a {
  padding: 10px 30px;
  background-color: #ff0909;
  font-size: 1rem;
  font-weight: 700;
  border-radius: 3px;
  color: #ffffff;
  text-decoration: none;
}
.star img {
  width: 20px;
  height: 20px;
  margin-right: 10px;
}

.swiper-slide {
  img {
    position: relative;
  }
  .buttons {
    position: absolute;
    bottom: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: flex;
    gap: 20px;
    opacity: 0;
    transition: opacity 0.3s;
  }

  &:hover .buttons {
    opacity: 1;
  }

  .play-button,
  .detail-button {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background-color: rgba(255, 255, 255, 0.678);
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    border: none;
    outline: none;
    position: relative;
  }

  .play-button img,
  .detail-button img {
    width: 30px;
    height: 30px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
}
@media screen and (max-width: 1200px) {
  .banner__text {
    bottom: 15%;
    left: 4%;
  }

  .banner__title {
    font-size: 3rem;
  }

  .banner__text span {
    font-size: 0.9rem;
  }

  .banner__text p {
    margin-bottom: 8px;
  }

  .banner__text a {
    padding: 8px 26px;
    font-size: 0.95rem;
  }
}
@media screen and (max-width: 768px) {
  .banner__text {
    bottom: 10%;
    left: 3%;
  }

  .banner__title {
    font-size: 2.5rem;
  }

  .banner__text span {
    font-size: 0.8rem;
  }

  .banner__text p {
    margin-bottom: 5px;
  }

  .banner__text a {
    padding: 8px 24px;
    font-size: 0.9rem;
  }
}
</style>
