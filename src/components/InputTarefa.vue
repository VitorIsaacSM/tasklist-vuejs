<template>
  <form
    @submit="
      criaNovaTarefa();
      $event.preventDefault();
    "
  >
    <div class="input-tarefa">
      <input type="text" v-model="novaTarefa" />
      <button type="submit">
        + Tarefa
      </button>
    </div>
  </form>
</template>

<script>
export default {
  name: "InputTarefa",
  data() {
    return {
      novaTarefa: ""
    };
  },
  methods: {
    criaNovaTarefa() {
      if (!this.novaTarefa) {
        return;
      }
      this.$emit("novaTarefa", this.novaTarefa);
      this.novaTarefa = "";
    }
  }
};
</script>

<style scoped lang="scss">
form {
  width: 100%;
  display: flex;
  justify-content: center;

  div.input-tarefa {
    max-width: 50vw;
    width: 100%;
    margin: 40px 20px;
    margin-bottom: 10px;
    display: flex;
    border-radius: 10px;

    input {
      flex: 1;
      border-radius: 10px 0 0 10px;
      padding: 8px 20px;
      background-color: rgba(255, 255, 255, 0.05);
      border: 1px solid white;
      color: white;
      font-size: 15px;

      &:focus {
        outline: none;
      }
    }

    button {
      border-radius: 0 10px 10px 0;
      padding: 8px 40px;
      background-color: dodgerblue;
      color: white;
      border: 1px solid white;
      font-size: 25px;
      cursor: pointer;

      &:hover {
        outline: none;
        background-color: rgba(dodgerblue, 0.5);
      }
    }
  }
}
</style>