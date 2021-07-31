<template>
  <div class="container mt-5">
    <form class="d-flex flex-column mt-5">
      <div class="mb-3 mx-auto">
        <label for="exampleInputEmail1" class="form-label">Please select a city</label>
        <select class="form-select" aria-label="Default select example" v-model="city">
          <option selected disabled>Please select a city</option>
          <option value="ahmedabad">Ahmedabad</option>
          <option value="chandigarh">Chandigarh</option>
          <option value="delhi">Delhi</option>
          <option value="jaipur">Jaipur</option>
          <option value="kolkata">Kolkata</option>
          <option value="lucknow">Lucknow</option>
          <option value="mumbai">Mumbai</option>
          <option value="pune">Pune</option>
        </select>
      </div>
      <div class="mb-3 mx-auto">
        <label for="exampleInputPassword1" class="form-label">Please select a date</label><br />
        <date-picker v-model="date" format="DD-MM-YYYY" value-type="DD-MM-YYYY"></date-picker>
      </div>

      <button
        type="submit"
        class="btn btn-primary w-25 mx-auto"
        :disabled="is_disabled"
        @click.prevent="login"
      >
        Submit
      </button>
    </form>
  </div>
</template>

<script>
import DatePicker from 'vue2-datepicker';
import 'vue2-datepicker/index.css';

export default {
  name: 'Container',
  components: { DatePicker },
  data: () => ({
    city: null,
    date: null,
  }),
  methods: {
    login() {
      if (this.city && this.date) {
        const url = `https://mademartindia.com/test/${this.date}/${this.city}-${this.date}.pdf`;
        window.location.href = url;
      }
      return true;
    },
  },

  computed: {
    is_disabled() {
      return !!(!this.city && !this.date);
    },
  },
};
</script>
