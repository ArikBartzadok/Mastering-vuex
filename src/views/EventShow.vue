<template>
    <div>
        <div class="event-header">
            <span class="eyebrow">
                @{{ event.title }} on {{ event.date }}
            </span>
            <h1 class="title">{{ event.title }}</h1>
            <h5>Organized by {{ event.organizer }}</h5>
            <h5>Category: {{ event.category }}</h5>
        </div>

        <BaseIcon name="map"><h2>Location</h2></BaseIcon>

        <address>{{ event.location }}</address>

        <h2>Event details</h2>
        <p>{{ event.description }}</p>

        <h2>Attendess
            <span class="badge -fill-gradient">
                {{ event.attendees ? event.attendees.length : 0 }}
            </span>
        </h2>
        <ul class="list-group">
            <li class="list-item" v-for="(attendee, index) in event.atendees" :key="index">
                <b>{{ attendee.name }}</b>
            </li>
        </ul>
    </div>
</template>

<script>
import EventService from '@/services/EventService.js'

export default {
    props: ['id'],
    data() {
        return {
            event: {}
        }
    },
    created() {
        EventService.getEvent(this.id)
            .then(response => {
                this.event = response.data
            })
            .catch(error => {
                console.log('There was an error: ', error.response)
            })
    }
}
</script>
