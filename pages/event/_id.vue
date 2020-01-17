<template>
	<div id="ik">
		<h2>{{event.title}}</h2>
	</div>
</template>
<script>
import { mapState } from 'vuex'
export default {
  head() {
   return {
    title: this.event.title,
    meta: [
    {
     hid: 'description',
     name: 'description',
     content: 'All you need to know about event' + this.event.title
    }
  ]
 }
},
  async fetch({ store, error , params}){
  try {
   await store.dispatch('events/fetchEvent', params.id)

 }catch(e) {
    error({ statusCode: 503, message: 'Unable to fetch event at this time, please try again' })
  }
  },
  computed: mapState({
    event: state => state.events.event
  })
}
</script>
