<script>
export default {
  data() {
    return {
      timer: [],
      isActive: false
    }
  },
  methods: {
    handleStart(index) {
      console.log(index)

      this.timer[index].isActive = !this.timer[index].isActive
      console.log(this.timer[index].isActive)
      if (this.timer[index].isActive) {
        this.timer[index].interval = setInterval(() => {
          if (this.timer[index].seconds >= 60) {
            this.timer[index].seconds = 0
            this.timer[index].minutes++
          }
          if (this.timer[index].minutes > 60) {
            this.timer[index].minutes = 0
            this.timer[index].hours++
          }

          this.timer[index].seconds++
        }, 1000)
      } else {
        clearInterval(this.timer[index].interval)
        return (this.timer[index].isActive = false)
      }
    },
    handleREset(index) {
      this.timer[index].seconds = 0
      this.timer[index].minutes = 0
      this.timer[index].hours = 0
      this.timer[index].isActive = false
      return clearInterval(this.interval)
    },
    addTimer() {
      this.timer.push({
        seconds: 0,
        minutes: 0,
        hours: 0,
        isActive: false,
        interval: ''
      })
    }
  },
  computed: {
    activePalyIcon() {
      return 'assets/pauseActive.svg'
    },
    inActivePalyIcon() {
      return 'assets/play.svg'
    },
    activeResetIcon() {
      return 'assets/resetActive.svg'
    },
    inActiveResetIcon() {
      return 'assets/reset.svg'
    }
  }
}
</script>

<template>
  <main class="main">
    <div class="container">
      <div class="timer-container">
        <div class="timer" v-for="(item, index) in timer" :key="index">
          <div :class="timer[index].isActive ? 'time Active ' : 'time'">
            <div class="hours" v-if="item.hours">{{ item.hours }}:</div>
            <div class="minutes" v-if="item.minutes">{{ item.minutes }}:</div>
            <div class="seconds">{{ item.seconds }}</div>
          </div>
          <div class="divider"></div>
          <div class="controllers">
            <div class="start" @click="handleStart(index)">
              <img :src="timer[index].isActive ? activePalyIcon : inActivePalyIcon" />
            </div>
            <div class="reset" @click="handleREset(index)">
              <img :src="timer[index].isActive ? activeResetIcon : inActiveResetIcon" />
            </div>
          </div>
        </div>
        <div class="Addtimer" @click="addTimer">
          <div class="AddtimerPlus"><img width="20" src="./assets/plus.svg" /></div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.main {
  background-color: #353638;
  height: 100vh;
}
.container {
  max-width: 1280px;
  margin: auto;
}
.divider {
  width: 100%;
  display: block;
  height: 1px;
  background-color: #ffffff;
}
.timer-container {
  width: 100%;

  display: flex;
  flex-wrap: wrap;
  align-items: start;
  gap: 15px;
}
.timer,
.Addtimer {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  margin-top: 20px;
  width: 225px;
  height: 120px;
  background-color: #696969;
}
.time {
  display: flex;
  justify-content: center;

  font-size: 22px;
  color: #9e9e9e;
}
.controllers {
  display: flex;
  justify-content: center;
  gap: 50px;
}
.start,
.reset {
  cursor: pointer;
}
.Active {
  color: #ffffff;
}
.AddtimerPlus {
  margin: auto;
  cursor: pointer;
}
</style>
