<template>
  <AddCard @newCustomer="addNewCustomer($event)" />
  <div class="container mt-3">
    <h3>Введите номер телефона, карты или имя для поиска</h3>
    <input type="text" placeholder="Жду..." v-model="search" />
    <ShowCards
      :customers="customers"
      @deleteCustomer="deleteCustomer($event)"
    />
  </div>
  <div class="container">
    <br /><br />
    <p @click="clearLocalStorage" class="pointer">
      Удалить все внесенные в базу карты
    </p>
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
      customers: [],
      search: "",
    };
  },
  methods: {
    getDataBase() {
      if (window.localStorage.getItem("discountsDatabase")) {
        this.dataBase = JSON.parse(
          window.localStorage.getItem("discountsDatabase")
        );
      }
    },
    setDataBase() {
      window.localStorage.setItem(
        "discountsDatabase",
        JSON.stringify(this.dataBase)
      );
    },
    addNewCustomer(customer) {
      this.dataBase.push(customer);
      this.setDataBase();
      this.createCustomersList();
    },
    deleteCustomer(id) {
      for (let index in this.dataBase) {
        if (this.dataBase[index].cardId == id) {
          this.dataBase.splice(index, 1);
        }
      }
      this.setDataBase();
      this.createCustomersList();
    },
    createCustomersList() {
      if (!this.search) {
        this.customers = this.dataBase.slice();
      } else {
        this.customers = this.dataBase.filter((customer) => {
          if (
            customer.phoneNumber.indexOf(this.search) != -1 ||
            customer.cardId.indexOf(this.search) != -1 ||
            customer.name.indexOf(this.search) != -1
          ) {
            return customer;
          }
        });
      }
    },
    clearLocalStorage() {
      this.dataBase = [];
      this.setDataBase();
      this.createCustomersList();
    },
  },
  created() {
    this.getDataBase();
    this.createCustomersList();
  },
  watch: {
    search(val) {
      this.createCustomersList();
    },
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

.pointer {
  cursor: pointer;
}

@import "~bootstrap/dist/css/bootstrap.css";
</style>
