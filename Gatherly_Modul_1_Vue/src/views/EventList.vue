<script setup>
const events = Array.from({ length: 6 }, (_, index) => ({
  id: index + 1,
  date: `Oct ${10 + index}, 2026`,
  category: ['Community', 'Technology', 'Music', 'Business', 'Art', 'Food'][index],
  title: ['Community Gathering', 'Tech Innovation Summit', 'Live Music Night', 'Business Connect', 'Creative Art Expo', 'Food Festival'][index],
  location: ['Main Auditorium, City Center', 'Innovation Hall, Tech City', 'Central Park Stage', 'Grand Convention Hall', 'Art District Gallery', 'Downtown Square'][index],
  description: 'Discover an exciting gathering, meet new people, and enjoy a memorable experience with the community.',
}))
</script>

<template>
  <div class="event-list-page">
    <header class="section-header">
      <h2 class="section-title">Upcoming Events</h2>
      <p class="section-desc">Discover the latest gatherings and activities happening near you.</p>
    </header>

    <div class="event-grid">
      <div class="event-card" v-for="event in events" :key="event.id">
        <div class="event-body">
          <div class="event-meta">
            <span class="event-date">{{ event.date }}</span>
            <span class="event-category">{{ event.category }}</span>
          </div>
          <h3>{{ event.title }}</h3>
          <p class="event-loc">⌖ {{ event.location }}</p>
          <p class="event-desc">{{ event.description }}</p>
          <div class="card-footer">
            <router-link :to="`/browse/events/${event.id}`" class="btn-link">View Details &rarr;</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
