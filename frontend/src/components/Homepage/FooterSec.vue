<template>
  <div>
    <footer class="footer">
      <!-- Logo and Contact Section -->
      <div class="logowithcontect">
        <div class="logo">
          <img
            :src="require('@/assets/logo.jpeg')"
            alt="Logo"
            @click.prevent="redirectHome"
            style="cursor: pointer"
          />
        </div>
        <div class="contact-info">
          <p>
            Address: TRE HOUSING PUBLICATION PRIVATE LIMITED <br />B-144.SECTOR
            XU 3 GREATER NOIDA GB NAGAR UP-201310
          </p>
          <p>Phone No: 012019575162, 9458846730</p>
          <p>Email: trehousingpublication@gmail.com</p>
        </div>
        <div class="social-icons">
          <a
            href="https://twitter.com/trepublication"
            target="_blank"
            rel="noopener noreferrer"
          >
            <i class="fab fa-twitter"></i>
          </a>
          <a
            href="https://wa.me/9458846730"
            target="_blank"
            rel="noopener noreferrer"
          >
            <i class="fab fa-whatsapp"></i>
          </a>
          <a
            href="https://t.me/trehousingpublication"
            target="_blank"
            rel="noopener noreferrer"
          >
            <i class="fab fa-telegram"></i>
          </a>
          <a
            href="https://www.youtube.com/@trehousingpublication"
            target="_blank"
            rel="noopener noreferrer"
          >
            <i class="fab fa-youtube"></i>
          </a>
        </div>
      </div>

      <!-- Vertical Bar -->
      <div class="vertical-bar-container">
        <div class="vertical-bar"></div>
      </div>

      <!-- Links Section -->
      <div class="links">
        <ul>
          <li><p class="home">Previous Year Paper</p></li>
          <li>
            <router-link to="/PYQ?course_id=1&sub_courses=1"
              >BPSC TRE 1.0</router-link
            >
          </li>
          <li>
            <router-link to="/PYQ?course_id=1&sub_courses=2"
              >BPSC TRE 2.0</router-link
            >
          </li>
          <li>
            <router-link to="/PYQ?course_id=1&sub_courses=3"
              >BPSC TRE 3.0</router-link
            >
          </li>
        </ul>
      </div>

      <!-- Other Sections -->
      <div class="syllabus">
        <ul>
          <li><p class="syl">Syllabus</p></li>
          <li>
            <router-link to="/syllabus?course_id=1&subject_id=17"
              >BPSC TRE (1-5)</router-link
            >
          </li>
          <li>
            <router-link to="/syllabus?course_id=1&subject_id=16"
              >BPSC TRE (6-8)</router-link
            >
          </li>
          <li>
            <router-link to="/syllabus?course_id=1&subject_id=15"
              >BPSC TRE (9-10)</router-link
            >
          </li>
          <li>
            <router-link to="/syllabus?course_id=1&subject_id=14"
              >BPSC TRE (11-12)</router-link
            >
          </li>
        </ul>
      </div>

      <!-- <div class="previous">
        <ul>
          <li><p class="pre">Previous Year Paper</p></li>
        </ul>
      </div> -->

      <div class="solved">
        <ul>
          <li><p class="sol">Solved Paper</p></li>
          <li><router-link to="/">BPSC TRE (1-5)</router-link></li>
          <li><router-link to="/">BPSC TRE (6-8)</router-link></li>
          <li><router-link to="/">BPSC TRE (9-10)</router-link></li>
          <li><router-link to="/">BPSC TRE (11-13)</router-link></li>
        </ul>
      </div>

      <div class="mock">
        <ul>
          <li><p class="moc">Mock Test</p></li>
          <li><router-link to="/">BPSC TRE (1-5)</router-link></li>
          <li><router-link to="/">BPSC TRE (6-8)</router-link></li>
          <li><router-link to="/">BPSC TRE (9-10)</router-link></li>
          <li><router-link to="/">BPSC TRE (11-13)</router-link></li>
        </ul>
      </div>
    </footer>

    <div class="footer-bottom">
      <ul>
        <div class="left-links">
          <li>
            <router-link to="/privacy-policy" class="term1"
              >Privacy Policy</router-link
            >
          </li>
          <li><a href="#" class="term2">Cookies Policy</a></li>
        </div>
        <li class="right-link">
          <router-link to="/terms-and-conditions" class="term3"
            >Terms & Conditions</router-link
          >
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "FooterSec",

  methods: {
    redirectHome() {
      this.$router.push({ path: "/" });
    },
  },
};
</script>

<style scoped>
@import url("https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css");

/* Reset styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
}

/* Footer Container */
.footer {
  background: #0057d9;
  color: white;
  padding: 2% 40px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

/* Logo and Contact Section */
.logowithcontect {
  width: 22%;
  padding: 10px 0;
  display: flex;
  flex-direction: column;
}

.logo {
  display: flex;
  align-items: center;
  padding: 0px;
}

.logo img {
  width: 90px;
  height: auto;
  object-fit: cover;
  border-radius: 75%;
}

.contact-info p {
  margin: 5px 0;
}

/* Social Icons */
.social-icons {
  display: flex;
  gap: 15px;
  padding: 10px 0;
}

.social-icons a {
  color: white;
  font-size: 30px;
  text-decoration: none;
  display: inline-block;
  padding: 10px;
  transition: color 0.3s ease;
}

.social-icons a:hover {
  color: #f1c40f;
}

/* Vertical Bar */
.vertical-bar-container {
  display: flex;
}

.vertical-bar {
  width: 2px;
  height: 35vh;
  background-color: white;
}

/* Links and Sections */
.footer .links,
.footer .syllabus,
.footer .previous,
.footer .solved,
.footer .mock {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 10px 15px;
  text-align: center; /* Centering the text */
  font-size: 20px;
}

.footer ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer ul li {
  margin-bottom: 8px;
}

.footer ul li a {
  color: white;
  text-decoration: none;
  display: block;
  padding: 5px 10px;
  transition: color 0.3s ease-in-out;
  font-size: 16px;
}

.footer ul li a:hover {
  color: black;
}

.home,
.syl,
.pre,
.sol,
.moc {
  text-decoration: underline !important;
}

/* Footer Bottom Section */
.footer-bottom {
  padding: 20px 40px;
  background: #0057d9;
  color: white;
  border-top: 0.5px solid wheat;
  display: flex;
}

.footer-bottom ul {
  list-style: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  margin: 0 auto;
  padding: 0;
}

.left-links {
  display: flex;
  gap: 20px;
}

.right-link {
  margin-left: auto;
  padding-right: 30px;
}

.footer-bottom ul li a {
  color: white;
  text-decoration: none;
  transition: color 0.3s ease-in-out;
}

.footer-bottom ul li a:hover {
  color: black;
}

/* Responsive Styles */
@media (max-width: 1024px) {
  .footer {
    flex-direction: column;
    text-align: center;
    padding: 20px;
  }

  .logowithcontect {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 20px;
  }

  .social-icons {
    justify-content: center;
    gap: 15px;
    margin-top: 10px;
  }

  .vertical-bar {
    display: none;
  }

  .footer-bottom {
    width: 100%;
    padding: 15px;
    text-align: center;
  }
}

@media (max-width: 768px) {
  .footer {
    flex-direction: column;
    text-align: center;
    padding: 10px 30px;
  }

  .vertical-bar-container {
    display: none;
  }

  .footer .links,
  .footer .syllabus,
  .footer .previous,
  .footer .solved,
  .footer .mock {
    align-items: center;
  }
}

@media (max-width: 480px) {
  .footer {
    align-items: center;
    justify-content: center;
  }

  .footer-bottom {
    padding: 10px;
  }

  .footer-bottom ul {
    flex-direction: column;
    align-items: center;
  }

  .footer-bottom ul li {
    margin-bottom: 6px;
  }
}
</style>
