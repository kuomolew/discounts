<template>
  <div v-if="areCards" class="container mt-3">
    <div class="row">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Номер карты</th>
            <th scope="col">Номер Телефона</th>
            <th scope="col">Имя</th>
            <th scope="col">Удалить</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(customer, index) in customers" :key="index">
            <th scope="row">{{ index + 1 }}</th>
            <td>{{ customer.cardId }}</td>
            <td>{{ customer.phoneNumber }}</td>
            <td>{{ customer.name }}</td>
            <td>
              <img
                src="../assets/delete.png"
                alt="Удалить"
                class="delete-icon"
                @click="deleteCustomer(customer.cardId)"
              />
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  <div v-else class="container mt-5">
    <p>Карты не найдены</p>
  </div>
</template>

<script>
export default {
  name: "ShowCards",
  props: {
    customers: {
      type: Object,
    },
  },
  data() {
    return {
      areCards: false,
    };
  },
  methods: {
    deleteCustomer(id) {
      console.log(id);
      this.$emit("deleteCustomer", id);
    },
    checkCards() {
      this.customers.length ? (this.areCards = true) : (this.areCards = false);
    },
  },
  mounted() {
    this.checkCards();
  },
  updated() {
    this.checkCards();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.delete-icon {
  height: 20px;
  width: auto;
  cursor: pointer;
}
</style>
