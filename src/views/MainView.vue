<template>
  <HeaderCont />
  <main id="main">
    <section class="main__cont">
      <div class="main__inner">
        <div v-for="list in lists" v-bind:key="list.text">{{ list.text }}</div>
      </div>
    </section>
  </main>
  <FooterCont />
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
  },

  data() {
    return {
      lists: [
        { text: "WE PROVIDE" },
        { text: "VISUAL CODING" },
        { text: "SOLUTIONS" },
        { text: "FOR YOU WEBS" },
      ],
    };
  },
};
</script>

<style lang="scss">
.main__cont {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: var(--dark_bg);

  .main__inner {
    font-size: 10vw;
    line-height: 0.85;
    font-family: var(--main_font);
    // text-align: left;
    color: var(--white);
    text-transform: uppercase;
  }
}

// // main Animation
// .main__inner > div {
//   opacity: 0;
//   transform: translateY(100px);
// }

//라이트 버전
.main__cont.light {
  background-color: var(--light_bg);

  .main__inner {
    color: var(--black);
  }
}

// #main.light {
//   background-color: var(--light_bg);
//   border-color: var(--light_border);
//   color: var(--black);

//   h4 {
//     color: var(--black);
//   }
//   a {
//     color: var(--black);

//     &::before {
//       background: var(--black);
//     }
//   }
//   div {
//     border-right-color: var(--light_border);
//     // background-color: var(--light_bg);
//     // border-color: var(--light_border);
//     // color: var(--black);
//   }
// }
</style>
