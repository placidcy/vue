<template>
  <section className="cont__title">
    <div className="container">
      <strong> {{ name1 }} </strong>
      <em> {{ name2 }}</em>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    name1: String,
    name2: String,
  },
};
</script>

<style scoped lang="scss">
//cont__title
.cont__title {
  padding: 15vmax 1% 10vmax;
  font-size: 5vmax;
  font-family: var(--main_font);
  text-transform: uppercase;
  line-height: 0.85;
  color: var(--white);

  em {
    display: block;
  }
}
@media (max-width: 600px) {
  .cont__title {
    text-align: center;
    padding-bottom: 10vw;
  }
}
//라이트 버전
.light.cont__title {
  background-color: var(--light_bg);
  border-color: var(--light_border);

  div {
    color: var(--black);

    &::before {
      background: var(--black);
    }
  }
}
</style>
