<template>
  <div class="movie-detail">
   
    <h2>{{ movie.Title }}</h2>
    <p>{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="movie poster" class="feature-img" />
    <p>{{ movie.Plot }}</p>
  </div>
</template>

<script>
import { ref, onBeforeMount} from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then(data => {
          movie.value = data;
          console.log(data);
          
        });
    });
    return {
      movie,
    };
  }
};
</script>

<style lang="scss" scoped>
.movie-detail {
  padding: 16px;
  font-size: 28px;
  font-weight: 600;
  margin-bottom: 16px;
}
.feature-img {
  display: block;
  max-width: 2000px;
  margin-bottom: 16px;
  
  border-radius: 8px;
}
p {
  color: #dfdddd;
  font-size: 18px;
  line-height: 1.4;
 margin-top: 16px;
}

</style>
