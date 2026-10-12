<script setup>
const features = [
  { icon: '🎟️', title: 'Curated Events', description: 'Discover events selected to match your interests.' },
  { icon: '🌍', title: 'Global Reach', description: 'Find gatherings and activities from different communities.' },
  { icon: '🤝', title: 'Community Driven', description: 'Meet people and build connections through shared experiences.' },
]
</script>

<template>
  <div class="home-page">
    <section class="hero">
      <div class="hero-content">
        <span class="badge">Welcome to Gatherly</span>
        <h1 class="hero-title">Connect, Discover, and Experience</h1>
        <p class="hero-subtitle">Join our vibrant community to explore the best events tailored for you.</p>
        <div class="hero-actions">
          <router-link to="/browse/events" class="btn btn-primary">Discover Events</router-link>
          <router-link to="/about" class="btn btn-secondary">Learn More</router-link>
        </div>
      </div>
    </section>

    <section class="features">
      <div class="feature-card" v-for="(feature, index) in features" :key="index">
        <div class="feature-icon">{{ feature.icon }}</div>
        <h3>{{ feature.title }}</h3>
        <p>{{ feature.description }}</p>
      </div>
    </section>

    <section class="sitemap-visual">
      <h2>Website Structure / Site-Map</h2>
      <p class="sitemap-desc">A quick overview of how this application is structured via Vue Router.</p>
      <ul class="tree">
        <li>
          <router-link to="/">Home</router-link>
          <ul>
            <li><router-link to="/about">About</router-link></li>
            <li>
              <router-link to="/browse">Browse</router-link>
              <ul>
                <li>
                  <router-link to="/browse/events">Event List</router-link>
                  <ul><li><router-link to="/browse/events/1">Event Detail (Example)</router-link></li></ul>
                </li>
                <li><router-link to="/browse/category">Category</router-link></li>
              </ul>
            </li>
            <li><router-link to="/contact">Contact</router-link></li>
          </ul>
        </li>
      </ul>
    </section>
  </div>
</template>
