<template>
  <HeaderCont />
  <main id="main">
    <TitleCont name1="youtube" name2="book" />
    <section className="youtube__cont">
      <div className="container">
        <div className="youtube__inner">
          <div className="youtube__search">
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
          <div className="youtube__list">
            <ul>
              <li v-for="movie in movies" :key="movie.id.videoId">
                <a
                  :href="`https://www.youtube.com/watch?v=${movie.id.videoId}`"
                >
                  <img
                    :src="movie.snippet.thumbnails.medium.url"
                    :alt="movie.snippet.title"
                  />
                  <p className="title">{{ movie.snippet.title }}</p>
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>
    <ContactCont />
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
    const movies = ref("");

    const SearchMovies = () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };
      fetch(
        "https://youtube.googleapis.com/youtube/v3/search?part=snippet&maxResults=30&q=먹방&type=video&key=AIzaSyDDXEC06dKJzJj7sqkotQnYJzY4_mWxeFY",
        requestOptions
      )
        .then((response) => response.json())
        .then((data) => {
          movies.value = data.items;
          console.log(movies);
        })
        .catch((error) => console.log("error", error));
    };

    setTimeout(() => {
      SearchMovies();
    }, 0);

    return {
      movies,
      SearchMovies,
    };
  },
};
</script>

<style lang="scss">
.youtube_cont {
}
.youtube__inner {
  // opacity: 0;
}
.youtube {
  padding-bottom: 30vh;
}

.youtube__list {
  ul {
    display: flex;
    flex-wrap: wrap;
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

.youtube__search {
  position: relative;
  label {
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
      opacity: 0.7;
    }
  }
}

@media (max-width: 800px) {
  .youtube__list {
    ul {
      display: flex;
      flex-wrap: wrap;

      li {
        flex: 1 1 40%;
        // margin: 1%;
      }
    }
  }
}

// //애니메이션
// .youtube__search,
// .youtube__list {
//   opacity: 0;
//   transform: translateY(100px);
// }

// 라이트버전
.light.youtube_cont {
  background: var(--light_bg);

  .youtube__inner {
    .top {
      .title {
        color: var(--black);
      }
    }

    .bottom {
      table {
        color: var(--black);
      }
    }
  }
}
</style>
