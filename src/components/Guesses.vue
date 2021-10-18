<template>
  <div>
    <h3 v-if="remarks">{{ remarks }}</h3>

    <p>No. of guesses: {{ guesses.length }}</p>

    <p>
      Guessed numbers are:
      <el-tag
        v-for="guess in guesses"
        :key="guess.id"
        :type="guess.isCorrect ? 'success' : 'danger'"
        effect="dark"
        class="tags"
        >{{ guess.number }}</el-tag
      >
    </p>
  </div>
</template>

<script>
export default {
  props: ["randomNumber", "guesses"],
  computed: {
    remarks() {
      let remarks = null;

      const length = this.guesses.length;
      if (length > 0) {
        if (this.guesses[length - 1].number === this.randomNumber) {
          remarks = "Yippie You Win!";
        } else if (this.guesses[length - 1].number > this.randomNumber) {
          remarks = "Your guess is too high.";
        } else if (this.guesses[length - 1].number < this.randomNumber) {
          remarks = "Your guess is too low.";
        }
      }

      return remarks;
    },
  },
};
</script>

<style scoped>
div {
  margin-top: 30px;
}
.tags {
  margin-left: 10px;
  margin-bottom: 10px;
  font-weight: 600;
}
</style>
