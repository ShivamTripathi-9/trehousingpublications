<template>
  <div>
    <nav ref="navMenu">
      <!-- Logo Section -->
      <div class="logo">
         <img :src="require('@/assets/logo.jpeg')" alt="Logo" />

      </div>

      <!-- Mobile Menu Icon (hamburger) -->
      <div class="menu-icon" @click="toggleMenu" ref="menuIcon">
        <div></div>
        <div></div>
        <div></div>
      </div>

      <!-- Navigation Links -->
      <ul :class="['nav-links', { active: isMenuActive }]">
        <li v-for="(item, index) in menuItems" :key="index" class="dropdown">
          <a href="#" @click.prevent="toggleDropdown(index)">
            {{ item.name }}
            <span
              v-if="item.submenu"
              class="dropdown-icon"
              :class="{ rotated: activeDropdown === index }"
            >
              <i class="bi bi-caret-down-fill"></i>
            </span>
          </a>

          <!-- Dropdown Menu -->
          <ul
            v-if="item.submenu"
            :class="['dropdown-menu', { show: activeDropdown === index }]"
          >
            <li
              v-for="(subItem, subIndex) in item.submenu"
              :key="subIndex"
              class="sub-dropdown"
            >
              <a href="#" @click.prevent="toggleSubDropdown(index, subIndex)">
                {{ subItem.name }}
                <span
                  v-if="subItem.submenu"
                  :class="[
                    'sub-dropdown-icon',
                    { rotated: activeSubDropdown[`${index}-${subIndex}`] },
                  ]"
                >
                  <i class="bi bi-caret-right-fill"></i>
                </span>
              </a>

              <!-- Sub-submenu -->
              <ul
                v-if="subItem.submenu"
                :class="[
                  'sub-dropdown-menu',
                  { show: activeSubDropdown[`${index}-${subIndex}`] },
                ]"
              >
               <li
  v-for="(subSubItem, subSubIndex) in subItem.submenu"
  :key="subSubIndex"
>
  <a
    v-if="subSubItem.url"
    :href="subSubItem.url"
    target="_blank"
    rel="noopener noreferrer"
  >
    {{ subSubItem.name }}
  </a>
  <a
    v-else
    href="#"
    @click.prevent="handleClick(subItem.courseId, subSubItem.id)"
  >
    {{ subSubItem.name }}
  </a>
</li>

              </ul>
            </li>
          </ul>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isMenuActive: false,
      activeDropdown: null,
      activeSubDropdown: {},
      menuItems: [
        {
          name: "Home",
          submenu: [
            { name: "About" },
            { name: "Mission & Vision" },
            { name: "Books" },
            { name: "Notification" },
            { name: "News Letter" },
          ],
        },
        {
          name: "Syllabus",
          submenu: [],
        },
        {
          name: "PYQP & Answer Key",
          submenu: [],
        },
        {
          name: "Solved Paper",
          submenu: [
            {
              name: "BPSC TRE",
              submenu: [
                { name: "BPSC TRE 1.0 (11-12) Computer Science" },
                { name: "BPSC TRE 2.0 (11-12) Computer Science" },
              ],
            },
          ],
        },
        {
          name: "Mock Test",
        },
      ],
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuActive = !this.isMenuActive;
    },

    async toggleDropdown(index) {
      const clickedItem = this.menuItems[index];

      if (
        ["Syllabus", "PYQP & Answer Key"].includes(clickedItem.name) &&
        clickedItem.submenu.length === 0
      ) {
        try {
          const formattedData = await this.fetchSyllabusData();
          this.menuItems[index].submenu = formattedData;
        } catch (error) {
          console.error("Error loading data:", error);
        }
      }

      this.activeDropdown = this.activeDropdown === index ? null : index;
      this.activeSubDropdown = {};
    },

    toggleSubDropdown(parentIndex, subIndex) {
      const key = `${parentIndex}-${subIndex}`;
      this.activeSubDropdown = {
        ...this.activeSubDropdown,
        [key]: !this.activeSubDropdown[key],
      };
    },

    async fetchSyllabusData() {
      const response = await fetch("https://cms.trehousingpublication.com/api/v1/");
      const apiData = await response.json();

      return apiData.map((item) => ({
        name: item.title,
        courseId: item.id,
        submenu: item.subjects.map((subject) => ({
          name: subject.title,
          id: subject.id,
        })),
      }));
    },

    handleClick(courseId, subjectId) {
      if (!courseId) return;

      // Detect if the active dropdown is "PYQP & Answer Key"
      const activeItem = this.menuItems[this.activeDropdown];
      if (activeItem && activeItem.name === "PYQP & Answer Key") {
        // Redirect to /PYQ with only course_id
        const query = new URLSearchParams({
          course_id: courseId,
          subject_id: subjectId,
        }).toString();
        window.location.href = `/PYQ?${query}`;
      } else if (subjectId) {

        const query = new URLSearchParams({
          course_id: courseId,
          subject_id: subjectId,
        }).toString();
        window.location.href = `/syllabus?${query}`;
      }

    },
  },
};
</script>

<style scoped>
@import url("https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css");

/* Navbar Styles */
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 30px;
  width: 100%;
  position: relative;

  
}

.logo {
  display: flex;
  align-items: center;
  padding: 0 50px;
}

.logo img {
  width: 90px;
  height: 90px;
  object-fit: cover;
  border-radius: 18px;
}




/* Navbar Links */
.nav-links {
  display: flex;
  align-items: center;
  list-style: none;
  flex-grow: 1;
  justify-content: center;
 
}

.nav-links li {
  position: relative;
  margin: 0 15px;
}

.nav-links a {
  text-decoration: none;
  color: black;
  font-size: 20px;
  transition: color 0.4s ease-in-out;
  display: flex;
  align-items: center;
}

.nav-links a:hover {
  font-weight: bold !important;
  text-decoration: none; /* REMOVE underline on hover */
}

/* Dropdown Menu */
.dropdown-menu {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  list-style-type: none;
  width: auto;
  z-index: 1001;
  border: none;
  text-decoration: none;
}

.dropdown-menu.show {
  display: block;
}

/* Styling for dropdown icons */
.dropdown-icon {
  padding-left: 7px;
  font-size: 20px;
  font-weight: bold;
  display: inline-block;
  transition: transform 0.4s ease-in-out; /* Smooth rotation */
  transform: rotate(0deg);
  text-decoration: none;
  cursor: pointer;
}

.dropdown-icon.rotated {
  transform: rotate(180deg);
  text-decoration: none;
  margin-left: 10px;
}

.dropdown-icon:hover {
  text-decoration: none;
}

/* Sub-dropdown menu */
.sub-dropdown {
  position: relative;
  font-size: 20px;
  width: 100%;
  right: 25px;
  padding: 10px 20px;
}

.sub-dropdown a {
  justify-content: space-between;
  align-items: center;
  font-size: 20px;
  width: 30vh;
  text-decoration: none; /* No underline */
}

.sub-dropdown-menu {
  display: none;
  position: absolute;
  top: -10px;
  left: 100%;
  background-color: white;
  list-style: none;
  padding: 10px 0;
  width: 40vh;
  height: auto;
  overflow-y: auto;
  z-index: 1000;
  scroll-behavior: smooth;
  text-align: left;
  font-size: 20px;
  right: 50px;
  border-radius: 10px;
  margin-left: -40px;
  text-decoration: none;
  transition: transform 0.4s ease; /* Smooth rotation */
  max-height: 400px;
 overflow-x: auto;  
}

.sub-dropdown-menu a {
  padding: 10px 0;
  text-decoration: none; /* No underline */
}

.sub-dropdown-menu.show {
  display: block;
}

.sub-dropdown-icon {
  padding-left: 7px;
  font-size: 20px;
  font-weight: bold;
  display: inline-block;
  transition: transform 0.4s ease; /* Smooth rotation */
  transform: rotate(0deg);
  cursor: pointer;
  text-decoration: none;
}

.sub-dropdown-icon.rotated {
  transform: rotate(90deg);
}

/* Mobile Menu Icon */
.menu-icon {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 30px;
  height: 22px;
  cursor: pointer;
}

.menu-icon div {
  width: 100%;
  height: 4px;
  background-color: black;
}

@media (max-width: 1024px) {
  .dropdown-menu,
  .sub-dropdown-menu {
    width: 100%;
  }
}

/* Responsive Design for Mobile Screens */
@media (max-width: 768px) {
  nav {
    padding: 15px 20px;
  }

  .logo img {
    width: 80px;
    height: 80px;
  }

  .logo {
    padding: 0 0px; 
  }
  .menu-icon {
    display: flex;
  }

  .nav-links {
    display: none;
    flex-direction: column;
    align-items: center;
    width: 100%;
    position: absolute;
    top: 100%;
    left: 0;
    background-color: white;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    padding: 0px 20px;
    z-index: 1002;
  }

  .nav-links.active {
    display: flex;
  }

  .nav-links li {
    margin: 10px 0;
    width: 100%;
    text-align: center;
    margin: 0;
    font-size: 18px;
    justify-content: space-between;
  }

  .dropdown-icon {
    font-size: 15px;
    margin-left: auto;
  }

  .dropdown-menu {
    position: static;
    width: 100%;
    padding: 0px 50px;
  }

  .dropdown-menu li a {
    width: 100%;
    padding: 5px 10px;
  }

  .sub-dropdown-menu {
    position: static;
    width: 100%;
    padding: 0px 100px;
    bottom: 0%;
    height: inherit;
  }

  .dropdown-menu li {
    padding: 0;
    margin: 0;
  }

  .sub-dropdown-menu li {
    text-align: center;
    display: block;
    padding: 0;
    margin: 0;
  }

  /* Scrollable Dropdown for Small Screens */
  .dropdown-menu {
    overflow-y: auto;
  }
}

/* Responsive Design for 480px Screens */
@media (max-width: 480px) {
  nav {
    padding: 15px;
  }

   .logo img {
    width: 70px;
    height: 70px;
  }

  .logo {
    padding: 0 5px;
  }

  .nav-links {
    padding: 8px;
  }

  .nav-links li {
    margin: 6px 0;
  }

  .dropdown-menu {
    padding: 0 30px;
  }

  .sub-dropdown-menu {
    padding: 0 80px;
  }

  .menu-icon {
    width: 22px;
    height: 18px;
  }

  .nav-links a {
    font-size: 16px;
  }

  .dropdown-menu {
    font-size: 16px;
  }

  .sub-dropdown-menu {
    font-size: 14px;
  }
}

/* Responsive Design for 365px Screens */
@media (max-width: 365px) {
  nav {
    padding: 10px;
  }

  
   .logo img {
    width: 50px;
    height: 50px;
  }

  .logo {
    padding: 0 5px;
  }

  .menu-icon {
    width: 20px;
    height: 16px;
  }

  .nav-links {
    padding: 5px;
  }

  .nav-links li {
    margin: 5px 0;
  }

  .dropdown-menu {
    padding: 0 20px;
  }

  .sub-dropdown-menu {
    padding: 0 50px;
  }

  .nav-links a {
    font-size: 14px;
  }

  .dropdown-menu {
    font-size: 14px;
  }

  .sub-dropdown-menu {
    font-size: 12px;
  }
}
</style>
