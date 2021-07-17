<template>
  <div class="container">
    <button
      v-if="buttonMode"
      @click="toggleView"
      type="button"
      class="btn btn-primary"
    >
      Добавить карту
    </button>

    <div class="row">
      <div class="col">
        <h4>Номер карты</h4>
        <input type="text" placeholder="Карта" />
      </div>
      <div class="col">
        <h4>Номер телефона</h4>
        <input type="text" placeholder="Телефон" />
      </div>
      <div class="col">
        <h4>Имя владельца</h4>
        <input type="text" placeholder="Имя" />
      </div>
    </div>
    <br />
    <div class="row">
      <div class="col">
        <button ttype="button" class="btn btn-success">Добавить карту</button>
      </div>
      <div class="col">
        <button type="button" class="btn btn-secondary">Очистить данные</button>
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
    };
  },
  methods: {
    toggleView() {
      this.buttonMode = !this.buttonMode;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
