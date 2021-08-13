<template>
  <div>
    <div class="container my-5">
      <h1 class="text-center">Read E-paper Online</h1>
      <p class="h6 text-center">Just select the date and city.</p>

      <form class="row mt-5">
        <div class="col-sm-12 col-md-6 col-lg-6 mb-4">
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
        <div class="col-sm-12 col-md-6 col-lg-6">
          <label for="exampleInputPassword1" class="form-label">Please select a date</label><br />
          <date-picker
            v-model="date"
            format="DD-MM-YYYY"
            value-type="DD-MM-YYYY"
            :disabled-date="disabledDate"
          ></date-picker>
        </div>
      </form>
    </div>

    <div class="fluid-container mt-5 mb-1 mx-md-3" v-if="url">
      <vue-pdf-app :pdf="url" @pages-rendered="pagesRendered" />
    </div>
  </div>
</template>

<script>
import DatePicker from 'vue2-datepicker';
import VuePdfApp from 'vue-pdf-app';

import 'vue2-datepicker/index.css';

export default {
  name: 'Container',
  components: { DatePicker, VuePdfApp },
  data: () => ({
    city: null,
    date: null,
    showPDF: false,
  }),
  methods: {
    disabledDate(date) {
      const today = new Date();
      today.setHours(0, 0, 0, 0);
      return date > today || date < new Date(1627606800000);
    },
    disabledRange(date) {
      return date < new Date(2021, 7, 2) || date > new Date(2021, 6, 31);
    },
    pagesRendered() {
      this.showPDF = true;
    },
  },

  computed: {
    url() {
      if (this.city && this.date) {
        return `https://thelazyshell.github.io/ie-newspaper/epapers/${this.date}/${this.city}.pdf`;
      }
      return false;
    },
  },
};
</script>
