<script setup>
import AppButton from '@/components/ui/AppButton.vue';
import AppCard from '@/components/ui/AppCard.vue';
</script>

<template>
  <div class="home-page">
    <section class="hero-section">
      <div class="hero-content">
        <h1 class="hero-title">
          Connect, Discover, and Experience
        </h1>

        <p class="hero-subtitle">
          A community event platform designed to bring ideas together.
          Discover hundreds of events near you.
        </p>

        <div class="hero-action">
          <AppButton
            variant="primary"
            @click="$router.push('/browse/events')"
          >
            Discover Events
          </AppButton>
        </div>
      </div>
    </section>

    <section class="features-section">
      <div class="features-header">
        <h2>Why Choose Gatherly?</h2>
        <p>
          Everything you need to host or attend unforgettable events.
        </p>
      </div>

      <div class="features-grid">
        <AppCard class="feature-card">
          <div class="feature-icon">🔎</div>
          <h3>Discover Easily</h3>
          <p>
            Find events tailored to your interests using our smart
            category and location filters.
          </p>
        </AppCard>

        <AppCard class="feature-card">
          <div class="feature-icon">🎟️</div>
          <h3>Seamless Ticketing</h3>
          <p>
            Register with one click and get your digital QR ticket
            instantly on your device.
          </p>
        </AppCard>

        <AppCard class="feature-card">
          <div class="feature-icon">📊</div>
          <h3>Host Like a Pro</h3>
          <p>
            Manage attendees, track revenue, and scan QR codes
            with our comprehensive dashboard.
          </p>
        </AppCard>
      </div>
    </section>
  </div>
</template>