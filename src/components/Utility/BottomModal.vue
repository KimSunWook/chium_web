<template lang="pug">
  div
    q-dialog(v-model="modal" position="bottom")
      q-card(class="bday-date-picker flex justify-center items-center" style="background-color: #F2F2F2")
        q-card-section
          div(class="row q-gutter-lg")
            div(class="col")
              div(class="column no-wrap q-gutter-lg  flex justify-center content-center items-center wheeler-year" v-touch-swipe.mouse="_ => onHandleSwipeWheel(_, 'startYearRange')" @wheel.prevent="onHandleScroll")
                div(
                  class="col text-subtitle1 no-padding date-wheel-val" 
                  style="transition: width 2s;transition-timing-function: ease;" 
                  v-for="year,index in yearRange" :class="{ 'text-grey-5': index === 0 }" 
                )
                  | {{ year }}

            div(class="col")
              div(class="column no-wrap q-gutter-lg  flex justify-center content-center items-center wheeler-year" v-touch-swipe.mouse="_ => onHandleSwipeWheel(_, 'startDayRange')" @wheel.prevent="onHandleScroll")
                div(class="col text-subtitle1 no-padding date-wheel-val" v-for="day,index in dayRange" :class="{ 'text-grey-5': index === 0 }" )
                  | {{ day < 10 ? '0'+day : day }}


            div(class="col")
              div(class="column no-wrap q-gutter-lg  flex justify-center content-center items-center wheeler-year" v-touch-swipe.mouse="_ => onHandleSwipeWheel(_, 'startMonthRange')" @wheel.prevent="onHandleScroll")
                div(class="col text-subtitle1 no-padding date-wheel-val" v-for="day,index in monthRange" :class="{ 'text-grey-5': index === 0 }" )
                  | {{ day < 10 ? '0'+day : day }}
</template>

<script>
import ModalMixins from 'src/mixins/ModalMixins'
import { each, isEqual, get, set } from 'lodash'

export default {
  props: {
    modal: {
      type: Boolean,
      default: false,
    }
  },
  data() {
    return {
      model: 0,
      startYearRange: 1980,
      startDayRange: 1,
      startMonthRange: 1,
      // yearMax(type) {
      //   switch (type) {
      //     case 'startYearRange': return [1980, ];
      //   }
      // },
    }
  },
  created() {
    // this.modal = this.openModal;
  },
  computed: {
    yearRange () {
      const ranges = [];
      for (let x = this.startYearRange; x <= this.startYearRange+1; x++) {
        ranges.push(x)
      }
      return ranges;
    },
    dayRange () {
      const ranges = [];
      for (let x = this.startDayRange; x <= this.startDayRange+1; x++) {
        ranges.push(x)
      }
      return ranges;
    },
    monthRange () {
      const ranges = [];
      for (let x = this.startMonthRange; x <= this.startMonthRange+1; x++) {
        ranges.push(x)
      }
      return ranges;
    },
   },
   methods: {
    onHandleSwipeWheel({ direction }, type, max = [0,0]) {
      console.log(direction);
      let range = get(this, type);
      if (isEqual(direction, 'up')) {
        if (range < new Date().getFullYear()) {
              range++;
              set(this, type, range);       
        }
      } else if(isEqual(direction, 'down')) {
          if (this.startYearRange > 1900) {
              range--;
              set(this, type, range);
          }
      }
    },
    onHandleScroll({ deltaY }) {
      if (this.startYearRange < new Date().getFullYear()) {  
        if (deltaY > 20) {
          this.startYearRange++;
        } 
         
      }
      if (this.startYearRange > 1900) {
        if (deltaY < -8) {
          this.startYearRange--;
        }
      }
    },
   },
  watch: {
    modal: {
      deep: true,
      handler(newVal) {
        console.log("newVal", newVal)
      },
    }
  },
}
</script>

<style lang="stylus">
  .bday-date-picker
    border-radius: 100px
    height: 268px 
    width: 375px

  .date-wheel-val
    font-family: 'notosanskr-medium'
    font-size: 30px
    -webkit-touch-callout: none
    -webkit-user-select: none
    -khtml-user-select: none
    -moz-user-select: none
    -ms-user-select: none
    user-select: none
  // .wheeler-year
  //   max-height: 30%
  //   overflow-y: scroll
</style>