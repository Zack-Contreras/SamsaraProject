<style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

  html {
    background: #00263E;
  }

  main {
    display: flex;
    justify-content: center;
    flex-direction: column;
    width: max-content;
    margin: auto;
    padding-bottom: 3rem;
  }

  .title h1 {
    margin: 0;
    font-family: 'Roboto';
    font-style: normal;
    font-weight: 500;
    font-size: 90px;
    line-height: 120px;
    color: white;
  }

  .title p {
    margin: 0;
    font-family: 'Roboto';
    font-style: normal;
    font-weight: 400;
    font-size: 36px;
    line-height: 42px;
    color: #0DE7EF;
  }

  @media screen and (max-width: 1224px) {

    main {
      padding: 0 1rem 0 1rem ;
    }  

    .title h1 {
      font-size: 55px;
      line-height: 70px;
    }

    .title p {
      font-size: 30px;
    }
  }

  @media screen and (max-width: 767px) {
    main {
      width: auto;
      padding-top: 1rem;
      margin-bottom: 2rem;
    }

    .title {
      margin: auto;
      text-align: center;
    }

    .title h1 {
      font-size: 35px;
      line-height: 42px;
    }

    .title p {
      font-size: 24px;
    }
  }

</style>

<template>
  <div id="app">
    <!-- Header w/ Logo -->
    <samsara-header/>
    <!-- Main Content -->
    <main>
      <!-- Title Section w/ Intro -->
      <section class="title">
        <h1>Top 3 Features</h1>
        <p>Here are some of our favorite features</p>
      </section>
      <!-- Feature Showcase -->
      <section>
        <samsara-feature-showcase/>
      </section>
    </main>
  </div>
</template>

<script>
import SamsaraHeader from './components/samsara_header.vue'
import FeatureShowcase from './components/samsara_feature_showcase.vue'
export default {
  components: {
    "samsara-header": SamsaraHeader,
    "samsara-feature-showcase": FeatureShowcase
  }
}
</script>

