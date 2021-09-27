<template>
  <div class="bg-bantinh">
    <div class="text-center mb-4">
      <button class="load-ban-tinh" @click="reLoad">
        <img src="/load.png" alt="">
      </button>
    </div>
    <div class="text-center text-white result">
      {{ count }}
    </div>
    <div class="soroban flex">
      <div class="bg-col-left" />
      <div v-for="i in hanghat" :key="i" class="hanghat" :class="`hanghat-${hanghat + 1 - i}`">
        <div :id="`hat-five-${i}`" class="hat-five" @click="runSeedFive($event)" />
        <div :id="`hat-one-${i}`" class="hat-one">
          <div :id="`one-1-${i}`" class="one-1" @click="runSeedOne($event)" />
          <div :id="`one-2-${i}`" class="one-2" @click="runSeedOne($event)" />
          <div :id="`one-3-${i}`" class="one-3" @click="runSeedOne($event)" />
          <div :id="`one-4-${i}`" class="one-4" @click="runSeedOne($event)" />
        </div>
      </div>
      <div class="bg-col-right" />
    </div>
  </div>
</template>

<script>
import { calculate, calculateFive } from '~/utils/calculate'

function addClass (element, className) {
  element.classList.add(className)
};
function removeClass (element, className) {
  element.classList.remove(className)
};
export default {
  data () {
    return {
      count: 0,
      hanghat: 8,
      d: 0
    }
  },
  methods: {
    hasClass (element, className) {
      do {
        if (element.classList && element.classList.contains(className)) {
          return true
        }
        element = element.parentNode
      } while (element)
      return false
    },
    runSeedFive (event) {
      const element = document.getElementById(event.currentTarget.id)
      const nameClassParent = element.parentNode.classList[1]
      if (this.hasClass(element, 'active-hat-five') === false) {
        addClass(element, 'active-hat-five')
        this.count += calculateFive(nameClassParent)
      } else {
        removeClass(element, 'active-hat-five')
        this.count -= calculateFive(nameClassParent)
      }
    },
    runSeedOne (event) {
      const element = document.getElementById(event.currentTarget.id)
      const elementParent = document.getElementById(element.parentNode.id)
      const nameClassParent = elementParent.parentNode.classList[1]
      switch (event.toElement.classList[0]) {
        case 'one-1':
          if (this.hasClass(elementParent, 'active-1') === false) {
            addClass(elementParent, 'active-1')
            this.count += calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-4') === true) {
            removeClass(elementParent, 'active-1')
            removeClass(elementParent, 'active-2')
            removeClass(elementParent, 'active-3')
            removeClass(elementParent, 'active-4')
            this.count -= calculate(nameClassParent)
            this.count -= calculate(nameClassParent)
            this.count -= calculate(nameClassParent)
            this.count -= calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-3') === true) {
            removeClass(elementParent, 'active-1')
            removeClass(elementParent, 'active-2')
            removeClass(elementParent, 'active-3')
            this.count -= calculate(nameClassParent)
            this.count -= calculate(nameClassParent)
            this.count -= calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-2') === true) {
            removeClass(elementParent, 'active-1')
            removeClass(elementParent, 'active-2')
            this.count -= calculate(nameClassParent)
            this.count -= calculate(nameClassParent)
          } else {
            removeClass(elementParent, 'active-1')
            this.count -= calculate(nameClassParent)
          }
          if (this.hasClass(elementParent, 'active-1') === true && this.d === 0) {
            this.count = 0
            this.d++
          }
          break

        case 'one-2':
          if (this.hasClass(elementParent, 'active-4') === true) {
            removeClass(elementParent, 'active-2')
            removeClass(elementParent, 'active-3')
            removeClass(elementParent, 'active-4')
            this.count -= calculate(nameClassParent)
            this.count -= calculate(nameClassParent)
            this.count -= calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-3') === true) {
            removeClass(elementParent, 'active-2')
            removeClass(elementParent, 'active-3')
            this.count -= calculate(nameClassParent)
            this.count -= calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-2') === true) {
            removeClass(elementParent, 'active-2')
            this.count -= calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-1') === false) {
            addClass(elementParent, 'active-1')
            addClass(elementParent, 'active-2')
            this.count += calculate(nameClassParent)
            this.count += calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-1') === true) {
            addClass(elementParent, 'active-2')
            this.count += calculate(nameClassParent)
          }
          if (this.hasClass(elementParent, 'active-1') === true && this.d === 0) {
            this.count = 0
            this.d++
          }
          if (this.hasClass(elementParent, 'active-2') === true && this.d === 0) {
            this.count = 0
            this.d++
          }
          break
        case 'one-3':
          if (this.hasClass(elementParent, 'active-4') === true) {
            removeClass(elementParent, 'active-3')
            removeClass(elementParent, 'active-4')
            this.count -= calculate(nameClassParent)
            this.count -= calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-2') === true && this.hasClass(elementParent, 'active-3') === false) {
            addClass(elementParent, 'active-3')
            this.count += calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-1') === false) {
            addClass(elementParent, 'active-3')
            addClass(elementParent, 'active-1')
            addClass(elementParent, 'active-2')
            this.count += calculate(nameClassParent)
            this.count += calculate(nameClassParent)
            this.count += calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-2') === false && this.hasClass(elementParent, 'active-1') === true) {
            addClass(elementParent, 'active-2')
            addClass(elementParent, 'active-3')
            this.count += calculate(nameClassParent)
            this.count += calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-2') === true && this.hasClass(elementParent, 'active-3') === false) {
            addClass(elementParent, 'active-3')
            this.count += calculate(nameClassParent)
          } else {
            removeClass(elementParent, 'active-3')
            this.count -= calculate(nameClassParent)
          }
          if (this.hasClass(elementParent, 'active-3') === true && this.d === 0) {
            this.count = 0
            this.d++
          }
          break
        case 'one-4':
          if (this.hasClass(elementParent, 'active-1') === false) {
            addClass(elementParent, 'active-1')
            addClass(elementParent, 'active-2')
            addClass(elementParent, 'active-3')
            addClass(elementParent, 'active-4')
            this.count += calculate(nameClassParent)
            this.count += calculate(nameClassParent)
            this.count += calculate(nameClassParent)
            this.count += calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-2') === false) {
            addClass(elementParent, 'active-2')
            addClass(elementParent, 'active-3')
            addClass(elementParent, 'active-4')
            this.count += calculate(nameClassParent)
            this.count += calculate(nameClassParent)
            this.count += calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-3') === false) {
            addClass(elementParent, 'active-3')
            addClass(elementParent, 'active-4')
            this.count += calculate(nameClassParent)
            this.count += calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-4') === false) {
            addClass(elementParent, 'active-4')
            this.count += calculate(nameClassParent)
          } else if (this.hasClass(elementParent, 'active-3') === true) {
            removeClass(elementParent, 'active-4')
            this.count -= calculate(nameClassParent)
          }
          if (this.hasClass(elementParent, 'active-4') === true && this.d === 0) {
            this.count = 0
            this.d++
          }
          break
        default:
          break
      }
      if (this.hasClass(elementParent, 'active-1') === false && this.hasClass(elementParent, 'active-2') === false &&
      this.hasClass(elementParent, 'active-3') === false &&
      this.hasClass(elementParent, 'active-4') === false) { this.count = 0 }
    },
    reLoad () {
      const elementHatFive = document.getElementsByClassName('active-hat-five')
      elementHatFive.forEach((element) => {
        removeClass(element, 'active-hat-five')
        this.reLoad()
      })
      const elementHatOne1 = document.getElementsByClassName('active-1')
      elementHatOne1.forEach((element) => {
        removeClass(element, 'active-1')
        this.reLoad()
      })
      const elementHatOne2 = document.getElementsByClassName('active-2')
      elementHatOne2.forEach((element) => {
        removeClass(element, 'active-2')
        this.reLoad()
      })
      const elementHatOne3 = document.getElementsByClassName('active-3')
      elementHatOne3.forEach((element) => {
        removeClass(element, 'active-3')
        this.reLoad()
      })
      const elementHatOne4 = document.getElementsByClassName('active-4')
      elementHatOne4.forEach((element) => {
        removeClass(element, 'active-4')
        this.reLoad()
      })
      this.count = 0
    }
  }
}
</script>

<style>
</style>
