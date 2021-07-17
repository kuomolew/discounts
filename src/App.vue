<template>
  <AddCard @newCustomer="addNewCard($event)" />
  <ShowCards />

  <br /><br />
  <div class="container">
    <p @click="clearLocalStorage">Снести все кхуям</p>
  </div>
</template>

<script>
import AddCard from "./components/AddCard.vue";
import ShowCards from "./components/ShowCards.vue";

export default {
  name: "App",
  components: {
    AddCard,
    ShowCards,
  },
  data() {
    return {
      dataBase: [],
    };
  },
  methods: {
    getDataBase() {
      console.log("Get db");
      if (window.localStorage.getItem("discountsDatabase")) {
        this.dataBase = JSON.parse(
          window.localStorage.getItem("discountsDatabase")
        );
      }
      console.log(this.dataBase);
    },
    setDataBase() {
      window.localStorage.setItem(
        "discountsDatabase",
        JSON.stringify(this.dataBase)
      );
    },
    addNewCard(customer) {
      this.dataBase.push(customer);
      this.setDataBase();
    },
    clearLocalStorage() {
      this.dataBase = [];
      this.setDataBase();
    },
  },
  created() {
    this.getDataBase();
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

@import "~bootstrap/dist/css/bootstrap.css";
</style>
