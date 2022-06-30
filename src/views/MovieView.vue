<template>
  <HeaderCont />
  <main id="main">
    <TitleCont name1="movie" name2="book" />
    <section className="movie__cont">
      <div className="container">
        <div className="movie__inner">
          <div className="movie__search">
            <form @submit.prevent="SearchMovies()">
              <label for="search" className="sr-only">검색하기</label>
              <input
                type="search"
                id="search"
                placeholder="검색하세요!"
                v-model="search"
              />
            </form>
            <button type="submit">검색</button>
          </div>
          <div className="movie__list">
            <ul>
              <li v-for="movie in movies" :key="movie.id">
                <a :href="`https://www.themoviedb.org/movie/` + movie.id">
                  <img
                    :src="
                      `https://image.tmdb.org/t/p/w500/` + movie.poster_path
                    "
                    :alt="movie.title"
                  />
                  <p className="title">{{ movie.title }}</p>
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>
      <ContactCont />
    </section>
  </main>
  <FooterCont />
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
  },

  setup() {
    const movies = ref([]);
    const search = ref("bts");

    const SearchMovies = () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };

      if (search.value != "") {
        fetch(
          `https://api.themoviedb.org/3/search/movie?api_key=f7c17123bdb6536cfab9cbd3bdc1e2ff&query=${search.value}`,
          requestOptions
        )
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.results;
            search.value = "";
            console.log(movies);
          })
          .catch((error) => console.log("error", error));
      }
    };
    SearchMovies();

    return {
      movies,
      search,
      SearchMovies,
    };
  },
};
</script>

<style lang="scss" scoped>
.movie__list {
  ul {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    gap: 1%;
    li {
      flex: 1 1 20%;
      margin: 1%;
      img {
        border-radius: 0.4em;
      }

      p {
        color: var(--white);
        font-family: var(--subKor_font);
        padding-top: 10px;
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
      }
    }
  }
}

.movie__search {
  position: relative;
  h2 {
    color: var(--white);
    font-size: 40px;
    font-family: var(--subKor_font);
    text-indent: -9999px;
    width: 0;
    height: 0;
  }
  input {
    border: 3px solid var(--dark_border);
    width: 98%;
    background: var(--black);
    border-radius: 50px;
    padding: 1rem;
    color: var(--light_bg);
    font-family: var(--subKor_font);
    margin: 0 1%;
    margin-bottom: 2%;
  }
  button {
    position: absolute;
    right: 20px;
    top: 8px;
    background: transparent;
    border: 0;
    color: var(--black);
    background: var(--white);
    font-family: var(--subKor_font);
    width: 40px;
    height: 40px;
    border-radius: 50%;
    font-size: 12px;
    transition: opacity 0.3s ease;

    &:active {
      opacity: 1;
    }
  }
}
</style>
