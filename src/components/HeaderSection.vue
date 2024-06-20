<template>
  <div>
    <header id="header" role="banner">
      <div class="header__inner container">
        <div class="logo">
          <h2><a href="/">MVKING</a></h2>
        </div>

        <div class="search">
          <input v-model="query" type="search" placeholder="" @keyup.enter="navigateToSearch" />
          <button @click="navigateToSearch">Search</button>
        </div>
      </div>
    </header>

    <router-view />
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: ''
    }
  },
  methods: {
    navigateToSearch() {
      if (this.query) {
        this.$router.push({ name: 'search', query: { q: this.query } })
      }
    }
  }
}
</script>

<style lang="scss">
.header__inner {
  padding: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;

  @media screen and (max-width: 768px) {
    flex-direction: column;
    padding: 10px;

    .logo {
      margin-bottom: 10px;
    }
  }

  .logo h2 {
    font-size: 2.5rem;
    font-weight: 900;
    color: #ff0000;
    margin: 0;
  }

  .search {
    position: relative;
    display: flex;
    align-items: center;
    color: #fff;

    @media screen and (max-width: 768px) {
      width: 50%;
      display: block;
    }

    input {
      background: linear-gradient(to right, #ff0000, #a00000);
      padding: 10px;
      width: 400px;
      border-radius: 10px;
      text-align: left;
      color: #fff;
      border: 1px solid #575757;

      @media screen and (max-width: 768px) {
        width: 100%;
      }
    }

    button {
      margin-left: 10px;
      padding: 10px 20px;
      color: #fff;
      background-color: #43404e;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: background-color 0.3s;

      @media screen and (max-width: 768px) {
        margin-top: 10px;
        width: 100%;
        margin-left: 0;
      }

      &:hover {
        background-color: #555;
      }
    }
  }
}
</style>
