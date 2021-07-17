<template>
  <div v-if="buttonMode" class="container">
    <button @click="toggleView" type="button" class="btn btn-primary">
      Добавить карту
    </button>
  </div>
  <div v-else class="container mb-5">
    <div class="row">
      <div class="col">
        <h4>Номер карты</h4>
        <input type="text" placeholder="Карта" v-model="cardId" />
      </div>
      <div class="col">
        <h4>Номер телефона</h4>
        <input type="text" placeholder="Телефон" v-model="phoneNumber" />
      </div>
      <div class="col">
        <h4>Имя владельца</h4>
        <input type="text" placeholder="Имя" v-model="name" />
      </div>
    </div>
    <br />
    <div class="row">
      <div class="col">
        <button
          @click="sendNewCard"
          type="button"
          class="btn btn-success"
          :disabled="isAddButtonDisabled()"
        >
          Добавить карту
        </button>
      </div>
      <div class="col">
        <button @click="clearInputs" type="button" class="btn btn-secondary">
          Очистить данные
        </button>
      </div>
      <div class="col">
        <button type="button" class="btn btn-danger" @click="toggleView">
          Отменить добавление
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddCard",
  props: {},
  data() {
    return {
      buttonMode: true,
      cardId: "",
      phoneNumber: "",
      name: "",
      isAddingDisabled: true,
    };
  },
  methods: {
    toggleView() {
      this.buttonMode = !this.buttonMode;
    },
    sendNewCard() {
      let customer = this.createCustomer();
      this.$emit("newCustomer", customer);
      this.clearInputs();
      this.toggleView();
    },
    createCustomer() {
      return {
        cardId: this.cardId,
        phoneNumber: this.phoneNumber,
        name: this.name,
      };
    },

    clearInputs() {
      this.cardId = "";
      this.phoneNumber = "";
      this.name = "";
    },
    abortAdding() {
      this.clearInputs;
      this.toggleView();
    },

    isAddButtonDisabled() {
      if (this.cardId && this.phoneNumber && this.name) {
        return false;
      }
      return true;
    },
  },
  computed: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
