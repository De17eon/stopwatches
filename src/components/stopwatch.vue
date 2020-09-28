<template>
  
  <div class="stopwatch">
    <div class="stopwatch__time" :class="{'stopwatch__time-active': isActive}">
      <p>{{ stopwatchTime }}</p>
    </div>
    <div class="stopwatch__btns">
      <button v-if="!isActive" class="btnsvg btn-left" @click.prevent="run">
        <!-- Треугольник -->
        <svg class="svg" :class="{'svg-active': isActive}" width="17" height="20" viewBox="0 0 17 20" xmlns="http://www.w3.org/2000/svg">
          <path d="M0 20V0L17 10L0 20Z"/>
        </svg>
      </button>

      <button v-else class="btnsvg btn-left"  @click.prevent="fix">
        <!-- Пауза. Две вертикальные палочки -->
        <svg class="svg" :class="{'svg-active': isActive}" width="10" height="20" viewBox="0 0 10 20"  xmlns="http://www.w3.org/2000/svg">
          <rect x="7" width="3" height="20" />
          <rect width="3" height="20" />
        </svg>
      </button>

      <button class="btnsvg btn-rigth"  @click.prevent="reset">
        <!-- Квадрат -->
        <svg class="svg" :class="{'svg-active': isActive}" width="20" height="20" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
          <rect width="20" height="20"/>
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Stopwatch',
  data: () => ({
    isActive: false,
    startTime: null,
    elapsedTime: null,
    fixedTime: null,
    requestAnimationId: null,
  }),
  computed: {
    stopwatchTime() {

      if (this.elapsedTime) {
        const seconds = this.elapsedTime.getUTCSeconds().toString()
        const minutes = this.elapsedTime.getUTCMinutes().toString()
        const hours = this.elapsedTime.getUTCHours().toString()

        if (hours > 0) {
          let result = hours + ':'
          result += (minutes < 10 ? '0' + minutes + ':' : minutes + ':')
          result += (seconds < 10 ? '0' + seconds : seconds)
          return result
        }

        if (minutes > 0) {
          let result = minutes + ':'
          result += (seconds < 10 ? '0' + seconds : seconds)
          return result
        }

        return seconds
      }

      return "0"
    }
  },
  methods: {
    tick() {
      this.elapsedTime = new Date((new Date).getTime() - this.startTime)
      this.requestAnimationId = requestAnimationFrame(this.tick)
    },
    run() {
      this.startTime = new Date((new Date).getTime() - this.fixedTime)
      this.fixedTime = null
      this.isActive = true
      this.requestAnimationId = requestAnimationFrame(this.tick)
    },
    fix() {
      cancelAnimationFrame(this.requestAnimationId)
      this.isActive = false
      this.startTime = null
      this.fixedTime = this.elapsedTime
    },
    reset() {
      cancelAnimationFrame(this.requestAnimationId)
      this.isActive = false
      this.startTime = null
      this.elapsedTime = null
      this.fixedTime = null
      this.requestAnimationId = null
    }
  }
}
</script>


<style>

.btnsvg {
  border: none;
  background: none;
}
.btn-left {
  position: absolute;
  top: 20px;
  left: 70px;
}
.btn-rigth {
  position: absolute;
  top: 20px;
  left: 135px;
}
.svg {
  fill: #9e9e9e;
}
.svg-active {
  fill: #eee;
}
/* .btnsvg:hover .svg {
  fill: #eee;
}
.btnsvg:hover .svg-active {
  fill: #9e9e9e;
} */


.stopwatch__status {
  position: absolute;
  width: 166px;
  height: 14px;
  left: 82px;
  top: 43px;
  font-family: Gotham Pro;
  font-style: normal;
  font-weight: normal;
  font-size: 15px;
  line-height: 14px;
  color: #696969;
}
.stopwatch {
  background-color: #696969;
  width: 225px;
  height: 120px;
  margin: 25px;
}
.stopwatch__time {
  height: 60px;
  width: 100%;
  display: flex;
  align-items: center;
}
.stopwatch__time {
  border-bottom: 1px solid #9E9E9E;
  justify-content: center;
}
.stopwatch__time-active {
  border-bottom: 1px solid #eee;
}
.stopwatch__btns {
  position:relative;
  width: 225px;
  height: 60px;
}
.stopwatch__time > p {
  font-family: Gotham Pro;
  font-style: normal;
  font-weight: normal;
  font-size: 22px;
  line-height: 21px;
  text-align: center;
  color: #9e9e9e;
}
.stopwatch__time-active > p {
 color: #eee;
}
@media (max-width: 320px) {
  .stopwatch {
    margin-top: 25px;
  }
}
</style>
