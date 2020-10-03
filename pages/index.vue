<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-img
        src="anniversary.jpg"
      />
      <v-card-title>
        記念日をカレンダーで計算
      </v-card-title>
      <v-calendar />
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
  components: {}
}
</script>
