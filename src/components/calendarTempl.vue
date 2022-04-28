<template>

  <div>{{ date?.toISOString().split("T")[0] }}</div>
  <div class="calendar-wrapper">
    <div class="calendar">
      <div class="custom-month-wrapper" v-if="displayMonths">
        <div
          class="custom-month"
          @click="changeCustomMonth(index)"
          v-for="(month, index) in customMounths"
          :key="index * Math.random()"
          v-bind:class="[currentMonth == index + 1 ? 'active' : '']"
        >
          {{ month }}
        </div>
      </div>
      <div class="custom-year-wrapper" v-if="displayYears">
        <div
          class="custom-year"
          @click="changeCustomYear(year)"
          v-for="(year, index) in customYears"
          :key="index * Math.random()"
          v-bind:class="[currentYear == year ? 'active' : '']"
        >
          {{ year }}
        </div>
      </div>
      <button class="open-months" @click="displayMonths = !displayMonths">
        {{ customMounths[currentMonth - 1] }}
        <svg
          width="10"
          height="6"
          viewBox="0 0 10 6"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M0.75 0.75L5 5.25L9.25 0.75"
            stroke="#3F3A38"
            stroke-width="1.5"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </button>
      <button class="open-years" @click="displayYears = !displayYears">
        {{ currentYear }}
        <svg
          width="10"
          height="6"
          viewBox="0 0 10 6"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M0.75 0.75L5 5.25L9.25 0.75"
            stroke="#3F3A38"
            stroke-width="1.5"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </button>
      <DatePicker
        v-model="date"
        highlight.style="font-weght: 400"
        color="#E24C3B"
        ref="calendar"
      >
      </DatePicker>
      <button class='custom-calendar-cancel'>Cancel</button>
      <button class='custom-calendar-set-date'>Set Date</button>
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
      date: new Date(),
      customMounths: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ],
      customYears: [
        2021, 2022, 2023, 2024, 2025, 2026, 2027, 2028, 2029, 2030, 2031, 2032,
      ],
      currentMonth: new Date().getMonth() + 1,
      currentYear: new Date().getFullYear(),
      displayMonths: false,
      displayYears: false,
    };
  },
  methods: {
    changeCustomMonth: async function (index) {
      const calendar = this.$refs.calendar;
      this.currentMonth = index + 1;
      this.displayMonths = !this.displayMonths;
      await calendar.move({ month: index + 1, year: this.currentYear });
    },
    changeCustomYear: async function (year) {
      const calendar = this.$refs.calendar;
      this.currentYear = year;
      this.displayYears = !this.displayYears;
      await calendar.move({ month: this.currentMonth, year: year });
    },
  },
};
</script>


