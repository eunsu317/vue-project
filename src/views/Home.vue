<template>
    <div>
      <h1>영화 목록</h1>
      <div v-if="loading">로딩 중...</div>
      <div v-else>
        <div v-for="movie in movies" :key="movie.id">
          <router-link :to="'/movie/' + movie.id">{{ movie.title }}</router-link>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        movies: [],
        loading: true,
      };
    },
    mounted() {
      this.fetchMovies();
    },
    methods: {
      fetchMovies() {
        axios.get('https://api.themoviedb.org/3/') // 여기에 API URL 입력
          .then(response => {
            this.movies = response.data.results; // API 응답에 따라 조정
            this.loading = false;
          })
          .catch(error => {
            console.error(error);
            this.loading = false; // 오류 발생 시 로딩 상태 종료
          });
      },
    },
  };
  </script>
  
  <style>
  /* 스타일 추가 가능 */
  </style>
  