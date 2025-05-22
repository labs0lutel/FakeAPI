<template>
  <div class="profile-page">
    <div class="profile-container" v-if="user">
      <h1 class="profile-title">My profile</h1>
      <div class="profile-content">
        <div class="profile-info">
          <div class="info-line"><span class="info-label">Username:</span> {{ user.username }}</div>
          <div class="info-line"><span class="info-label">Name:</span> {{ user.firstName }}</div>
          <div class="info-line"><span class="info-label">Lastname:</span> {{ user.lastName }}</div>
          <div class="info-line"><span class="info-label">Gender:</span> {{ user.gender }}</div>
          <div class="info-line"><span class="info-label">Email:</span> {{ user.email }}</div>
        </div>
        <div class="profile-image-container">
          <img src="/cat.svg">
        </div>
      </div>
    </div>
    <div v-else-if="error" class="error-message">
      {{ error }}
    </div>
    <footer class="footer">
      <div class="social-links">
        <a href="#" class="social-link"><img src="/fb.svg" alt="Facebook"></a>
        <a href="#" class="social-link"><img src="/insta.svg" alt="Instagram"></a>
        <a href="#" class="social-link"><img src="/tw.svg" alt="Twitter"></a>
        <a href="#" class="social-link"><img src="/lin.svg" alt="Linkedin"></a>
      </div>
      <p class="copyright">Copyright ©2020 All rights reserved</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'ProfileView',
  data() {
    return {
      user: null,
      error: null
    }
  },
  created() {
    this.loadProfile()
  },
  methods: {
    loadProfile() {
      try {
        const token = localStorage.getItem('token')
        if (!token) {
          this.$router.push('/login')
          return
        }

        const userData = localStorage.getItem('user')
        if (!userData) {
          throw new Error('Данные пользователя не найдены')
        }

        this.user = JSON.parse(userData)
      } catch (error) {
        this.error = error.message
      }
    }
  }
}
</script>

<style scoped>
.profile-page {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  font-family: 'Heebo', sans-serif;
  padding: 32px;
  background-color: #fff;
}

.profile-container {
  flex: 1;
  max-width: 800px;
  margin: 0 auto;
  width: 100%;
  padding: 32px 0;
}

.profile-title {
  font-size: 34px;
  font-weight: 700;
  color: #21243D;
  margin-bottom: 40px;
}

.profile-content {
  display: flex;
  justify-content: space-between;
  gap: 48px;
  align-items: flex-start; 
}

.profile-info {
  display: block; 
}

.info-line {
  display: flex; 
  width: fit-content; 
  margin-bottom: 12px;
  color: #21243D;
  white-space: nowrap;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.25);
  padding: 8px 12px;
  background: white;
}

.info-label {
  display: inline-block;
  min-width: 80px; 
  font-weight: 500;
}

.profile-image-container {
  width: 240px;
  height: 240px;
}

.profile-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.error-message {
  color: #FF6464;
  text-align: center;
  padding: 32px;
  font-size: 16px;
}

.footer {
  text-align: center;
  padding: 32px 0;
  margin-top: auto;
}

.social-links {
  margin-bottom: 16px;
}

.social-link {
  color: #21243D;
  font-size: 24px;
  margin: 0 8px;
  text-decoration: none;
  transition: color 0.3s;
}

.social-link:hover {
  color: #FF6464;
}

.copyright {
  color: #21243D;
  font-size: 14px;
  margin: 0;
  font-weight: 400;
}
</style>