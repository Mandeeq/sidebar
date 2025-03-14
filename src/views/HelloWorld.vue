<script setup>
import { ref, onMounted } from 'vue';

const isSidebarOpen = ref(true); // Start with the sidebar open

const toggleSidebar = () => {
  isSidebarOpen.value = !isSidebarOpen.value;
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
  <!-- Import Boxicons -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/boxicons@2.1.4/css/boxicons.min.css" />

  <div class="container">
    <!-- Sidebar -->
    <aside 
      :class="['sidebar', { 'show': isSidebarOpen }]" 
      @mouseenter="handleMouseEnter" 
      @mouseleave="handleMouseLeave">
      <nav>
        <h2 class="logo">MyApp</h2>
        <ul>
          <li>
            <a href="#" class="nav_link active">
              <i class='bx bx-grid-alt'></i> 
              <span class="nav-text">Dashboard</span>
            </a>
          </li>
          <li>
            <a href="#" class="nav_link">
              <i class='bx bx-user'></i> 
              <span class="nav-text">Users</span>
            </a>
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

    <!-- Main Content -->
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
}

.sidebar ul li a i {
  font-size: 1.5rem;
  margin-right: 10px;
}

/* When sidebar is minimized, hide text */
.sidebar:not(.show) .nav-text {
  opacity: 0;
  visibility: hidden;
}

/* Keep icons visible when sidebar is minimized */
.sidebar:not(.show) i {
  font-size: 1.5rem; /* Adjust the icon size if needed */
}

/* Sidebar link hover and active state */
.sidebar ul li a:hover,
.sidebar ul li a.active {
  background: #555;
}
</style>
