<template>
  <div id="app">
    <h1>Tarefas</h1>
    <Percentage :tasks="tasks" />
    <InputTarefa @novaTarefa="adicionaTask($event)"/>
    <p @click="tasks = []" class="reset">Resetar Tarefas</p>
    <Tasklist
      @eventToggle="toggleTask($event)"
      @eventRemove="removeTask($event)"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import Tasklist from "./components/Tasklist";
import InputTarefa from "./components/InputTarefa";
import Percentage from "./components/Percentage";

export default {
  name: "App",
  components: { Tasklist, InputTarefa, Percentage },
  data() {
    return {
      tasks: []
    };
  },
  methods: {
    toggleTask(index) {
      this.tasks[index].active = !this.tasks[index].active;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    adicionaTask(text) {
      this.tasks.push({
        text,
        active: true
      })
    }
  },
  watch: {
    tasks(newTasks) {
      localStorage.tasks = JSON.stringify(newTasks);
    }
  },
  created() {
    this.tasks = localStorage.tasks ? JSON.parse(localStorage.tasks) : [];
  }
};
</script>

<style lang="scss">
body {
  font-family: "Lato", sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #fff;
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  padding-top: 100px;

  h1 {
    margin-bottom: 5px;
    font-weight: 300;
    font-size: 3rem;
  }

  p.reset {
    font-size: 1.2rem;
    text-decoration: underline;
    color: white;
    cursor: pointer;
    margin-bottom: 25px;

    &:hover {
      color: dodgerblue;
    }
  }
}
</style>
