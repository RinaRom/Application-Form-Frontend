<template>
  <div class="home">
    <table class="home__table">
      <tr>
        <td class="home-table__title">Имя</td>
        <td class="home-table__title">Фамилия</td>
        <td class="home-table__title">Телефон</td>
        <td class="home-table__title">Почта</td>
      </tr>
      <tr v-for="item in data" :key="item.id">
        <td class="home-table__text">{{ item?.name }}</td>
        <td class="home-table__text">{{ item?.last_name }}</td>
        <td class="home-table__text">{{ item?.phone }}</td>
        <td class="home-table__text">{{ item?.email }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import { api_url } from "@/config/config";

export default {
  name: "HomeView",
  components: {},
  data: () => {
    return {
      data: [],
    };
  },
  methods: {
    Get() {
      fetch(api_url + "/api/v1/application")
        .then((data) => data.json())
        .then((data) => (this.data = data));
    },
  },
  mounted() {
    this.Get();
  },
};
</script>
<style lang="scss" scoped>
.home {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  .home__table {
    background-color: aliceblue;
    border: 1px solid #376ecc;
    width: 60%;
    tr {
      .home-table__title {
        background: #376ecc;
        text-align: center;
        font-size: 20px;
        color: white;
        padding: 15px;
      }

      .home-table__text {
        text-align: center;
        font-size: 20px;
        padding: 10px;
      }
    }
  }
}
</style>
