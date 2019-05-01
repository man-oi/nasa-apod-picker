<template>
  <div id="app">
    <div id="app-inner">
      <!-- <header id="app-header">
        <div id="nav">
          <router-link to="/">Home</router-link> |
          <router-link to="/about">About</router-link>
        </div>
      </header> -->

      <main id="app-main">
        <router-view/>
      </main>
    </div>
  </div>
</template>


<script>
export default {
  name: 'app',
  components: {
  },
};
</script>


<style lang="scss">
body {
  padding: 0;
  margin: 0;

  background-image: url('./assets/background.jpg');
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;


  &::before {
    content: '';
    display: block;

    background-color: rgba(255, 255, 255, 0.2);

    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
  }
}

h1, h2, h3, h4, h5, h6 {
  margin-top: 0;
}

#app {
  min-height: 100vh;
  max-width: 900px;
  padding: 0 40px;
  margin: 0 auto;

  background-color: rgba(255, 255, 255, 0.8);

  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

  #app-inner {
    padding-top: 30px;
    padding-bottom: 60px;
  }

    #app-header {
      margin-bottom: 40px;

      text-align: center;
    }
</style>


<style lang="scss">
.el-row {
  margin-bottom: 20px;
  &:last-child {
    margin-bottom: 0;
  }
}
</style>
