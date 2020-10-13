<template>
  <div class="barra">
    <div class="complete" :style="{ width: completePercentage + '%' }"></div>
    <p>{{ completePercentage }} %</p>
  </div>
</template>

<script>
export default {
  name: "Percentage",
  props: ["tasks"],
  computed: {
    completePercentage() {
      if (!this.tasks || !this.tasks.length) {
        return 0;
      }
      let tarefasCompletas = 0;
      this.tasks.forEach(t => (!t.active ? tarefasCompletas++ : null));

      return Math.floor((tarefasCompletas / this.tasks.length) * 100);
    }
  }
};
</script>

<style scoped lang="scss">
div.barra {
  max-width: 50vw;
  width: 100%;
  margin: 40px 20px;
  display: flex;
  justify-content: center;
  border-radius: 10px;
  border: 1px solid white;
  background-color: transparent;
  text-align: center;
  position: relative;

  div.complete {
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    background-color: green;
    z-index: 1;
    border-radius: 10px;
    transition: width 0.3s ease;
  }

  p {
    z-index: 2;
    margin: 14px;
  }
}
</style>