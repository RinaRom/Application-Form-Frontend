<template>
  <div class="wrapper">
    <div class="box">
      <h1 class="box__title">Подача заявки</h1>
      <form class="box__form" @submit.prevent="create">
        <input
          class="box-form__input"
          placeholder="Имя"
          type="text"
          v-model="name"
          required
        />
        <input
          class="box-form__input"
          placeholder="Фимилия"
          type="text"
          v-model="last_name"
          required
        />
        <input
          class="box-form__input"
          placeholder="Телефон"
          type="text"
          pattern="\+7[0-9]{10}"
          v-model="phone"
          required
        />
        <input
          class="box-form__input"
          placeholder="Email"
          type="email"
          v-model="email"
          required
        />
        <button class="box-form__button" type="submit">Отправить</button>
      </form>
    </div>
  </div>
</template>

<script>
import { api_url } from "@/config/config";

export default {
  name: "FormView",
  data: () => {
    return {
      name: "",
      last_name: "",
      phone: "",
      email: "",
    };
  },
  methods: {
    create() {
      fetch(api_url + "/api/v1/application", {
        method: "POST",
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
        body: new URLSearchParams({
          name: this.name,
          last_name: this.last_name,
          phone: this.phone,
          email: this.email,
        }),
      }).then(() => {
        this.$router.push("/");
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  .box {
    display: flex;
    flex-direction: column;
    border: 2px solid #376ecc;
    border-radius: 18px;
    padding: 26px;
    background: aliceblue;
    width: 40%;
    .box__title {
      font-weight: 700;
      font-size: 36px;
      line-height: 72px;
      color: #212b27;
    }
    .box__form {
      display: flex;
      flex-direction: column;

      .box-form__input {
        background: #ffffff;
        border: 1px solid rgba(0, 0, 0, 0.1);
        border-radius: 15px;
        font-family: "Karla", sans-serif;
        padding: 22px 26px;
        margin-bottom: 16px;
        width: 100%;
      }
      .box-form__button {
        background: #376ecc;
        border-radius: 23px;
        font-family: "Karla", sans-serif;
        font-weight: 400;
        font-size: 24px;
        line-height: 44px;
        color: #ffffff;
        padding: 12px 16px;
        text-align: center;
        cursor: pointer;
        margin-bottom: 15px;
      }
    }
  }
}
</style>
