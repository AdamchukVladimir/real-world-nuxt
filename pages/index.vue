<template>
  <div>
    <h1>Events</h1>
    <EventCard 
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="data"
      />
  </div>
</template>
<script>
/* eslint-disable */
import EventCard from '../components/EventCard.vue'
import {mapState} from 'vuex'

export default {
  components: { EventCard },
  head() {
    return {
      title: 'Event Listing'
    }
  },
  async asyncData({store, error}) {
  //const response = await $axios.get('http://localhost:3000/events')   
    try{
        await store.dispatch('events/fetchEvents')
    }catch (e) {
        error({
          statusCode: 503,
          message: 'Unable to fetch events at this time. Please try again.'
        })
    }
  },
  computed: mapState({
    events: state => state.events.events
  })    
  // asyncData({$axios, error}) {
  //  // return context.$axios.get('http://localhost:3000/events').then(response=>{
  // return $axios.get('http://localhost:3000/events').then(response=>{  
  //     return{
  //       events: response.data
  //     }
  //   })
  //   .catch(e =>{
  //     error({
  //       statusCode: 503,
  //       message: 'Unable to fetch events at this time. Please try again.'
  //     })
  //   })
  // }  


}
</script>
