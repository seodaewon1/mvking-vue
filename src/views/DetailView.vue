<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import { useRoute } from 'vue-router'
import HeaderSection from '@/components/HeaderSection.vue'
import FooterSection from '@/components/FooterSection.vue'

const route = useRoute()
const movieID = ref(null)
const movie = ref(null)
const credits = ref([])
const apikey = '9fd9ecd1406306cca1771dc03b2fd6ac'

onMounted(async () => {
  movieID.value = route.params.movieID
  await fetchMovieDetails()
})

const fetchMovieDetails = async () => {
  try {
    const response = await axios.get(
      `https://api.themoviedb.org/3/movie/${movieID.value}?api_key=${apikey}`
    )
    movie.value = response.data
    console.log('Movie Details:', response.data)

    const videoResponse = await axios.get(
      `https://api.themoviedb.org/3/movie/${movieID.value}/videos?api_key=${apikey}`
    )
    if (movie.value && videoResponse.data.results.length > 0) {
      const teaserKey = videoResponse.data.results[0].key
      movie.value.teaserKey = teaserKey
    }

    const responseCredits = await axios.get(
      `https://api.themoviedb.org/3/movie/${movieID.value}/credits?api_key=${apikey}`
    )
    credits.value = responseCredits.data.cast
    console.log('Credits:', credits.value)
  } catch (error) {
    console.error('Error fetching movie details:', error)
  }
}
</script>

<template>
  <div>
    <HeaderSection />
    <div v-if="movie" class="detail-container">
      <!-- Background Image -->
      <div
        class="background-image"
        :style="{
          backgroundImage: `url(https://image.tmdb.org/t/p/original/${movie.poster_path})`
        }"
      ></div>

      <div class="movie-details">
        <img
          v-if="movie.poster_path"
          :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path"
          :alt="movie.title"
          class="poster"
        />
        <div class="details">
          <h2 class="title">{{ movie.title }}</h2>
          <p class="overview">{{ movie.overview }}</p>
          <p class="info">vote: {{ movie.vote_average.toFixed(1) }}</p>
          <p class="info">popularity: {{ movie.popularity.toFixed(2) }}</p>
          <p class="info">date: {{ movie.release_date }}</p>
          <p class="info">genres: {{ movie.genres.map((genre) => genre.name).join(', ') }}</p>
        </div>
      </div>
      <div class="credits">
        <h3>Actor</h3>
        <ul>
          <li v-for="credit in credits" :key="credit.cast_id" class="credit">
            <div class="credit-info">
              <img
                v-if="credit.profile_path"
                :src="'https://image.tmdb.org/t/p/w500/' + credit.profile_path"
                :alt="credit.name"
                class="profile-image"
              />
              <div class="name-and-character">
                <span class="cast__name">{{ credit.name }}</span
                ><br />
                <span class="char__name">{{ credit.character }}</span>
              </div>
            </div>
          </li>
        </ul>
      </div>
      <div class="teaser" v-if="movie.teaserKey">
        <h3>Teaser</h3>
        <iframe
          width="560"
          height="315"
          :src="'https://www.youtube.com/embed/' + movie.teaserKey"
          frameborder="0"
          allowfullscreen
        ></iframe>
      </div>
    </div>
    <FooterSection />
  </div>
</template>

<style lang="scss" scoped>
.background-image {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  opacity: 0.2; /* Adjust transparency here */
  z-index: -1; /* Ensure the background is behind other content */
}

.detail-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.movie-details {
  display: flex;
  margin-bottom: 20px; /* 디테일과 티저 섹션 간의 간격 */
}

.poster {
  width: 200px;
  height: auto;
  border-radius: 8px;
  margin-right: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.details {
  flex: 1;
}

.title {
  font-size: 2rem;
  margin-bottom: 10px;
}

.overview {
  margin-bottom: 15px;
  line-height: 1.6;
}

.info {
  margin-bottom: 8px;
}

.credits {
  margin-bottom: 20px; /* 출연진 섹션과 티저 섹션 간의 간격 */
}

.credits h3 {
  font-size: 2rem;
  font-weight: 600;
  margin-bottom: 10px;
}
ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.credit {
  margin-bottom: 10px;
}
.credit-info {
  width: 200px;
  display: flex;
}

.profile-image {
  width: 80px;
  height: 120px;
  border-radius: 8px;
  margin-right: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.name-and-character {
  flex: 1;
  display: block;
}

.cast__name {
  font-weight: bold;
}

.teaser {
  border-top: 1px solid #ccc; /* 티저 섹션 위에 선 추가 */
  padding-top: 20px; /* 선 위에 여백 추가 */
}

.teaser h3 {
  font-size: 2rem;
  font-weight: 600;
  margin-bottom: 10px;
}

.teaser iframe {
  margin-top: 10px;
}
</style>
