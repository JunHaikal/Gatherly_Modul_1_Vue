<script setup>
import { ref } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import Breadcrumb from '@/components/app/Breadcrumb.vue'

const route = useRoute()
const router = useRouter()
const isSidebarOpen = ref(false)

const navItems = [
  {
    name: 'Overview',
    path: '/dashboard',
    icon: '📊',
    exact: true
  },
  {
    name: 'Manage Events',
    path: '/dashboard/events',
    icon: '🎟️',
    exact: false
  },
  {
    name: 'Event Categories',
    path: '/dashboard/category',
    icon: '🏷️',
    exact: false
  }
]

const toggleSidebar = () => {
  isSidebarOpen.value = !isSidebarOpen.value
}

const closeSidebar = () => {
  isSidebarOpen.value = false
}

const isActive = (item) => {
  if (item.exact) {
    return route.path === item.path
  }
  return route.path.startsWith(item.path)
}
</script>

<template>
  <div class="dashboard-layout">
    <!-- Mobile Sidebar Backdrop -->
    <div
      v-if="isSidebarOpen"
      class="sidebar-backdrop"
      @click="closeSidebar"
    ></div>

    <!-- Sidebar -->
    <aside class="dash-sidebar" :class="{ 'is-open': isSidebarOpen }">
      <div class="sidebar-header">
        <router-link to="/" class="sidebar-logo">
          <svg width="26" height="30" viewBox="0 0 24 28" fill="none" xmlns="http://www.w3.org/2000/svg" class="logo-svg">
            <path d="M12 0L22.3923 6V18L12 24L1.6077 18V6L12 0Z" fill="white" />
            <path d="M15 9.5 C15 9.5 14 8 12 8 C9.5 8 8 10 8 12.5 C8 15 9.5 17 12 17 C14 17 15 16 15.5 14.5 V 12.5 H 12.5" stroke="#1A1643" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" />
          </svg>
          <div class="logo-title">
            <span class="brand-name">Gatherly</span>
            <span class="portal-badge">Admin</span>
          </div>
        </router-link>
        <button class="close-btn" @click="closeSidebar" aria-label="Close Sidebar">&times;</button>
      </div>

      <div class="sidebar-nav-container">
        <div class="nav-section-title">MAIN MENU</div>
        <nav class="sidebar-menu">
          <router-link
            v-for="item in navItems"
            :key="item.path"
            :to="item.path"
            class="sidebar-link"
            :class="{ active: isActive(item) }"
            @click="closeSidebar"
          >
            <span class="link-icon">{{ item.icon }}</span>
            <span class="link-text">{{ item.name }}</span>
          </router-link>
        </nav>

        <div class="nav-section-title">QUICK LINKS</div>
        <nav class="sidebar-menu">
          <router-link to="/" class="sidebar-link">
            <span class="link-icon">🌐</span>
            <span class="link-text">Public Website</span>
          </router-link>
          <router-link to="/browse/events" class="sidebar-link">
            <span class="link-icon">🔍</span>
            <span class="link-text">Browse Events</span>
          </router-link>
          <router-link to="/contact" class="sidebar-link">
            <span class="link-icon">✉️</span>
            <span class="link-text">Contact Support</span>
          </router-link>
        </nav>
      </div>

      <!-- User Profile Card -->
      <div class="sidebar-user">
        <div class="user-avatar">JH</div>
        <div class="user-info">
          <span class="user-name">Jun Haikal</span>
          <span class="user-role">Organizer Admin</span>
        </div>
        <router-link to="/" class="logout-link" title="Back to site">
          &rarr;
        </router-link>
      </div>
    </aside>

    <!-- Main Workspace -->
    <div class="dash-main-wrapper">
      <!-- Dashboard Top Header -->
      <header class="dash-topbar">
        <div class="topbar-left">
          <button class="menu-toggle-btn" @click="toggleSidebar" aria-label="Toggle Menu">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <line x1="3" y1="12" x2="21" y2="12"></line>
              <line x1="3" y1="6" x2="21" y2="6"></line>
              <line x1="3" y1="18" x2="21" y2="18"></line>
            </svg>
          </button>
          <div class="current-layout-label">
            <span class="layout-pill">Dashboard Layout</span>
          </div>
        </div>

        <div class="topbar-right">
          <router-link to="/" class="btn-visit-site">
            <span>&larr; Back to Public Site</span>
          </router-link>
          <div class="user-badge">
            <span class="status-dot"></span>
            <span class="user-name-small">Jun Haikal</span>
          </div>
        </div>
      </header>

      <!-- Content Area with Breadcrumb -->
      <main class="dash-content-area">
        <Breadcrumb />
        <router-view />
      </main>
    </div>
  </div>
</template>

<style scoped>
.dashboard-layout {
  display: flex;
  min-height: 100vh;
  background-color: #f7f7fc;
  color: #24213d;
}

/* Sidebar Styles */
.dash-sidebar {
  width: 270px;
  background-color: #1c1948;
  color: #ffffff;
  display: flex;
  flex-direction: column;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  z-index: 1000;
  transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  box-shadow: 4px 0 24px rgba(0, 0, 0, 0.08);
}

.sidebar-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1.5rem 1.25rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.sidebar-logo {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  text-decoration: none;
  color: #ffffff;
}

.logo-title {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.brand-name {
  font-size: 1.25rem;
  font-weight: 800;
  letter-spacing: -0.02em;
}

.portal-badge {
  font-size: 0.65rem;
  background: var(--primary, #6644ff);
  padding: 0.2rem 0.45rem;
  border-radius: 6px;
  text-transform: uppercase;
  font-weight: 700;
  letter-spacing: 0.04em;
}

.close-btn {
  display: none;
  background: none;
  border: none;
  color: #ffffff;
  font-size: 1.75rem;
  cursor: pointer;
  padding: 0;
  line-height: 1;
}

.sidebar-nav-container {
  flex: 1;
  overflow-y: auto;
  padding: 1.5rem 1rem;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.nav-section-title {
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  color: rgba(255, 255, 255, 0.4);
  padding-left: 0.75rem;
  margin-bottom: 0.25rem;
}

.sidebar-menu {
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
}

.sidebar-link {
  display: flex;
  align-items: center;
  gap: 0.85rem;
  padding: 0.75rem 0.95rem;
  border-radius: 10px;
  color: rgba(255, 255, 255, 0.75);
  text-decoration: none;
  font-size: 0.92rem;
  font-weight: 500;
  transition: all 0.2s ease;
}

.sidebar-link:hover {
  color: #ffffff;
  background: rgba(255, 255, 255, 0.08);
  transform: translateX(3px);
}

.sidebar-link.active {
  color: #ffffff;
  background: var(--primary, #6644ff);
  font-weight: 600;
  box-shadow: 0 4px 14px rgba(102, 68, 255, 0.35);
}

.link-icon {
  font-size: 1.15rem;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

/* User Card at bottom of sidebar */
.sidebar-user {
  padding: 1rem 1.25rem;
  background: rgba(0, 0, 0, 0.2);
  border-top: 1px solid rgba(255, 255, 255, 0.08);
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.user-avatar {
  width: 36px;
  height: 36px;
  background: var(--primary, #6644ff);
  color: #ffffff;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 0.85rem;
}

.user-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.user-name {
  font-size: 0.88rem;
  font-weight: 600;
  color: #ffffff;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.user-role {
  font-size: 0.72rem;
  color: rgba(255, 255, 255, 0.5);
}

.logout-link {
  color: rgba(255, 255, 255, 0.6);
  text-decoration: none;
  font-size: 1.1rem;
  padding: 0.3rem;
  transition: color 0.2s;
}

.logout-link:hover {
  color: #ffffff;
}

/* Main workspace */
.dash-main-wrapper {
  flex: 1;
  margin-left: 270px;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  min-width: 0;
}

/* Topbar */
.dash-topbar {
  height: 68px;
  background: #ffffff;
  border-bottom: 1px solid #eceaf5;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 2rem;
  position: sticky;
  top: 0;
  z-index: 99;
}

.topbar-left {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.menu-toggle-btn {
  display: none;
  background: none;
  border: 1px solid #e2dfef;
  border-radius: 8px;
  padding: 0.45rem;
  cursor: pointer;
  color: #1c1948;
}

.layout-pill {
  display: inline-block;
  padding: 0.3rem 0.75rem;
  background: #f0edff;
  color: var(--primary, #6644ff);
  font-size: 0.8rem;
  font-weight: 700;
  border-radius: 999px;
}

.topbar-right {
  display: flex;
  align-items: center;
  gap: 1.25rem;
}

.btn-visit-site {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.5rem 0.9rem;
  border-radius: 8px;
  border: 1px solid #e0ddf0;
  background: #ffffff;
  color: #555172;
  font-size: 0.85rem;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.2s ease;
}

.btn-visit-site:hover {
  border-color: var(--primary, #6644ff);
  color: var(--primary, #6644ff);
}

.user-badge {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.88rem;
  font-weight: 600;
  color: #1c1948;
}

.status-dot {
  width: 8px;
  height: 8px;
  background: #10b981;
  border-radius: 50%;
}

/* Content */
.dash-content-area {
  flex: 1;
  padding: 2rem;
  max-width: 1400px;
  width: 100%;
  box-sizing: border-box;
}

/* Responsive */
@media (max-width: 900px) {
  .dash-sidebar {
    transform: translateX(-100%);
  }
  .dash-sidebar.is-open {
    transform: translateX(0);
  }
  .close-btn {
    display: block;
  }
  .dash-main-wrapper {
    margin-left: 0;
  }
  .menu-toggle-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
  }
  .sidebar-backdrop {
    position: fixed;
    inset: 0;
    background: rgba(15, 12, 40, 0.5);
    backdrop-filter: blur(2px);
    z-index: 999;
  }
  .dash-topbar {
    padding: 0 1rem;
  }
  .dash-content-area {
    padding: 1.25rem;
  }
}
</style>
