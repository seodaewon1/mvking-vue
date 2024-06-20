<template>
  <div>
    <h1>"{{ $route.query.q }}" Search results for</h1>
    <div v-if="loading" class="loading">Loading...</div>
    <div v-else class="results">
      <div v-for="movie in movies" :key="movie.id" class="movie">
        <!-- 영화 포스터, 제목 및 개봉 연도 표시 -->
        <img :src="getImageUrl(movie.poster_path)" alt="Movie Poster" class="movie-poster" />
        <h2 @click="viewDetails(movie.id)" class="movie-title">{{ movie.title }}</h2>
        <p>{{ getReleaseYear(movie.release_date) }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      movies: [],
      loading: true
    }
  },
  created() {
    this.fetchMovies()
  },
  watch: {
    '$route.query.q'() {
      this.fetchMovies()
    }
  },
  methods: {
    async fetchMovies() {
      this.loading = true
      try {
        const response = await axios.get(
          `https://api.themoviedb.org/3/search/movie?api_key=9fd9ecd1406306cca1771dc03b2fd6ac&query=${this.$route.query.q}&page=1`
        )
        this.movies = response.data.results
      } catch (error) {
        console.error('데이터를 가져오는 중 에러 발생:', error)
      } finally {
        this.loading = false
      }
    },
    viewDetails(movieID) {
      this.$router.push({ name: 'detail', params: { movieID: movieID } })
    },
    getImageUrl(posterPath) {
      return posterPath
        ? `https://image.tmdb.org/t/p/w300${posterPath}`
        : 'https://via.placeholder.com/300x450?text=No+Image'
    },
    getReleaseYear(releaseDate) {
      return releaseDate ? releaseDate.substring(0, 4) : '-'
    }
  }
}
</script>

<style scoped>
h1 {
  text-align: center;
  font-size: 3rem; /* 기본 폰트 크기 설정 */
}

.loading {
  font-size: 18px;
  text-align: center;
  margin-top: 20px;
}

.results {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
  margin-top: 20px;
}

.movie {
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 20px;
  width: 300px;
  transition: transform 0.3s;
  text-align: center;
}

.movie:hover {
  transform: translateY(-10px);
}

.movie-title {
  cursor: pointer;
  color: #fdfdfd;
  text-decoration: underline;
  margin-top: 10px;
}

.movie-poster {
  width: 100%;
  height: auto;
  border-radius: 10px;
  margin-bottom: 10px;
}

p {
  color: #929292;
  margin-bottom: 0;
}

@media screen and (max-width: 768px) {
  h1 {
    font-size: 2rem; /* 작은 화면에서 폰트 크기 다시 조정 */
  }

  .results {
    gap: 10px; /* 작은 화면에서 간격 조정 */
  }

  .movie {
    width: 250px; /* 작은 화면에서 영화 카드 너비 조정 */
  }
}
</style>
