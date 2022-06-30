<template>
  <HeaderCont />
  <main id="main">
    <TitleCont name1="reference" name2="book" />
    <section className="refer__cont">
      <div className="container">
        <div className="refer__inner">
          <h2>CSS</h2>
          <ul className="refer__list" v-for="port in ports" :key="port.id">
            <li>
              <a href="">
                <span className="num"> {{ port.id }} </span>
                <span className="title"> {{ port.title }} </span>
                <span className="desc"> {{ port.desc }} </span>
                <span className="use"> {{ port.use }} </span>
              </a>
            </li>
          </ul>
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
    const ports = ref([]);

    const Reference = () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };
      fetch(
        "https://webstoryboy.github.io/react2022/src/assets/json/refer.json",
        requestOptions
      )
        .then((response) => response.json())
        .then((data) => (ports.value = data.data.htmlRefer))
        .catch((error) => console.log("error", error));
    };

    setTimeout(() => {
      Reference();
    }, 0);

    return {
      ports,
      Reference,
    };
  },
};
</script>

<style lang="scss">
.refer__cont {
  background-color: var(--dark_bg);
  min-height: 100vh;
}
.refer__inner {
  h2 {
    color: var(--white);
    font-size: 2rem;
    margin-bottom: 1rem;
  }
}

.refer__list {
  a {
    display: block;
    color: var(--white);

    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid var(--light_bg);
    padding: 1.3rem 0;
    transform: all 0.3s;
    font-family: var(--subKor_font);

    &:hover {
      background: var(--light_bg);
      color: var(--black);
    }

    span {
      display: inline-block;
    }
    span:nth-child(1) {
      width: 6%;
      text-align: center;
    }
    span:nth-child(2) {
      width: 20%;
    }
    span:nth-child(3) {
      width: 64%;
    }
    span:nth-child(4) {
      width: 10%;
      text-align: center;
    }
  }
}

.refer__table {
  margin-top: 400px;
  color: var(--black);
  font-family: var(--subKor_font);

  h3 {
    font-size: 3rem;
  }
  p {
    background-color: var(--dark_bg);
    color: var(--black);
    padding: 1.3rem;
  }
  .table {
    color: var(--white);
    font-family: var(--subKor_font);
    border: 1px solid var(--dark_border);
    margin-top: 0.5em;

    th,
    td {
      font-weight: normal;
      padding: 1em;
      border-bottom: 1px solid var(--dark_bg);
      border-left: 1px solid var(--dark_bg);
    }
  }
}

//라이트
.light.refer__cont {
  background: var(--light_bg);
  .refer__inner {
    h2 {
      color: var(--black);
    }
    table {
      border-top: 1px solid var(--dark_border);
      border-bottom: 2px solid var(--dark_border);
      color: var(--black);
      td {
        border-top: 1px solid var(--dark_border);
      }
    }
  }
}
</style>
