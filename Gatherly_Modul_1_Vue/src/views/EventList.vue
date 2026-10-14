<script setup>
import { ref, computed } from 'vue';
import { useRouter } from 'vue-router';

import EventCard from '@/components/event/EventCard.vue';
import SearchBar from '@/components/event/SearchBar.vue';
import CategoryFilter from '@/components/event/CategoryFilter.vue';

const router = useRouter();

const events = [
  {
    id: 1,
    title: 'Vue.js Mastery Workshop',
    date: 'Oct 12, 2026',
    cat: 'Workshop',
    loc: '📍 Tech Hub, Jakarta',
    desc: 'Master modern Vue.js concepts, Composition API, and state management to build high-performance web applications interactively.'
  },
  {
    id: 2,
    title: 'National Tech Meetup',
    date: 'Oct 16, 2026',
    cat: 'Meetup',
    loc: '📍 Main Auditorium, City Center',
    desc: 'A gathering of hundreds of developers and tech enthusiasts to share the latest industry trends and expand professional networks.'
  },
  {
    id: 3,
    title: 'Startup Pitch Competition',
    date: 'Nov 02, 2026',
    cat: 'Competition',
    loc: '📍 Innovation Center',
    desc: 'Watch the best tech startups compete for thousands in investment prizes and mentorship opportunities.'
  },
  {
    id: 4,
    title: 'UI/UX Design Sprint',
    date: 'Nov 10, 2026',
    cat: 'Workshop',
    loc: '📍 Creative Studio',
    desc: 'Master the art of designing user interfaces using the latest UI/UX design tools and visual hierarchy principles.'
  },
  {
    id: 5,
    title: 'Digital Marketing Seminar',
    date: 'Nov 18, 2026',
    cat: 'Seminar',
    loc: '📍 Grand Hotel Hall',
    desc: 'Learn advanced digital marketing strategies, from SEO optimization to user segmentation to sustainable audience growth.'
  },
  {
    id: 6,
    title: 'Community Leaders Summit',
    date: 'Dec 05, 2026',
    cat: 'Conference',
    loc: '📍 Gatherly HQ',
    desc: 'An exclusive event for community leaders to formulate sustainable ecosystem development strategies.'
  }
];

const searchQuery = ref('');
const selectedCategory = ref('All');

const categories = [
  'All',
  'Workshop',
  'Meetup',
  'Competition',
  'Seminar',
  'Conference'
];

const filteredEvents = computed(() => {
  return events.filter((event) => {
    const search = searchQuery.value.toLowerCase();

    const matchesSearch =
      event.title.toLowerCase().includes(search) ||
      event.loc.toLowerCase().includes(search);

    const matchesCategory =
      selectedCategory.value === 'All' ||
      event.cat === selectedCategory.value;

    return matchesSearch && matchesCategory;
  });
});

const handleViewDetail = (id) => {
  router.push(`/browse/events/${id}`);
};
</script>

<template>
  <div class="event-list-page">
    <div class="header-section">
      <h2 class="section-title">Upcoming Events</h2>

      <p class="section-desc">
        Discover workshops, seminars, tech meetups, and competitions near you.
      </p>
    </div>

    <div class="filters-section">
      <SearchBar v-model="searchQuery" />

      <CategoryFilter
        :categories="categories"
        v-model="selectedCategory"
      />
    </div>

    <div v-if="filteredEvents.length > 0" class="event-grid">
      <EventCard
        v-for="event in filteredEvents"
        :key="event.id"
        :event="event"
        @view-detail="handleViewDetail"
      />
    </div>

    <div v-else class="empty-state">
      <p>No events found matching your criteria.</p>
    </div>
  </div>
</template>

<style scoped>
.header-section {
  margin-bottom: var(--space-8);
}

.section-title {
  font-size: 2.2rem;
  margin-bottom: var(--space-2);
}

.section-desc {
  color: var(--text-muted);
  font-size: 1.1rem;
}

.filters-section {
  margin-bottom: var(--space-6);
}

.event-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: var(--space-6);
}

.empty-state {
  text-align: center;
  padding: var(--space-12);
  color: var(--text-muted);
  background: var(--bg-light);
  border-radius: var(--space-4);
}

@media (max-width: 700px) {
  .event-grid {
    grid-template-columns: 1fr;
  }
}
</style>