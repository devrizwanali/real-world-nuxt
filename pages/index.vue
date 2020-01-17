<template>
  <div>
     <h1>Events</h1>
     why not rendering first time
        <EventCard
          v-for="(event, index) in events"
          :key="index"
          :event="event"
        />
  </div>
</template>
<script type="text/javascript">
import EventCard from '~/components/EventCard'
import { mapState } from 'vuex'

export default {
  head() {
    return {
      title: 'Event Listing',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Where you can find all the events taking place in your neighborhood'
        }
      ]
    }
  },
 async fetch({ store,error}){
  try {
   store.dispatch('events/fetchEvents')
 }catch(e) {
    error({ statusCode: 503, message: 'Unable to fetch events at this time, please try again' })
  }
  },
  computed: mapState({
        events: state => state.events.events
      }),
  components: {
    EventCard
  }
}
</script>
