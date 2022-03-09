<template>
  <div id="birthday" aria-label="Please enter date of birth">
    <fieldset 
    id="months" 
    aria-label="Select a month" 
    :dateSelected="this.dateSelected">

      <label class="uppercase">Month</label>
      <label for="monthList">Select a month</label>
      <div id="monthList">
        <input
          type="button"
          class="month"
          :aria-label="month.longText"
          :class="{ active: monthSelected === month.text}"
          v-for="month in months"
          :key="month.text" 
          :value="month.text"
          v-on:click="selectedMonth(month)"
        >
      </div>
    </fieldset>

    <fieldset 
    id="days" 
    aria-label="Select a day" 
    v-if="this.monthSelected" 
    :dateSelected="this.dateSelected">

      <label class="uppercase">Day</label>
      <label for="dayList">Select a day</label>
      <div id="dayList">
        <input 
          type="button"
          class="day"
          :aria-label="day"
          :class="{ active: daySelected === day}"
          v-for="day in displayDays"
          :key="day" 
          :value="day"
          v-on:click="selectedDay(day)"
        >
      </div>
    </fieldset>

    <fieldset 
    id="year" 
    aria-label="Input year" 
    v-if="this.monthSelected && this.daySelected" 
    :dateSelected="this.dateSelected"
    >
      <label class="uppercase">Input Year</label>
      <label aria-label="Four Digit Year">Four Digit YYYY</label>
      <input
        type="text"
        id="dobYear"
        name="year"
        maxlength="4"
        :value="year"
        aria-label="Four Digit Year"
      >
    </fieldset>

  </div>
</template>

<script>
  export default {
    name: 'BirthdayComp',
    data() {
        return {
            months: [
                { text: 'Jan', value: '01', longText: 'January' },
                { text: 'Feb', value: '02', longText: 'February' },
                { text: 'Mar', value: '03', longText: 'March' },
                { text: 'Apr', value: '04', longText: 'April' },
                { text: 'May', value: '05', longText: 'May' },
                { text: 'Jun', value: '06', longText: 'June' },
                { text: 'Jul', value: '07', longText: 'July' },
                { text: 'Aug', value: '08', longText: 'August' },
                { text: 'Sep', value: '09', longText: 'September' },
                { text: 'Oct', value: '10', longText: 'October' },
                { text: 'Nov', value: '11', longText: 'November' },
                { text: 'Dec', value: '11', longText: 'December' }
            ],
            days: [],
            year: '',
            birthday: ['', '', '',],
            month: null,
            
            monthSelected: false,
            daySelected: false,
            yearSelected: false,

            birthMonth:'',
            birthDate:'',
            birthYear: ''
        }
    },
    methods: {
      selectedMonth(month) {
          // console.log('clicked '+ month);
          this.birthday[0] = month.value; // returns month digital value
          this.birthday[1] = '';
          this.monthSelected = month.text; // adds active class to individual month input select
          console.log(this.birthday);
          this.month = month.text; // returns month textual value which should be used for the computed property below on toggling the appropriate # of days!
      },
      selectedDay(day) {
          // console.log('clicked '+ day);
          this.birthday[1] = day;
          this.daySelected = day; // adds active class to individual day input select
          console.log(this.birthday);
          this.birthDay = day;
      },
      selectedYear(year) {
          // console.log('clicked '+ day);
          this.birthday[1] = year;
          this.yearSelected = year; // adds active class to individual day input select
          console.log(this.birthday);
          this.birthYear = year;
      },
      submittedYear(year) {
          this.birthday[2] = year;
          console.log(this.birthday);
      },
      selectMonth (month, index) {
        this.form.month = this.form.month ? null : month;
        this.monthIndex = this.monthSelected ? null : index;
        this.monthSelected = !this.monthSelected; // boolean
      },
      selectDate (date) {
        this.form.day = this.form.day ? null : date;
        this.dateSelected = !this.dateSelected; // boolean
      },
      updateYear (year) {
        this.form.year = year || null;
        this.yearSelected = !!year.length; // boolean?
      }
    },
    computed: {
        displayDays() {
            if (this.month === 'Feb') {
                return ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10',
                    '11', '12', '13', '14', '15', '16', '17', '18', '19', '20',
                    '21', '22', '23', '24', '25', '26', '27', '28', '29']
            } else if (this.month === 'Apr' || this.month === 'Jun' || this.month === 'Sep' || this.month === 'Nov') {
                return ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10',
                    '11', '12', '13', '14', '15', '16', '17', '18', '19', '20',
                    '21', '22', '23', '24', '25', '26', '27', '28', '29', '30']
            } else {
                return ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10',
                    '11', '12', '13', '14', '15', '16', '17', '18', '19', '20',
                    '21', '22', '23', '24', '25', '26', '27', '28', '29', '30', '31']
            }
        }
    }
}

</script>

<style scoped>
#birthday {
  max-width: 420px;
}

#months, #days, #year {
    border: 0.125rem solid #e5e5e5;
    border-radius: 0.5rem;
    margin-bottom: 0.625rem;
}

#months > div, #days > div, #year {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  gap: 0.75rem 0.4375rem;
  justify-content: center;
  padding: 10% 11% 10%;
  box-sizing: border-box;
}

input {
  text-align: center;
  width: 5.0625rem;
  height: 2.625rem;
  background: #fff;
  border-radius: 6.25rem;
  border: 0.125rem solid #5500B3;
  line-height: 2.4rem;
}

#days > div {
  justify-content: left;
}

#days > div > input {
  border-radius: 10rem;
  width: 2.625rem;
}

#months > div > input:hover, #days > div > input:hover {
  cursor: pointer;
  background: #efefef;
}

#year input {
  font-size: 1.125rem;
  font-weight: 400;
  border: #ececec;
  box-sizing: border-box;
  padding: 0.3125rem 0.875rem 0rem;
  background: #ececec solid;
  border-radius: 0.625rem;
  height: 3.75rem;
  border-style: none;
  width: 80%;
}

.uppercase {
  text-transform: uppercase;
}

.month.active,
.day.active {
  background: rgba(85,0,179,.5);
  color: #fff;
}

#year > input {
  border: 0.125rem solid #5500B3; 
}
</style>