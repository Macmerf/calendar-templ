<template>
  <div class="datepicker-wrapper w-50">
    <div class="input-date-wrapper" @click="shown = !shown" >
    <input type="date"  class="form-control"  v-model="date"  readonly />
    <svg width="20" height="22" viewBox="0 0 20 22" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M18 2H17V0H15V2H5V0H3V2H2C0.9 2 0 2.9 0 4V20C0 21.1 0.9 22 2 22H18C19.1 22 20 21.1 20 20V4C20 2.9 19.1 2 18 2ZM18 20H2V9H18V20ZM18 7H2V4H18V7Z" fill="#4E5256"/>
    </svg>
  </div>
    <div v-if="shown" class="calendar-wrapper">
      <div class="calendar">
        <DatePicker v-model="date" color="#E24C3B" :model-config="modelConfig">
        </DatePicker>
        <button @click="shown = !shown" class="custom-calendar-cancel">
          Cancel
        </button>
        <button @click="shown = !shown" class="custom-calendar-set-date">
          Set Date
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { DatePicker } from "v-calendar";
import "v-calendar/dist/style.css";

export default {
  name: "calendarTempl",
  components: {
    DatePicker,
  },
  data() {
    return {
      date: new Date().toLocaleDateString(),
      shown: false,
      modelConfig: {
        type: "string",
        mask: "YYYY-MM-DD", // Uses 'iso' if missing
      },
    };
  },
  methods: {},
};
</script>


