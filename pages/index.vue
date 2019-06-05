<template>
  <v-layout>
    <v-flex xs12>
      <v-card>
        <v-card-text class="pa-0">
          <div class="cont-chat-messages">
            <v-list
              v-for="(item, i) in history"
              :key="i"
              subheader
              dense
              two-line
            >
              <template>
                <v-subheader>
                  {{ item.date }}
                </v-subheader>

                <v-divider></v-divider>

                <v-list-tile
                  v-for="(message, j) in item.messages"
                  :key="j"
                  avatar
                  ripple
                  @click="() => {}"
                >
                  <v-list-tile-avatar>
                    <v-icon>chat</v-icon>
                  </v-list-tile-avatar>

                  <v-list-tile-content>
                    <v-list-tile-title>{{ message.alias }}</v-list-tile-title>
                    <v-list-tile-sub-title>
                      <span>{{ formatMessageTime(message.date) }} &mdash;</span>
                      {{ message.text }}
                    </v-list-tile-sub-title>
                  </v-list-tile-content>
                </v-list-tile>
              </template>
            </v-list>
          </div>
          <v-divider></v-divider>
          <v-text-field
            light
            solo
            autofocus
            prepend-inner-icon="sentiment_very_satisfied"
            append-icon="send"
            label="Escribe un mensaje"
            hide-details
          ></v-text-field>
        </v-card-text>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data() {
    return {
      history: [
        {
          date: 'Yesterday',
          messages: [
            {
              avatar: 'https://cdn.vuetifyjs.com/images/lists/1.jpg',
              alias: 'Brunch this weekend',
              date: '2019-06-01 17:31:30 UTC',
              text:
                "I'll be in your neighborhood doing errands this weekend. Do you want to hang out? I'll be in your neighborhood"
            },
            {
              avatar: 'https://cdn.vuetifyjs.com/images/lists/2.jpg',
              alias: 'Summer BBQ',
              date: '2019-06-01 17:32:35 UTC',
              text: "Wish I could come, but I'm out of town this weekend."
            },
            {
              avatar: 'https://cdn.vuetifyjs.com/images/lists/2.jpg',
              alias: 'Summer BBQ',
              date: '2019-06-01 17:32:36 UTC',
              text: "Wish I could come, but I'm out of town this weekend."
            },
            {
              avatar: 'https://cdn.vuetifyjs.com/images/lists/3.jpg',
              alias: 'Oui oui',
              date: '2019-06-01 17:34:40 UTC',
              text: 'Do you have Paris recommendations? Have you ever been?'
            }
          ]
        },
        {
          date: 'Today',
          messages: [
            {
              avatar: 'https://cdn.vuetifyjs.com/images/lists/4.jpg',
              alias: 'Birthday gift',
              date: '2019-06-02 17:36:30 UTC',
              text:
                'Have any ideas about what we should get Heidi for her birthday?'
            },
            {
              avatar: 'https://cdn.vuetifyjs.com/images/lists/4.jpg',
              alias: 'Birthday gift',
              date: '2019-06-02 17:36:31 UTC',
              text:
                'Have any ideas about what we should get Heidi for her birthday?'
            },
            {
              avatar: 'https://cdn.vuetifyjs.com/images/lists/5.jpg',
              alias: 'Recipe to try',
              date: '2019-06-02 18:38:35 UTC',
              text:
                'We should eat this: Grate, Squash, Corn, and tomatillo Tacos.'
            }
          ]
        }
      ]
    }
  },

  methods: {
    getLocalDate(originalDate) {
      const [date, time, zone] = originalDate.split(' ')
      const [year, month, day] = date.split('-')
      const localDate = new Date(`${year} ${month} ${day} ${time} ${zone}`)

      const localYear = localDate.getFullYear()
      let localMonth = localDate.getMonth() + 1
      let localDay = localDate.getDate()
      const localHours = localDate.getHours()
      let localMinutes = localDate.getMinutes()
      let localSeconds = localDate.getSeconds()

      if (localMonth < 10) {
        localMonth = `0${localMonth}`
      }

      if (localDay < 10) {
        localDay = `0${localDay}`
      }

      if (localMinutes < 10) {
        localMinutes = `0${localMinutes}`
      }

      if (localSeconds < 10) {
        localSeconds = `0${localSeconds}`
      }

      return {
        year: localYear,
        month: localMonth,
        day: localDay,
        hours: localHours,
        minutes: localMinutes,
        seconds: localSeconds
      }
    },

    formatMessageTime(dateUTC) {
      if (!dateUTC) {
        return null
      }

      const objDate = this.getLocalDate(dateUTC)

      return `${objDate.hours}:${objDate.minutes} Hrs.`
    }
  }
}
</script>

<style lang="scss" scoped>
.cont-chat-messages {
  overflow: auto;
}
</style>
