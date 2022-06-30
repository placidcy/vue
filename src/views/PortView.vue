<template>
  <HeaderCont />
  <main id="main">
    <TitleCont name1="Portfolio" name2="book" />
    <section className="port__cont">
      <div className="container">
        <div className="port__inner">
          <div className="port__item" v-for="port in ports" :key="port.id">
            <figure class="img">
              <a href="/"><img :src="port.image" :alt="port.title" /></a>
            </figure>
            <div className="text">
              <h3>{{ port.title }}</h3>
              <p>{{ port.category }}</p>
            </div>
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
    const ports = ref([]);

    const Portfolios = () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };
      fetch(
        "https://webstoryboy.github.io/dothome1/portfolio.json",
        requestOptions
      )
        .then((response) => response.json())
        .then((data) => (ports.value = data.data.ports))
        .catch((error) => console.log("error", error));
    };

    setTimeout(() => {
      Portfolios();
    }, 2000);

    return {
      ports,
      Portfolios,
    };
  },
};
</script>

<style lang="scss">
.port__cont {
  padding-bottom: 20vh;
}
.port__inner {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-bottom: 100px;
}
.port__item {
  flex: 1 1 30%;
  margin: 1%;

  .img {
  }
  .text {
    padding: 1.4em;
    background-color: #e0dad2;

    h3 {
      color: var(--white);
      font-family: var(--main_font);
      font-size: 2.6rem;
      line-height: 1;
      padding-top: 0.2em;
      text-transform: uppercase;
    }
    p {
      color: var(--white);
      font-family: var(--sub_font);
    }
  }
}
</style>
