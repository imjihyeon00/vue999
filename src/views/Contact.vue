<template>
  <div class="light">
    <Header />
    <main id="main">
      <section id="mainCont">
        <h2 class="sr-only">연락처 컨텐츠 영역입니다.</h2>
        <div class="main__cont">
          <div class="l1">You are</div>
          <div class="l2">already</div>
          <div class="l3">doing well.</div>
        </div>
      </section>
    </main>
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';

export default {
  components: {
    Header,
    Footer,
  },
};
</script>

<style scoped lang="scss">
// contact__info
.contact__info {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  background: #000;
  color: #fff;
  border-top: 1px solid #2e2e30;

  p {
    font-size: 24px;
    font-weight: 400;
    margin-bottom: 80px;
    font-family: 'Rajdhani';
  }

  h3 {
    font-size: 9vw;
    line-height: 1;
    text-transform: uppercase;
    margin-bottom: 5rem;
    font-family: 'saol';
  }

  a {
    color: #000;
    background: #f0eeeb;
    border-radius: 50px;
    padding: 18px 53px;
    font-size: 20px;
    font-weight: 400;
    text-transform: uppercase;
    font-family: 'Rajdhani';
  }
}
</style>
