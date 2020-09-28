<template>
  <div class="container">
      <stopwatch v-for="i in countStopwatches" :key="i" />
      <div @click="add">
          <addstopwatch/>
      </div>
  </div>
</template>

<script>
import stopwatch from './stopwatch';
import addstopwatch from './addstopwatch';

export default {
    name: 'container',
    data: () => ({
        countStopwatches: 4
    }),
    components: {
        stopwatch,
        addstopwatch
    },
    methods: {
        add() {
            this.countStopwatches++
        }
    }
}
</script>

<style>
.container {
    margin: auto;
    margin-top: 47px;
    display: flex;
    flex-wrap: wrap;
}
@media (max-width: 767px) {
  .container {
    flex-direction: column;
    align-content: center;
  }
}
@media (min-width: 768px) and (max-width: 1023px) {
  .container {
    width: 550px;
    flex-direction: row;
  }
}
@media (min-width: 1024px) {
  .container {
    width: 825px;
    flex-direction: row;
  }
}
</style>