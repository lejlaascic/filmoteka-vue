<template>
  <div class="movie-detail">
    <header>
      <div class="header-title">
        <h2>{{ movie.Title }}({{ movie.Year }})</h2>
        <p><i class="fas fa-star"></i>{{ movie.imdbRating }}</p>
      </div>
      <div class="header-info">
        <span> {{ movie.Runtime }}</span> | <span>{{ movie.Genre }}</span> |
        <span>{{ movie.Released }}</span>
      </div>
    </header>
    <div class="main">
      <div class="main-img">
        <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
      </div>
      <div class="main-info">
        <p><span>Description: </span>{{ movie.Plot }}</p>
        <p><span>Director: </span>{{ movie.Director }}</p>
        <p><span>Writers: </span>{{ movie.Writer }}</p>
        <p><span>Actors: </span>{{ movie.Actors }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";
export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `https://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          movie.value = data;
          console.log(data);
        });
    });
    return {
      movie,
    };
  },
};
</script>

<style lang='scss'>
.movie-detail {
  width: 80%;
  margin: 0 auto;
  header {
    width: 100%;
    border-bottom: 2px solid #888;
    background-color: inherit;
    display: flex;
    padding: 20px;
    flex-direction: column;
    .header-title {
      display: flex;
      justify-content: space-between;
      width: 100%;
      padding: 10px 0;
      margin-bottom: 20px;
      h2 {
        color: #fff;
        font-size: 38px;
        font-weight: 600;
        margin: 0;
      }
      p {
        font-size: 26px;
        color: #fff;
        i {
          font-size: 26px;
          color: #fb9027;
          margin-right: 5px;
        }
      }
    }
    .header-info {
      display: flex;
      width: 100%;
      justify-content: center;
      align-items: center;
      color: #fff;
      span {
        margin: 0 10px;
        &:hover {
          cursor: pointer;
          opacity: 0.6;
        }
      }
    }
  }
  .main {
    width: 100%;
    display: flex;
    padding: 20px;
    .main-img {
      flex: 1 1 50%;
      .featured-img {
        width: 100%;
      }
    }
    .main-info {
      display: flex;
      flex: 1 1 50%;
      flex-direction: column;
      padding: 16px;
      color: #fff;
      p {
        margin: 20px;
        font-size: 18px;
        span {
          font-weight: 800;
          color: #242424;
          margin-right: 8px;
          font-size: 22px;
        }
      }
    }
  }
}

@media screen and (max-width: 690px) {
  .movie-detail {
    width: 100%;
    padding: 10px;
    header {
      display: flex;
      padding: 8px;
      flex-direction: column;
      .header-title {
        display: flex;
        justify-content: space-between;
        width: 100%;
        padding: 10px 0;
        margin-bottom: 10px;
        h2 {
          font-size: 28px;
        }
        p {
          font-size: 20px;

          i {
            font-size: 20px;
          }
        }
      }
      .header-info {
        display: flex;
        width: 100%;
        justify-content: center;
        align-items: center;
        color: #fff;
        margin-bottom: 10px;
        span {
          margin: 0 2px;
          font-size: 15px;
          &:hover {
            cursor: pointer;
            opacity: 0.6;
          }
        }
      }
    }
    .main {
      width: 100%;
      display: flex;
      flex-direction: column;
      padding: 20px;
      .main-img {
        .featured-img {
          width: 100%;
        }
      }
      .main-info {
        padding: 16px;
        color: #fff;
        p {
          margin: 20px;
          font-size: 18px;
          span {
            font-weight: 800;
            color: #222;
            margin-right: 8px;
            font-size: 22px;
          }
        }
      }
    }
  }
}

@media screen and (min-width: 1024px) {
  .movie-detail {
    width: 100%;
    padding: 20px;
    header {
      width: 100%;
      display: flex;
      padding: 18px;
      flex-direction: column;
      .header-title {
        display: flex;
        justify-content: space-between;
        width: 100%;
        padding: 10px 0;
        margin-bottom: 20px;
        h2 {
          font-size: 42px;
          font-weight: 600;
        }
        p {
          font-size: 24px;

          i {
            font-size: 24px;
          }
        }
      }
      .header-info {
        display: flex;
        width: 100%;
        justify-content: center;
        align-items: center;
        span {
          margin: 0 10px;
          font-size: 18px;
        }
      }
    }
    .main {
      width: 100%;
      display: flex;
      padding: 20px;
      margin-top: 50px;
      .main-img {
        flex: 1 1 50%;
      }
      .main-info {
        display: flex;
        flex: 1 1 50%;
        flex-direction: column;
        padding: 16px;

        p {
          margin: 20px;
          font-size: 20px;
          span {
            font-size: 26px;
          }
        }
      }
    }
  }
}

@media screen and (min-width: 1600px) {
  .movie-detail {
    width: 80%;
    margin: 0 auto;
    header {
      width: 100%;
      display: flex;
      padding: 20px;
      flex-direction: column;
      .header-title {
        display: flex;
        justify-content: space-between;
        width: 100%;
        padding: 10px 0;
        margin-bottom: 20px;
        h2 {
          font-size: 48px;
        }
        p {
          font-size: 26px;

          i {
            font-size: 26px;
          }
        }
      }
      .header-info {
        display: flex;
        width: 100%;
        justify-content: center;
        align-items: center;
        span {
          margin: 0 10px;
          font-size: 20px;
        }
      }
    }
    .main {
      width: 100%;
      display: flex;
      padding: 20px;
      .main-img {
        flex: 1 1 50%;
      }
      .main-info {
        display: flex;
        flex: 1 1 50%;
        flex-direction: column;
        padding: 16px;

        p {
          font-size: 20px;
          span {
            font-size: 24px;
          }
        }
      }
    }
  }
}
</style>
