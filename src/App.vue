<template>
  <div class="app-box">
    <date-form
      @calcTheAge="calcTheAge"
    ></date-form>
    <!-- Age Display -->
    <div class="age-box">
      <h2 class="age-item">
        <span>{{ ageYear }}</span>years
      </h2>
      <h2 class="age-item">
        <span>{{ ageMonth }}</span>months
      </h2>
      <h2 class="age-item">
        <span>{{ ageDay }}</span>days
      </h2>
    </div>
  </div>
</template>

<script>
import DateForm from './components/DateForm.vue';
export default {
  components: {
    DateForm
  },
  data() {
    return {
      ageYear: '--',
      ageMonth: '--',
      ageDay: '--'
    }
  },
  methods: {
    calcTheAge(dob) {
      var today = new Date();
      var birthDate = new Date(dob);
      var age = today.getFullYear() - birthDate.getFullYear();
      var m = today.getMonth() - birthDate.getMonth();
      if (m < 0 || (m === 0 && today.getDate() < birthDate.getDate())) {
          age--;
      }
      var months = today.getMonth() - birthDate.getMonth();
      if (months < 0) {
          months += 12;
      }
      var days = today.getDate() - birthDate.getDate();
      if (days < 0) {
          days += new Date(today.getFullYear(), today.getMonth(), 0).getDate();
          months--;
      }
      this.ageYear = age;
      this.ageMonth = months;
      this.ageDay = days;
    }
  }
}
</script>

<style scoped>
.app-box {
  background-color: var(--clr-white);
  padding: 70px;
  border-radius: 40px 40px 200px 40px;
}
.age-item {
  font-size: 90px;
  font-style: italic;
  font-weight: 800;
  line-height: 100%;
}
.age-item span {
  color: var(--clr-purple);
  margin-right: 15px;
}

/* RWD Styles */
@media only screen and (max-width: 820px) {
  .app-box {
    padding: 50px;
  }
  .age-item {
    font-size: 50px;
  }
}
</style>