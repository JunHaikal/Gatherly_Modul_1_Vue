<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const stats = [
  { label: 'Total Events', value: '24', change: '+12% this month', icon: '🎟️', trend: 'up' },
  { label: 'Total Attendees', value: '1,840', change: '+18% this month', icon: '👥', trend: 'up' },
  { label: 'Tickets Sold', value: '1,320', change: '85% occupancy', icon: '🎫', trend: 'up' },
  { label: 'Total Revenue', value: 'Rp 48.5M', change: '+15.2% vs last month', icon: '💳', trend: 'up' }
]

const recentEvents = [
  {
    id: 1,
    title: 'Community Gathering 2026',
    category: 'Community',
    date: 'Oct 15, 2026',
    location: 'Main Auditorium, City Center',
    status: 'Active',
    attendees: '455 / 500'
  },
  {
    id: 2,
    title: 'Tech Innovation Summit',
    category: 'Technology',
    date: 'Oct 18, 2026',
    location: 'Innovation Hall, Tech City',
    status: 'Active',
    attendees: '320 / 350'
  },
  {
    id: 3,
    title: 'Live Music Night',
    category: 'Music',
    date: 'Oct 22, 2026',
    location: 'Central Park Stage',
    status: 'Draft',
    attendees: '0 / 200'
  },
  {
    id: 4,
    title: 'Business Connect Meetup',
    category: 'Business',
    date: 'Oct 28, 2026',
    location: 'Grand Convention Hall',
    status: 'Active',
    attendees: '180 / 200'
  }
]

const filterStatus = ref('all')

const handleCreateEvent = () => {
  alert('Fitur tambah event siap dikembangkan di modul berikutnya!')
}
</script>

<template>
  <div class="dashboard-page">
    <!-- Header Greeting -->
    <header class="dash-header">
      <div>
        <h1 class="dash-title">Organizer Dashboard</h1>
        <p class="dash-subtitle">Selamat datang kembali! Pantau performa dan kelola event Gatherly Anda.</p>
      </div>
      <div class="dash-actions">
        <button class="btn btn-primary" @click="handleCreateEvent">
          <span>+ Create New Event</span>
        </button>
      </div>
    </header>

    <!-- Stat Cards Grid -->
    <section class="stats-grid">
      <div class="stat-card" v-for="(stat, idx) in stats" :key="idx">
        <div class="stat-top">
          <span class="stat-icon">{{ stat.icon }}</span>
          <span class="stat-trend badge">{{ stat.change }}</span>
        </div>
        <div class="stat-bottom">
          <h3 class="stat-value">{{ stat.value }}</h3>
          <p class="stat-label">{{ stat.label }}</p>
        </div>
      </div>
    </section>

    <!-- Main Content: Recent Events & Quick Overview -->
    <section class="dashboard-content">
      <!-- Events Table -->
      <div class="panel-card events-panel">
        <div class="panel-header">
          <div>
            <h2>Recent Events</h2>
            <p>Daftar event yang sedang aktif dan dikelola</p>
          </div>
          <router-link to="/browse/events" class="btn-link">View All Events &rarr;</router-link>
        </div>

        <div class="table-container">
          <table class="dash-table">
            <thead>
              <tr>
                <th>Event Name</th>
                <th>Category</th>
                <th>Date</th>
                <th>Attendees</th>
                <th>Status</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in recentEvents" :key="item.id">
                <td>
                  <div class="event-cell-name">
                    <strong>{{ item.title }}</strong>
                    <span class="event-cell-loc">📍 {{ item.location }}</span>
                  </div>
                </td>
                <td>
                  <span class="category-pill">{{ item.category }}</span>
                </td>
                <td>{{ item.date }}</td>
                <td>
                  <div class="attendee-stat">
                    <span>{{ item.attendees }}</span>
                  </div>
                </td>
                <td>
                  <span
                    class="status-badge"
                    :class="item.status.toLowerCase()"
                  >
                    {{ item.status }}
                  </span>
                </td>
                <td>
                  <router-link :to="`/browse/events/${item.id}`" class="table-btn-link">
                    Detail
                  </router-link>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- Quick Tips & Shortcuts -->
      <div class="panel-card shortcuts-panel">
        <div class="panel-header">
          <h2>Quick Navigation</h2>
          <p>Akses cepat modul</p>
        </div>

        <div class="shortcut-list">
          <router-link to="/browse/events" class="shortcut-item">
            <div class="shortcut-icon">🎟️</div>
            <div class="shortcut-info">
              <strong>Event Directory</strong>
              <span>Katalog publik event Gatherly</span>
            </div>
            <span class="arrow">&rsaquo;</span>
          </router-link>

          <router-link to="/browse/category" class="shortcut-item">
            <div class="shortcut-icon">🏷️</div>
            <div class="shortcut-info">
              <strong>Categories</strong>
              <span>Kelola dan jelajahi kategori event</span>
            </div>
            <span class="arrow">&rsaquo;</span>
          </router-link>

          <router-link to="/" class="shortcut-item">
            <div class="shortcut-icon">🏠</div>
            <div class="shortcut-info">
              <strong>Public Homepage</strong>
              <span>Lihat halaman utama pengguna</span>
            </div>
            <span class="arrow">&rsaquo;</span>
          </router-link>

          <router-link to="/contact" class="shortcut-item">
            <div class="shortcut-icon">💬</div>
            <div class="shortcut-info">
              <strong>Support & Contact</strong>
              <span>Bantuan & hubungi tim Gatherly</span>
            </div>
            <span class="arrow">&rsaquo;</span>
          </router-link>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.dashboard-page {
  display: flex;
  flex-direction: column;
  gap: 1.75rem;
}

.dash-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.dash-title {
  font-size: 1.85rem;
  font-weight: 800;
  color: #1c1948;
  margin-bottom: 0.25rem;
}

.dash-subtitle {
  color: #73718b;
  margin: 0;
  font-size: 0.95rem;
}

.dash-actions {
  display: flex;
  gap: 0.75rem;
}

/* Stat Cards */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.25rem;
}

.stat-card {
  background: white;
  border: 1px solid #eceaf5;
  border-radius: 16px;
  padding: 1.35rem;
  box-shadow: 0 8px 24px rgba(30, 24, 75, 0.04);
  display: flex;
  flex-direction: column;
  gap: 1rem;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.stat-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 28px rgba(30, 24, 75, 0.08);
}

.stat-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.stat-icon {
  font-size: 1.8rem;
  background: #f4f2ff;
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 12px;
}

.stat-trend {
  font-size: 0.75rem;
  padding: 0.25rem 0.6rem;
  background: #ecfdf5;
  color: #059669;
  border-radius: 999px;
  font-weight: 600;
}

.stat-value {
  font-size: 1.65rem;
  font-weight: 800;
  color: #1c1948;
  margin: 0 0 0.2rem 0;
}

.stat-label {
  color: #73718b;
  font-size: 0.88rem;
  margin: 0;
}

/* Dashboard content */
.dashboard-content {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 1.5rem;
}

.panel-card {
  background: white;
  border: 1px solid #eceaf5;
  border-radius: 16px;
  padding: 1.5rem;
  box-shadow: 0 8px 24px rgba(30, 24, 75, 0.04);
}

.panel-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1.25rem;
}

.panel-header h2 {
  font-size: 1.2rem;
  font-weight: 700;
  color: #1c1948;
  margin: 0 0 0.2rem 0;
}

.panel-header p {
  color: #73718b;
  font-size: 0.85rem;
  margin: 0;
}

/* Table */
.table-container {
  overflow-x: auto;
}

.dash-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.9rem;
}

.dash-table th {
  text-align: left;
  padding: 0.85rem 0.75rem;
  color: #73718b;
  font-weight: 600;
  border-bottom: 1px solid #f0edf8;
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.dash-table td {
  padding: 1rem 0.75rem;
  border-bottom: 1px solid #f6f5fc;
  color: #333;
}

.dash-table tbody tr:hover {
  background-color: #faf9ff;
}

.event-cell-name {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
}

.event-cell-loc {
  font-size: 0.78rem;
  color: #73718b;
}

.category-pill {
  display: inline-block;
  padding: 0.25rem 0.65rem;
  background: #f0edff;
  color: var(--primary, #6644ff);
  border-radius: 999px;
  font-size: 0.78rem;
  font-weight: 600;
}

.status-badge {
  display: inline-block;
  padding: 0.25rem 0.65rem;
  border-radius: 999px;
  font-size: 0.75rem;
  font-weight: 600;
}

.status-badge.active {
  background: #ecfdf5;
  color: #059669;
}

.status-badge.draft {
  background: #fffbeb;
  color: #d97706;
}

.table-btn-link {
  color: var(--primary, #6644ff);
  text-decoration: none;
  font-weight: 600;
  font-size: 0.85rem;
}

.table-btn-link:hover {
  text-decoration: underline;
}

/* Shortcuts */
.shortcut-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.shortcut-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 0.9rem;
  background: #fafafe;
  border: 1px solid #eeeaf7;
  border-radius: 12px;
  text-decoration: none;
  color: inherit;
  transition: all 0.2s ease;
}

.shortcut-item:hover {
  background: #f1edff;
  border-color: #d8cefc;
  transform: translateX(3px);
}

.shortcut-icon {
  font-size: 1.4rem;
  width: 40px;
  height: 40px;
  background: white;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 6px rgba(0,0,0,0.04);
}

.shortcut-info {
  display: flex;
  flex-direction: column;
  flex: 1;
}

.shortcut-info strong {
  font-size: 0.92rem;
  color: #1c1948;
}

.shortcut-info span {
  font-size: 0.78rem;
  color: #73718b;
}

.arrow {
  font-size: 1.3rem;
  color: #9c99b3;
}

/* Responsive */
@media (max-width: 1024px) {
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .dashboard-content {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 640px) {
  .stats-grid {
    grid-template-columns: 1fr;
  }
  .dash-header {
    flex-direction: column;
    align-items: flex-start;
  }
  .dash-actions {
    width: 100%;
  }
  .dash-actions .btn {
    width: 100%;
  }
}
</style>
