<template>
  <div class="home">
    <div class="feauture-card">
      <router-link to="/movie/tt0451279">
        <img
          src="https://pbs.twimg.com/media/DMHahHQX0AAJlSt.jpg:large"
          alt="Wonder Woman "
          class="futured-image"
        />
        <div class="detail">
          <h3>Wonder Woman</h3>
          <p>
            Diana, princess of the Amazons, trained to be an unconquerable
            warrior. Raised on a sheltered island paradise, when a pilot crashes
            on their shores and tells of a massive conflict raging in the
            outside world, Diana leaves her home, convinced she can stop the
            threat.
          </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input
        type="text"
        placeholder="What are you looking for?"
        v-model="search"
      />
      <input type="submit" value="Search" />
    </form>

    <div class="movie-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from "vue";
import env from "@/env.js";
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
            // console.log(movies.value);
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

<style lang="scss">
.home {
  .feauture-card {
    position: relative;
    .futured-image {
      display: block;
      width: 100%;
      height: 400px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }
    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
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

      &[type="text"] {
        width: 100%;
        color: #fff;
        background-color: #496583;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;
        &::placeholder {
          color: #f3f3f3;
        }

        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }
      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #42bb83;
        padding: 16px;
        border-radius: 8px;
        color: #fff;
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
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }

          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #42bb83;
            color: #fff;
            bottom: 16px;
            left: 0;
            text-transform: capitalize;
          }
        }

        .detail {
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
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
@media screen and (min-width: 690px) {
  .home {
    width: 100%;
    .feauture-card {
      .futured-image {
        height: 400px;
      }
    }
    .detail {
      h3 {
        font-size: 32px;
      }
      p {
        font-size: 18px;
      }
    }
    .movie-list {
      .movie {
        max-width: 25%;
        flex: 1 1 25%;
        .movie-link {
          .product-image img {
            height: 275px;
          }
          .detail {
            .year {
              font-size: 14px;
            }

            h3 {
              font-size: 18px;
            }
          }
        }
      }
    }
  }
}
@media screen and (min-width: 1024px) {
  .home {
    width: 100%;
    .feauture-card {
      .futured-image {
        height: 500px;
      }
    }
    .detail {
      h3 {
        font-size: 28px;
      }
      p {
        font-size: 17px;
      }
    }
    .movie-list {
      .movie {
        max-width: 25%;
        flex: 1 1 25%;
        .movie-link {
          .product-image img {
            height: 400px;
          }
          .detail {
            .year {
              font-size: 18px;
            }

            h3 {
              font-size: 22px;
            }
          }
        }
      }
    }
  }
}
@media screen and (min-width: 1600px) {
  .home {
    width: 80%;
    margin: auto;
    .feauture-card {
      .futured-image {
        height: 600px;
      }
    }
    .detail {
      h3 {
        font-size: 32px;
      }
      p {
        font-size: 18px;
      }
    }
    .movie-list {
      .movie {
        max-width: 25%;
        flex: 1 1 25%;
        .movie-link {
          .product-image img {
            height: 500px;
          }
          .detail {
            .year {
              font-size: 18px;
            }

            h3 {
              font-size: 22px;
            }
          }
        }
      }
    }
  }
}
</style>