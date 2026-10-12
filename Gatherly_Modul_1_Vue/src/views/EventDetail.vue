<script setup>
import { useRoute, useRouter } from 'vue-router'

const route = useRoute()
const router = useRouter()
</script>

<template>
  <div class="event-detail-page">
    <button @click="router.push('/browse/events')" class="btn btn-back">&larr; Back to Events</button>

    <div class="detail-header">
      <div class="header-content">
        <span class="event-tag">Community Event</span>
        <h1>Community Gathering ({{ route.params.id }})</h1>
        <div class="meta-info">
          <div class="meta-item"><span class="icon">📅</span><span>October 15, 2026</span></div>
          <div class="meta-item"><span class="icon">📍</span><span>Main Auditorium, City Center</span></div>
          <div class="meta-item"><span class="icon">👥</span><span>500+ Attendees</span></div>
        </div>
      </div>
    </div>

    <div class="detail-content">
      <div class="main-desc">
        <h2>About This Event</h2>
        <p>Join us for a community gathering designed to bring people together. Enjoy an opportunity to meet new friends, share ideas, and take part in engaging activities.</p>
        <p>Expand your network, discover new interests, and create meaningful memories with fellow attendees.</p>
        <h2>Agenda</h2>
        <ul class="agenda-list">
          <li><strong>09:00 AM</strong> - Registration &amp; Welcome Coffee</li>
          <li><strong>10:00 AM</strong> - Opening Keynote Speech</li>
          <li><strong>11:30 AM</strong> - Networking Session</li>
          <li><strong>01:00 PM</strong> - Closing Remarks</li>
        </ul>
      </div>
      <aside class="sidebar">
        <div class="ticket-card">
          <h3>Registration</h3>
          <p class="price">Free</p>
          <p class="ticket-desc">Secure your spot today before it runs out.</p>
          <button class="btn btn-primary" @click="alert('Registrasi ini hanya contoh praktikum.')">Register Now</button>
          <p class="spots">Only 45 spots left</p>
        </div>
      </aside>
    </div>
  </div>
</template>
