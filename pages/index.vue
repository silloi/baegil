<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-img
        src="anniversary.jpg"
      />
      <v-card-title>
        記念日をカレンダーで計算
      </v-card-title>
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
          v-model="value"
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
          <v-list-item>
            <v-list-item-content two-line>
              <v-list-item-title>2020年10月10日</v-list-item-title>
              <v-list-item-subtitle>10日</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
          <v-list-item>20日</v-list-item>
          <v-list-item>1ヶ月</v-list-item>
          <v-list-item>50日</v-list-item>
          <v-list-item>2ヶ月</v-list-item>
          <v-list-item>3ヶ月</v-list-item>
          <v-list-item>100日</v-list-item>
          <v-list-item>6ヶ月</v-list-item>
          <v-list-item>200日</v-list-item>
          <v-list-item>300日</v-list-item>
          <v-list-item>500日</v-list-item>
          <v-list-item>1000日</v-list-item>
        </v-list>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            nuxt
            to="/inspire"
          >
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>

export default {
  data: () => ({
    focus: new Date(),
    value: '',
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
    setDay (date) {
      const calculateDayAfter = day => new Date(Date.parse(date) + 1000 * 60 * 60 * 24 * day)

      const numbersMemorial = [
        10,
        20,
        50,
        100,
        200,
        500
      ]

      const datesMemorial = numbersMemorial.map((number) => {
        return {
          number,
          date: calculateDayAfter(number)
        }
      })

      const events = []

      datesMemorial.map((date) => {
        events.push({
          name: `${date.number}日目`,
          start: date.date,
          end: date.date
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
