<template>
  <div class="container mt-3">
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
    return {};
  },
  methods: {
    deleteCustomer(id) {
      console.log(id);
      this.$emit("deleteCustomer", id);
    },
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
