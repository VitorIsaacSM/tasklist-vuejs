<template>
  <div class="list">
    <div
      v-for="(task, index) in tasks"
      class="task"
      :class="{ done: !task.active }"
      :key="index"
      @click="toggleTaskActive(index)"
    >
      <i
        @click="
          removeTask(index);
          $event.stopPropagation();
        "
        class="fas fa-times remove"
      ></i>
      <h4>{{ task.text }}</h4>
    </div>
  </div>
</template>

<script>
export default {
  name: "Tasklist",
  props: ["tasks"],
  methods: {
    toggleTaskActive(index) {
      this.$emit("eventToggle", index);
    },
    removeTask(index) {
      this.$emit("eventRemove", index);
    }
  }
};
</script>

<style scoped lang="scss">
.list {
  width: 100%;
  max-width: 90vw;
  margin: 0 auto;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;

  .task {
    padding: 25px 50px;
    color: white;
    border-radius: 12px;
    background-color: tomato;
    margin-right: 20px;
    margin-bottom: 15px;
    position: relative;
    transition: background-color 0.3s ease;
    cursor: pointer;
    max-width: 22vw;
    word-break: break-word;

    &.done {
      background-color: green;
      text-decoration: line-through;
    }
  }

  .remove {
    position: absolute;
    top: 8px;
    right: 5px;
    transition: color 0.2s ease, transform 0.2s ease;
    color: rgba(white, 0.5);
    cursor: pointer;
    font-size: 1.2rem;
    width: 20px;
    height: 20px;

    &:hover {
      transform: scale(1.1);
      color: white;
    }
  }
}
</style>
