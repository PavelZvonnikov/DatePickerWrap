<template>
  <v-app>
    <div class='app'>
      <DatePickerWrap :value='picker' :range='range' :format='format' @changeDate='changeDate' />
    </div>
  </v-app>
</template>

<script>
import DatePickerWrap from './components/DatePickerWrap';

export default {
  name: 'App',

  components: {
    DatePickerWrap
  },

  data: () => ({
    // picker: ["20111009", "20111015"],
    picker: "20111031",
    format: "YYYYMMDD",
    range: false,
  }),
  methods: {
    changeDate(newValue) {
      this.picker = (this.range) ? [...newValue] : newValue
    }
  },
};
</script>
