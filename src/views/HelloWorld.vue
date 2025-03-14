<script setup>
import { ref, onMounted } from 'vue';

const isSidebarOpen = ref(true);
const isDashboardDropdownOpen = ref(false);
const isUsersDropdownOpen = ref(false);

const toggleSidebar = () => {
  isSidebarOpen.value = !isSidebarOpen.value;
};

const toggleDashboardDropdown = () => {
  isDashboardDropdownOpen.value = !isDashboardDropdownOpen.value;
};

const toggleUsersDropdown = () => {
  isUsersDropdownOpen.value = !isUsersDropdownOpen.value;
};

// Handle mouse enter and leave events for hover functionality
const handleMouseEnter = () => {
  isSidebarOpen.value = true;
};

const handleMouseLeave = () => {
  isSidebarOpen.value = false;
};

onMounted(() => {
  document.querySelectorAll('.nav_link').forEach((link) => {
    link.addEventListener('click', () => {
      document.querySelectorAll('.nav_link').forEach((l) => l.classList.remove('active'));
      link.classList.add('active');
    });
  });
});
</script>

<template>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/boxicons@2.1.4/css/boxicons.min.css" />

  <div class="container">
    <aside 
      :class="['sidebar', { 'show': isSidebarOpen }]" 
      @mouseenter="handleMouseEnter" 
      @mouseleave="handleMouseLeave">
      <nav>
        <h2 class="logo">MyApp</h2>
        <ul>
          <!-- Dashboard Dropdown -->
          <li>
            <a href="#" class="nav_link" @click="toggleDashboardDropdown">
              <i class='bx bx-grid-alt'></i> 
              <span class="nav-text">Dashboard</span>
              <i class='bx bx-chevron-down dropdown-icon'></i>
            </a>
            <ul v-if="isDashboardDropdownOpen" class="dropdown-menu">
              <li><a href="#">Overview</a></li>
              <li><a href="#">Analytics</a></li>
              <li><a href="#">Reports</a></li>
            </ul>
          </li>

          <!-- Users Dropdown -->
          <li>
            <a href="#" class="nav_link" @click="toggleUsersDropdown">
              <i class='bx bx-user'></i> 
              <span class="nav-text">Users</span>
              <i class='bx bx-chevron-down dropdown-icon'></i>
            </a>
            <ul v-if="isUsersDropdownOpen" class="dropdown-menu">
              <li><a href="#">Manage Users</a></li>
              <li><a href="#">Roles</a></li>
              <li><a href="#">Permissions</a></li>
            </ul>
          </li>

          <li>
            <a href="#" class="nav_link">
              <i class='bx bx-message-square-detail'></i> 
              <span class="nav-text">Messages</span>
            </a>
          </li>
          <li>
            <a href="#" class="nav_link">
              <i class='bx bx-folder'></i> 
              <span class="nav-text">Files</span>
            </a>
          </li>
          <li>
            <a href="#" class="nav_link">
              <i class='bx bx-cog'></i> 
              <span class="nav-text">Settings</span>
            </a>
          </li>
        </ul>
      </nav>
    </aside>

    <main>
      <header></header>
      <section class="content">
        <h1>Welcome</h1>
        <p>This is your dashboard.</p>
      </section>
    </main>
  </div>
</template>

<style scoped>
.sidebar {
  width: 200px;
  background: #E6E8F7;
  color: black;
  position: fixed;
  top: 0;
  left: -200px;
  height: 100vh;
  padding: 20px;
  transition: 0.3s ease-in-out;
}

.sidebar.show {
  left: 0;
}

.sidebar h2 {
  text-align: center;
  margin-bottom: 20px;
}

.sidebar ul {
  list-style: none;
  padding: 0;
}

.sidebar ul li {
  margin: 15px 0;
}

.sidebar ul li a {
  color: black;
  text-decoration: none;
  display: flex;
  align-items: center;
  padding: 10px;
  border-radius: 5px;
  transition: background 0.3s;
  justify-content: space-between;
}

.sidebar ul li a i {
  font-size: 1.5rem;
  margin-right: 10px;
}

.sidebar:not(.show) .nav-text {
  opacity: 0;
  visibility: hidden;
}

.sidebar:not(.show) i {
  font-size: 1.5rem;
}

/* Sidebar link hover and active state */
.sidebar ul li a:hover,
.sidebar ul li a.active {
  background: #555;
}

.dropdown-menu {
  background: #D9DBF1;
  padding-left: 20px;
  list-style: none;
}

.dropdown-menu li {
  margin: 2px 0; /* Reduce space between items */
}

.dropdown-menu li a {
  display: block;
  padding: 1px 1px; /* Reduce padding */
  color: black;
  text-decoration: none;
  transition: 0.3s;
  font-size: 0.9rem; /* Adjust font size if necessary */
}

.dropdown-menu li a:hover {
  background: #ccc;
}

/* Dropdown icon rotation */
.dropdown-icon {
  transition: transform 0.3s;
}

.nav_link[aria-expanded="true"] .dropdown-icon {
  transform: rotate(180deg);
}
</style>
