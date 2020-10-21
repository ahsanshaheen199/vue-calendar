<template>
  <h2>Calendar</h2>
  <div class="calendar-wrap">
      <h2>{{currentMonthName}} {{currentYear}}</h2>
      <div class="days-wrapper">
          <div v-for="day in days" :key="day">{{day}}</div>
      </div>
      <div class="days-wrapper">
          <div v-for="date in startDay" :key="date"></div>
          <div v-for="date in daysInMonth" :key="date">{{date}}</div>
      </div>
      <div class="arrow-wrapper">
          <button @click="prev">Previous</button>
          <button @click="next">Next</button>
      </div>
  </div>
</template>

<script>
export default {
    name: 'Calendar',
    data() {
        return {
            days: ['sun','mon','tues','wed','thu','fri','sat'],
            currentMonth: new Date().getMonth(),
            currentYear: new Date().getFullYear()
        }
    },
    methods: {
        prev() {
            if( this.currentMonth === 0 ) {
                this.currentYear--;
                this.currentMonth = 11;
            } else {
                this.currentMonth--;
            }
        },
        next() {
            if( this.currentMonth === 11 ) {
                this.currentMonth = 0;
                this.currentYear++;
            } else {
                this.currentMonth++;
            }
        }
    },
    computed: {
        daysInMonth() {
            const month = new Date().getMonth();
            const year = new Date().getFullYear();

            const count = new Date(this.currentYear,this.currentMonth + 1,0).getDate();

            return count;
        },
        startDay() {
            return new Date(this.currentYear, this.currentMonth, 1).getDay();
        },
        currentMonthName() { return new Date(this.currentYear,this.currentMonth ).toLocaleString("default", { month: "long" }) }
    }
}
</script>

<style>

</style>