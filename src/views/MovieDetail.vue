<template>
    <div>
      <h1>{{ movie.title }}</h1>
      <p>개봉일: {{ movie.release_date }}</p>
      <p>{{ movie.overview }}</p>
      <router-link to="/">뒤로 가기</router-link>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        movie: {},
        loading: true,
      };
    },
    mounted() {
      this.fetchMovieDetail();
    },
    methods: {
      fetchMovieDetail() {
        const movieId = this.$route.params.id; // URL 파라미터에서 영화 ID 가져오기
        axios.get('https://api.themoviedb.org/3/') // API URL 수정
          .then(response => {
            this.movie = response.data; // 응답 데이터에서 영화 정보 가져오기
            this.loading = false; // 로딩 상태 해제
          })
          .catch(error => {
            console.error(error);
            this.loading = false; // 오류 발생 시 로딩 상태 해제
          });
      },
    },
  };
  </script>
  
  <style>
  /* 스타일 추가 가능 */
  </style>
  