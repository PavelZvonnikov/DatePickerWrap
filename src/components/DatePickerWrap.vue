<template>
  <div class='calendar'>
    <v-date-picker v-model='localValue' :range='range'></v-date-picker>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'DatePicker',
  props: {
    value: {
      type: [String, Array]
    },
    range: {
      type: Boolean
    },
    format: {
      type: String
    },
  },
  methods: {

  },
  computed: {
    localValue: {
      get() {
        if (!this.range) {
          try {
            const date = moment(this.value, this.format).format("YYYY-MM-DD");
            return date;
          } catch (error) {
            console.error(error);
            const currentDate = moment().format("YYYY-MM-DD");
            return currentDate
          }
        } else {
          try {
            const datesArr = this.value.map(item => moment(item, this.format).format("YYYY-MM-DD"))
            return datesArr
          } catch (error) {
              const firstDate = moment().format("YYYY-MM-DD");
              return [firstDate]
          }
        }
      },
      set(newValue) {
        if (!this.range) {
          const date = moment(newValue, 'YYYY-MM-DD').format(this.format);
          this.$emit('changeDate', date);
        } else {
          const datesArr = newValue.map(date => moment(date, 'YYYY-MM-DD').format(this.format));
          this.$emit('changeDate', datesArr);
        }
      }
    }
  }
};
</script>
