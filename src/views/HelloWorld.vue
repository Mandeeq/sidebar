<script setup>
import { ref, onMounted } from 'vue';

const isSidebarOpen = ref(true);
const isCmsDropdownOpen = ref(false); // CMS dropdown
const isDashboardDropdownOpen = ref(false); // Dashboard dropdown
const isUsersDropdownOpen = ref(false); // Users dropdown

const toggleSidebar = () => {
  isSidebarOpen.value = !isSidebarOpen.value;
};

const toggleCmsDropdown = () => {
  isCmsDropdownOpen.value = !isCmsDropdownOpen.value;
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
  <div class="container">
    <aside 
      :class="['sidebar', { 'show': isSidebarOpen }]" 
      @mouseenter="handleMouseEnter" 
      @mouseleave="handleMouseLeave">
      <nav>
        <h2 class="logo">MyApp</h2>
        <ul>
          <!-- CMS Dropdown -->
          <li>
            <a href="#" class="nav_link" @click="toggleCmsDropdown">
              <span class="nav-text">CMS</span>
              <i class="bx bx-chevron-down dropdown-icon"></i>
            </a>
            <ul v-if="isCmsDropdownOpen" class="dropdown-menu">
              <!-- Dashboard Item -->
              <li>
                <a href="#" @click="toggleDashboardDropdown">
                  <span class="nav-text">Dashboard</span>
                  <i class="bx bx-chevron-down dropdown-icon"></i>
                </a>
                <ul v-if="isDashboardDropdownOpen" class="dropdown-menu">
                  <li><a href="#">Overview</a></li>
                  <li><a href="#">Analytics</a></li>
                  <li><a href="#">Reports</a></li>
                </ul>
              </li>
              <!-- Users Item -->
              <li>
                <a href="#" @click="toggleUsersDropdown">
                  <span class="nav-text">Users</span>
                  <i class="bx bx-chevron-down dropdown-icon"></i>
                </a>
                <ul v-if="isUsersDropdownOpen" class="dropdown-menu">
                  <li><a href="#">Manage Users</a></li>
                  <li><a href="#">Roles</a></li>
                  <li><a href="#">Permissions</a></li>
                </ul>
              </li>
              <li><a href="#">Messages</a></li>
              <li><a href="#">Files</a></li>
              <li><a href="#">Settings</a></li>
            </ul>
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
  padding: 10px 10px 20px;
  transition: 0.3s ease-in-out;
}

.sidebar.show {
  left: 0;
}

.sidebar h2 {
  text-align: center;
  margin-bottom: 10px;
}

.sidebar ul {
  list-style: none;
  padding: 0;
}

.sidebar ul li {
  margin: 10px 0;
}

.sidebar ul li a {
  color: black;
  text-decoration: none;
  display: flex;
  align-items: center;
  padding: 8px 10px;
  border-radius: 5px;
  transition: background 0.3s;
  justify-content: space-between;
}



.dropdown-menu {
  background: #D9DBF1;
  padding-left: 10px;
  list-style: none;
}

.dropdown-menu li {
  margin: 2px 0;
}

.dropdown-menu li a {
  display: block;
  padding: 5px 10px;
  color: black;
  text-decoration: none;
  transition: 0.3s;
  font-size: 0.9rem;
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
.dropdown-icon {
  font-size: 20px; /* Set the size of the dropdown icon */
  transition: transform 0.3s;
}

</style>
