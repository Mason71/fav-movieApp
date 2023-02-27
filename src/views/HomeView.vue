<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0388629">
        <img
          src="https://i.pinimg.com/564x/78/2f/03/782f032235bd4b00c80de140b8e70538.jpg"
          alt="one piece poster"
          class="feature-img"
        />
        <div class="detail">
          <h3>One Piece</h3>
          <p>
            Monkey D. Luffy wants to become the King of all pirates. The gang
            sets sail to unknown seas in Grand Line to find the treasure of One
            Piece.
          </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input
        type="text"
        placeholder="What are You Looking for?"
        v-model="search"
      />
      <input type="submit" value="Search" />
    </form>
    <div class="movie-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        {{ movie.title }}
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>
              {{ movie.Title }}
            </h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import env from "@/env.js";
import { ref } from "vue";

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    };

    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>
<style lang="scss" scoped>
@media screen and (max-width: 481px) {
  .home {
    .feature-card {
      position: relative;
      .feature-img {
        display: block;
        width: 100%;
        height: 300px;
        object-fit: cover;

        position: relative;
        z-index: 0;
      }

      .detail {
        position: absolute;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: rgba(0, 0, 0, 0.5);
        padding: 16px;
        z-index: 1;

        h3 {
          color: #fff;
          margin-bottom: 16px;
        }
        p {
          color: #fff;
        }
      }
    }
    .search-box {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 16px;

      input {
        display: block;
        appearance: none;
        border: none;
        outline: none;
        background: none;
        background-color: #496583;

        padding: 10px 16px;
        border-radius: 8px;
        width: 100%;
        text-align: center;
        margin-bottom: 15px;
        transition: 0.4s;
        font-size: 20px;

        &::palceholeder {
          color: #f3f3f3;
        }
        & [type="text"] &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }

        &[type="SUBMIT"] {
          width: 100%;
          max-width: 300px;
          background: #42b883;
          padding: 16px;
          border-radius: 8px;
          clear: #fff;
          font-size: 20px;
          text-transform: uppercase;
          transition: 0.4s;
          &:active {
            background-color: #3b8070;
          }
        }
      }
    }
    .movie-list {
      color: #f3f3f3;
      display: flex;
      flex-wrap: wrap;
      margin: 0px 8px;

      .movie {
        max-width: 50%;
        flex: 1 1 50%;
        padding: 16px 8px;
        .movie-link {
          display: flex;
          flex-direction: column;
          height: 100%;
          .product-image {
            position: relative;
            display: block;
            img {
              border-radius: 8px;
              display: block;
              width: 100%;
              height: 275px;
              object-fit: cover;
            }
            .type {
              position: absolute;
              padding: 8px 16px;
              background-color: #42b883;
              color: #fff;
              bottom: 16px;
              left: 0px0;
              text-transform: capitalize;
            }
          }
          .detail {
            background-color: #496583;
            padding: 16px 8px;
            flex: 1 1 100;
            border-radius: 0px 0px 8px 8px;
            .year {
              color: #aaa;
              font-size: 14px;
            }
            h3 {
              color: #fff;
              font-weight: 600;
              font-size: 18px;
            }
          }
        }
      }
    }
  }
}
@media screen and (min-width: 481px) {
  .home {
    .feature-card {
      position: relative;
      .feature-img {
        display: block;
        width: 100%;
        height: 100%;
        object-fit: cover;
        padding: 5px;

        border-radius: 16px;
        position: relative;
        z-index: 0;
      }

      .detail {
        position: absolute;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: rgba(0, 0, 0, 0.5);
        padding: 16px;
        z-index: 1;

        h3 {
          color: #fff;
          margin-bottom: 16px;
        }
        p {
          color: #fff;
        }
      }
    }
    .search-box {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 16px;

      input {
        display: block;
        appearance: none;
        border: none;
        outline: none;
        background: none;
        background-color: #496583;

        padding: 10px 16px;
        border-radius: 8px;
        width: 50%;
        text-align: center;
        margin-bottom: 15px;
        transition: 0.4s;
        font-size: 20px;

        &::palceholeder {
          color: #f3f3f3;
        }
        & [type="text"] &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }

        &[type="SUBMIT"] {
          width: 100%;
          max-width: 300px;
          background: #42b883;
          padding: 16px;
          border-radius: 8px;
          clear: #fff;
          font-size: 20px;
          text-transform: uppercase;
          transition: 0.4s;
          &:active {
            background-color: #3b8070;
          }
        }
      }
    }
    .movie-list {
      color: #f3f3f3;
      display: flex;
      flex-wrap: wrap;
      margin: 0px 8px;

      .movie {
        max-width: 50%;
        flex: 1 1 50%;
        padding: 16px 8px;
        .movie-link {
          display: flex;
          flex-direction: column;
          height: 100%;
          .product-image {
            position: relative;
            display: block;
            img {
              border-radius: 8px;
              display: block;
              width: 100%;
              height: 600px;
              object-fit: cover;
            }
            .type {
              position: absolute;
              padding: 8px 16px;
              background-color: #42b883;
              color: #fff;
              bottom: 16px;
              left: 0px0;
              text-transform: capitalize;
            }
          }
          .detail {
            background-color: #496583;
            padding: 16px 8px;
            flex: 1 1 100;
            border-radius: 0px 0px 8px 8px;
            .year {
              color: #aaa;
              font-size: 14px;
            }
            h3 {
              color: #fff;
              font-weight: 600;
              font-size: 18px;
            }
          }
        }
      }
    }
  }
}
</style>
