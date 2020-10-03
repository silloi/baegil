<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-img
        src="anniversary.jpg"
      />
      <h1>記念日をカレンダーで計算</h1>
      <v-sheet
        tile
        class="d-flex"
      >
        <v-btn
          icon
          class="ma-2"
          @click="$refs.calendar.prev()"
        >
          <v-icon>mdi-chevron-left</v-icon>
        </v-btn>
        <v-spacer />
        <v-toolbar-title v-if="$refs.calendar">
          {{ $refs.calendar.title }}
        </v-toolbar-title>
        <v-spacer />
        <v-btn
          icon
          class="ma-2"
          @click="$refs.calendar.next()"
        >
          <v-icon>mdi-chevron-right</v-icon>
        </v-btn>
      </v-sheet>
      <v-sheet height="420">
        <v-calendar
          ref="calendar"
          v-model="focus"
          locale="ja-jp"
          :day-format="timestamp => new Date(timestamp.date).getDate()"
          :month-format="timestamp => (new Date(timestamp.date).getMonth() + 1) + ' /'"
          :events="events"
          @click:date="selectDay"
        />
      </v-sheet>
      <v-card>
        <v-card-title class="headline">
          記念日
        </v-card-title>
        <v-list>
          <v-list-item v-for="event in events" :key="event.name">
            <v-list-item-content two-line>
              <v-list-item-title>{{ formatDate(event.start) }}</v-list-item-title>
              <v-list-item-subtitle>{{ event.name }}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>

const numbersMemorial = [
  10,
  20,
  50,
  100,
  200,
  500
]

export default {
  data: () => ({
    focus: '',
    events: [],
    type: 'month',
    typeToLabel: {
      month: '月',
      week: '週',
      day: '日'
    }
  }),
  mounted () {
    this.setDay(new Date())
  },
  methods: {
    formatDate (date) {
      const weekdays = ['日', '月', '火', '水', '木', '金', '土']

      const year = date.getFullYear()
      const month = date.getMonth() + 1
      const weekday = weekdays[date.getDay()]
      const day = date.getDate()

      return `${year}年${month}月${day}日（${weekday}）`
    },
    setDay (date) {
      this.focus = date
      const calculateDayAfter = day => new Date(Date.parse(date) + 1000 * 60 * 60 * 24 * (day - 1))

      const datesMemorial = numbersMemorial.map((number) => {
        return {
          number,
          date: calculateDayAfter(number)
        }
      })

      const events = []

      events.push({
        name: '1日目',
        start: date,
        color: 'red'
      })

      datesMemorial.map((date) => {
        events.push({
          name: `${date.number}日目`,
          start: date.date
        })
      })

      this.events = events
    },
    selectDay ({ date }) {
      const dateDate = new Date(`${date}T00:00:00`)

      this.setDay(dateDate)
    }
  }
}
</script>

<style scoped>
h1 {
  font-size: 2rem !important;
  font-weight: 400;
  line-height: 6rem;
  letter-spacing: normal !important;
  font-family: "Roboto", sans-serif !important;
  text-align: center;
}
</style>
