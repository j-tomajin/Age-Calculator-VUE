<script>
  import DateField from './components/DateField.vue';
  import UserAge from './components/UserAge.vue';

  export default {
    name: 'App',
    components: {
      DateField,
      UserAge,
    },
    data: function() {
      return {
        daysOld: 0,
        monthsOld: 0,
        yearsOld: 0,
      }
    },
    methods: {
      checkDate: function(day, month, year) {
        // setting input into birthday
        let birthday = `${month}/${day}/${year}`
        // setting the input birthday into new Date
        let birthdayObj = new Date(birthday)

        // calculate the difference between the date now and the birthday
        let calcAge = Date.now() - birthdayObj
        
        // setting the difference date into new Date
        let ageDate = new Date(calcAge)
        
        // setting each date 
        this.yearsOld = ageDate.getFullYear() - 1970 //
        this.monthsOld = ageDate.getMonth()
        this.daysOld = ageDate.getDate() - 1
      }
    },
  }

</script>

<template>
  <main class="main">
    <DateField
      @check-date="checkDate" />

    <UserAge 
      :yearsOld="yearsOld"
      :monthsOld="monthsOld"
      :daysOld="daysOld"
    />
  </main>
</template>

<style lang="scss">
  @use './assets/scss/utilities' as *;

  body {
    padding-block: clampf(80, 780, 160);
  }

  .main {
    padding: clampf(24, 780, 56);
  }
</style>
