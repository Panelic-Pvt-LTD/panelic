<template>
  <div class="cosmos-theme">
    <!-- Import the standalone preloader component -->
    <Preloader :show="isLoading" />

    <!-- Animated background -->
    <div class="cosmos-bg">
      <div class="stars-container" ref="starsContainer">
        <!-- Stars will be generated in the mounted hook -->
      </div>
      <div class="nebula nebula-1"></div>
      <div class="nebula nebula-2"></div>
      <div class="nebula nebula-3"></div>
      <div class="planet-ring"></div>
    </div>

    <!-- Content wrapper -->
    <div class="content-wrapper" :class="{ 'content-visible': !isLoading }">
      <!-- Left side: Brand panel -->
      <div class="brand-panel">
        <div class="brand-content">
          <div class="logo-container">
            <div class="logo-icon">
              <svg viewBox="0 0 24 24" class="logo-svg">
                <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"></path>
              </svg>
            </div>
            <h1 class="logo-text">PANELIC</h1>
          </div>
          
          <p class="brand-tagline">The next generation Pterodactyl dashboard</p>
          
          <div class="feature-list">
            <div class="feature-item">
              <div class="feature-icon">
                <svg viewBox="0 0 24 24" class="feature-svg">
                  <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"></path>
                </svg>
              </div>
              <div class="feature-text">
                <h3>Secure Authentication</h3>
                <p>Enterprise-grade security with advanced encryption</p>
              </div>
            </div>
            
            <div class="feature-item">
              <div class="feature-icon">
                <svg viewBox="0 0 24 24" class="feature-svg">
                  <rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect>
                  <line x1="9" y1="3" x2="9" y2="21"></line>
                </svg>
              </div>
              <div class="feature-text">
                <h3>Intuitive Dashboard</h3>
                <p>Seamless control over all your servers</p>
              </div>
            </div>
            
            <div class="feature-item">
              <div class="feature-icon">
                <svg viewBox="0 0 24 24" class="feature-svg">
                  <circle cx="12" cy="12" r="10"></circle>
                  <path d="M16 8l-8 8"></path>
                  <path d="M8 8l8 8"></path>
                </svg>
              </div>
              <div class="feature-text">
                <h3>Premium Experience</h3>
                <p>Built for performance and visual excellence</p>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Right side: Login form -->
      <div class="login-panel">
        <div class="login-card">
          <div class="login-header">
            <h2>Welcome back</h2>
            <p>Sign in to your account</p>
          </div>
          
          <form @submit.prevent="handleSubmit" class="login-form">
            <div class="form-group" :class="{ 'focused': emailFocused }">
              <label for="email">Email address</label>
              <div class="input-wrapper">
                <input 
                  id="email" 
                  type="email" 
                  v-model="email" 
                  required
                  @focus="emailFocused = true"
                  @blur="emailFocused = false"
                  placeholder="name@company.com"
                  autocomplete="email"
                />
                <div class="input-icon">
                  <svg viewBox="0 0 24 24">
                    <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm-.4 4.25l-7.07 4.42c-.32.2-.74.2-1.06 0L4.4 8.25a.85.85 0 1 1 .9-1.44L12 11l6.7-4.19a.85.85 0 1 1 .9 1.44z"></path>
                  </svg>
                </div>
              </div>
            </div>
            
            <div class="form-group" :class="{ 'focused': passwordFocused }">
              <div class="label-container">
                <label for="password">Password</label>
                <a href="#" class="forgot-link">Forgot password?</a>
              </div>
              <div class="input-wrapper">
                <input 
                  id="password" 
                  :type="showPassword ? 'text' : 'password'" 
                  v-model="password" 
                  required
                  @focus="passwordFocused = true"
                  @blur="passwordFocused = false"
                  placeholder="••••••••••"
                  autocomplete="current-password"
                />
                <div class="input-icon">
                  <svg viewBox="0 0 24 24">
                    <path d="M12 4C9 4 7 6 7 9v3H6c-.6 0-1 .4-1 1v8c0 .6.4 1 1 1h12c.6 0 1-.4 1-1v-8c0-.6-.4-1-1-1h-1V9c0-3-2-5-5-5zm5 8v7H7v-7h10zm-5-8c1.7 0 3 1.3 3 3v3H9V9c0-1.7 1.3-3 3-3z"></path>
                  </svg>
                </div>
                <button 
                  type="button" 
                  class="password-toggle" 
                  @click="showPassword = !showPassword"
                  aria-label="Toggle password visibility"
                >
                  <svg v-if="showPassword" viewBox="0 0 24 24">
                    <path d="M12 4.5C7 4.5 2.73 7.61 1 12c1.73 4.39 6 7.5 11 7.5s9.27-3.11 11-7.5c-1.73-4.39-6-7.5-11-7.5zM12 17c-2.76 0-5-2.24-5-5s2.24-5 5-5 5 2.24 5 5-2.24 5-5 5zm0-8c-1.66 0-3 1.34-3 3s1.34 3 3 3 3-1.34 3-3-1.34-3-3-3z"></path>
                  </svg>
                  <svg v-else viewBox="0 0 24 24">
                    <path d="M12 7c2.76 0 5 2.24 5 5 0 .65-.13 1.26-.36 1.83l2.92 2.92c1.51-1.26 2.7-2.89 3.43-4.75-1.73-4.39-6-7.5-11-7.5-1.4 0-2.74.25-3.98.7l2.16 2.16C10.74 7.13 11.35 7 12 7zM2 4.27l2.28 2.28.46.46C3.08 8.3 1.78 10.02 1 12c1.73 4.39 6 7.5 11 7.5 1.55 0 3.03-.3 4.38-.84l.42.42L19.73 22 21 20.73 3.27 3 2 4.27zM7.53 9.8l1.55 1.55c-.05.21-.08.43-.08.65 0 1.66 1.34 3 3 3 .22 0 .44-.03.65-.08l1.55 1.55c-.67.33-1.41.53-2.2.53-2.76 0-5-2.24-5-5 0-.79.2-1.53.53-2.2zm4.31-.78l3.15 3.15.02-.16c0-1.66-1.34-3-3-3l-.17.01z"></path>
                  </svg>
                </button>
              </div>
            </div>
            
            <button type="submit" class="sign-in-button">
              <span>Sign in</span>
              <svg viewBox="0 0 24 24" class="button-icon">
                <path d="M13 9l3 3m0 0l-3 3m3-3H8m9 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h9a3 3 0 013 3v1"></path>
              </svg>
            </button>
            
            <div class="alternate-actions">
              <p>Don't have an account? <a href="#" @click.prevent="showSignupModal = true">Create account</a></p>
            </div>
          </form>
        </div>
      </div>
    </div>
    
    <!-- Signup Modal -->
    <div class="modal-overlay" v-if="showSignupModal" @click.self="showSignupModal = false">
      <div class="modal-container">
        <div class="modal-close" @click="showSignupModal = false">
          <svg viewBox="0 0 24 24">
            <path d="M18 6L6 18M6 6l12 12"></path>
          </svg>
        </div>
        
        <div class="modal-header">
          <h2>Create your account</h2>
          <p>Join Panelic to get started</p>
        </div>
        
        <form @submit.prevent="handleSignup" class="modal-form">
          <div class="form-group" :class="{ 'focused': signupEmailFocused }">
            <label for="signup-email">Email address</label>
            <div class="input-wrapper">
              <input 
                id="signup-email" 
                type="email" 
                v-model="signupEmail" 
                required
                @focus="signupEmailFocused = true"
                @blur="signupEmailFocused = false"
                placeholder="name@company.com"
                autocomplete="email"
              />
              <div class="input-icon">
                <svg viewBox="0 0 24 24">
                  <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm-.4 4.25l-7.07 4.42c-.32.2-.74.2-1.06 0L4.4 8.25a.85.85 0 1 1 .9-1.44L12 11l6.7-4.19a.85.85 0 1 1 .9 1.44z"></path>
                </svg>
              </div>
            </div>
          </div>
          
          <div class="form-group" :class="{ 'focused': signupPasswordFocused }">
            <label for="signup-password">Password</label>
            <div class="input-wrapper">
              <input 
                id="signup-password" 
                :type="showSignupPassword ? 'text' : 'password'" 
                v-model="signupPassword" 
                required
                @focus="signupPasswordFocused = true"
                @blur="signupPasswordFocused = false"
                placeholder="••••••••••"
                autocomplete="new-password"
              />
              <div class="input-icon">
                <svg viewBox="0 0 24 24">
                  <path d="M12 4C9 4 7 6 7 9v3H6c-.6 0-1 .4-1 1v8c0 .6.4 1 1 1h12c.6 0 1-.4 1-1v-8c0-.6-.4-1-1-1h-1V9c0-3-2-5-5-5zm5 8v7H7v-7h10zm-5-8c1.7 0 3 1.3 3 3v3H9V9c0-1.7 1.3-3 3-3z"></path>
                </svg>
              </div>
              <button 
                type="button" 
                class="password-toggle" 
                @click="showSignupPassword = !showSignupPassword"
                aria-label="Toggle password visibility"
              >
                <svg v-if="showSignupPassword" viewBox="0 0 24 24">
                  <path d="M12 4.5C7 4.5 2.73 7.61 1 12c1.73 4.39 6 7.5 11 7.5s9.27-3.11 11-7.5c-1.73-4.39-6-7.5-11-7.5zM12 17c-2.76 0-5-2.24-5-5s2.24-5 5-5 5 2.24 5 5-2.24 5-5 5zm0-8c-1.66 0-3 1.34-3 3s1.34 3 3 3 3-1.34 3-3-1.34-3-3-3z"></path>
                </svg>
                <svg v-else viewBox="0 0 24 24">
                  <path d="M12 7c2.76 0 5 2.24 5 5 0 .65-.13 1.26-.36 1.83l2.92 2.92c1.51-1.26 2.7-2.89 3.43-4.75-1.73-4.39-6-7.5-11-7.5-1.4 0-2.74.25-3.98.7l2.16 2.16C10.74 7.13 11.35 7 12 7zM2 4.27l2.28 2.28.46.46C3.08 8.3 1.78 10.02 1 12c1.73 4.39 6 7.5 11 7.5 1.55 0 3.03-.3 4.38-.84l.42.42L19.73 22 21 20.73 3.27 3 2 4.27zM7.53 9.8l1.55 1.55c-.05.21-.08.43-.08.65 0 1.66 1.34 3 3 3 .22 0 .44-.03.65-.08l1.55 1.55c-.67.33-1.41.53-2.2.53-2.76 0-5-2.24-5-5 0-.79.2-1.53.53-2.2zm4.31-.78l3.15 3.15.02-.16c0-1.66-1.34-3-3-3l-.17.01z"></path>
                </svg>
              </button>
            </div>
          </div>
          
          <div class="form-group" :class="{ 'focused': signupConfirmPasswordFocused }">
            <label for="signup-confirm-password">Confirm password</label>
            <div class="input-wrapper">
              <input 
                id="signup-confirm-password" 
                :type="showSignupConfirmPassword ? 'text' : 'password'" 
                v-model="signupConfirmPassword" 
                required
                @focus="signupConfirmPasswordFocused = true"
                @blur="signupConfirmPasswordFocused = false"
                placeholder="••••••••••"
                autocomplete="new-password"
              />
              <div class="input-icon">
                <svg viewBox="0 0 24 24">
                  <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"></path>
                </svg>
              </div>
              <button 
                type="button" 
                class="password-toggle" 
                @click="showSignupConfirmPassword = !showSignupConfirmPassword"
                aria-label="Toggle password visibility"
              >
                <svg v-if="showSignupConfirmPassword" viewBox="0 0 24 24">
                  <path d="M12 4.5C7 4.5 2.73 7.61 1 12c1.73 4.39 6 7.5 11 7.5s9.27-3.11 11-7.5c-1.73-4.39-6-7.5-11-7.5zM12 17c-2.76 0-5-2.24-5-5s2.24-5 5-5 5 2.24 5 5-2.24 5-5 5zm0-8c-1.66 0-3 1.34-3 3s1.34 3 3 3 3-1.34 3-3-1.34-3-3-3z"></path>
                </svg>
                <svg v-else viewBox="0 0 24 24">
                  <path d="M12 7c2.76 0 5 2.24 5 5 0 .65-.13 1.26-.36 1.83l2.92 2.92c1.51-1.26 2.7-2.89 3.43-4.75-1.73-4.39-6-7.5-11-7.5-1.4 0-2.74.25-3.98.7l2.16 2.16C10.74 7.13 11.35 7 12 7zM2 4.27l2.28 2.28.46.46C3.08 8.3 1.78 10.02 1 12c1.73 4.39 6 7.5 11 7.5 1.55 0 3.03-.3 4.38-.84l.42.42L19.73 22 21 20.73 3.27 3 2 4.27zM7.53 9.8l1.55 1.55c-.05.21-.08.43-.08.65 0 1.66 1.34 3 3 3 .22 0 .44-.03.65-.08l1.55 1.55c-.67.33-1.41.53-2.2.53-2.76 0-5-2.24-5-5 0-.79.2-1.53.53-2.2zm4.31-.78l3.15 3.15.02-.16c0-1.66-1.34-3-3-3l-.17.01z"></path>
                </svg>
              </button>
            </div>
            <div class="password-requirements" v-if="signupPasswordFocused || signupConfirmPasswordFocused">
              <p>Password must be at least 8 characters</p>
            </div>
          </div>
          
          <div class="terms-checkbox">
            <label class="checkbox-container">
              <input type="checkbox" v-model="agreeToTerms" required>
              <span class="checkmark"></span>
              <span class="checkbox-label">I agree to the <a href="#" @click.stop>Terms of Service</a> and <a href="#" @click.stop>Privacy Policy</a></span>
            </label>
          </div>
          
          <button type="submit" class="sign-up-button" :disabled="!agreeToTerms">
            <span>Create account</span>
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
// Import the preloader component
import Preloader from './components/Preloader.vue';

export default {
  name: 'App',
  components: {
    Preloader
  },
  data() {
    return {
      email: '',
      password: '',
      showPassword: false,
      emailFocused: false,
      passwordFocused: false,
      isLoading: true,
      
      // Signup modal data
      showSignupModal: false,
      signupEmail: '',
      signupPassword: '',
      signupConfirmPassword: '',
      showSignupPassword: false,
      showSignupConfirmPassword: false,
      signupEmailFocused: false,
      signupPasswordFocused: false,
      signupConfirmPasswordFocused: false,
      agreeToTerms: false
    }
  },
  mounted() {
    // Generate stars with fixed positions
    this.generateStars();
    
    // Simulate loading time (you can replace this with actual loading logic)
    setTimeout(() => {
      this.isLoading = false;
    }, 2500);
  },
  methods: {
    generateStars() {
      const starsContainer = this.$refs.starsContainer;
      const starCount = 200;
      
      // Clear any existing stars
      starsContainer.innerHTML = '';
      
      // Create stars with fixed random positions
      for (let i = 0; i < starCount; i++) {
        const star = document.createElement('div');
        star.className = 'star';
        
        // Set fixed random positions and animation delays
        star.style.top = `${Math.random() * 100}%`;
        star.style.left = `${Math.random() * 100}%`;
        star.style.animationDelay = `${Math.random() * 10}s`;
        
        // Add size variation
        if (i % 3 === 0) {
          star.classList.add('star-large');
        } else if (i % 2 === 0) {
          star.classList.add('star-small');
        }
        
        starsContainer.appendChild(star);
      }
    },
    handleSubmit() {
      console.log('Login attempt with:', {
        email: this.email,
        password: this.password
      });
      // Here you would typically call your authentication API
    },
    handleSignup() {
      if (this.signupPassword !== this.signupConfirmPassword) {
        alert("Passwords don't match");
        return;
      }
      
      console.log('Signup attempt with:', {
        email: this.signupEmail,
        password: this.signupPassword
      });
      // Here you would typically call your user registration API
      
      // Close the modal after submission
      this.showSignupModal = false;
      
      // Reset the form
      this.signupEmail = '';
      this.signupPassword = '';
      this.signupConfirmPassword = '';
      this.agreeToTerms = false;
    }
  }
}
</script>

<style>
/* Base reset */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #000;
  color: #fff;
  overflow-x: hidden;
}

/* Cosmos theme styling */
.cosmos-theme {
  min-height: 100vh;
  position: relative;
  background-color: #050505;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

/* Premium animated background */
.cosmos-bg {
  position: fixed;
  inset: 0;
  background: linear-gradient(to bottom, #050505, #0c0c1d);
  z-index: 0;
  overflow: hidden;
}

.stars-container {
  position: absolute;
  inset: 0;
  z-index: 0;
}

.star {
  position: absolute;
  width: 2px;
  height: 2px;
  background-color: rgba(255, 255, 255, 0.7);
  border-radius: 50%;
  z-index: 1;
  animation: twinkle 5s infinite;
}

.star-small {
  width: 1px;
  height: 1px;
}

.star-large {
  width: 3px;
  height: 3px;
  background-color: rgba(224, 227, 255, 0.8);
}

@keyframes twinkle {
  0%, 100% { opacity: 0.2; }
  50% { opacity: 1; }
}

.nebula {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.2;
  z-index: 0;
  animation: pulse 15s ease-in-out infinite alternate;
}

.nebula-1 {
  top: -10%;
  right: -10%;
  width: 70vw;
  height: 70vw;
  background: radial-gradient(circle, rgba(92, 58, 180, 0.2), rgba(77, 0, 160, 0.1), transparent 70%);
}

.nebula-2 {
  bottom: -20%;
  left: -10%;
  width: 60vw;
  height: 60vw;
  background: radial-gradient(circle, rgba(0, 108, 172, 0.15), rgba(21, 12, 117, 0.1), transparent 70%);
  animation-delay: 3s;
}

.nebula-3 {
  top: 40%;
  left: 30%;
  width: 50vw;
  height: 50vw;
  background: radial-gradient(circle, rgba(92, 0, 138, 0.1), rgba(41, 0, 99, 0.05), transparent 70%);
  animation-delay: 6s;
}

.planet-ring {
  position: fixed;
  top: 45%;
  left: 60%;
  width: 100vw;
  height: 8vh;
  background: linear-gradient(
    90deg,
    transparent 0%,
    rgba(135, 38, 192, 0.03) 20%,
    rgba(193, 97, 255, 0.1) 50%,
    rgba(135, 38, 192, 0.03) 80%,
    transparent 100%
  );
  transform: rotate(-25deg);
  z-index: 0;
  filter: blur(5px);
}

@keyframes pulse {
  0% { 
    opacity: 0.1;
    transform: scale(1);
  }
  50% { 
    opacity: 0.2;
    transform: scale(1.1);
  }
  100% { 
    opacity: 0.1;
    transform: scale(1);
  }
}

/* Content layout */
.content-wrapper {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  width: 100%;
  padding: 0;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.8s ease 0.3s, transform 0.8s ease 0.3s;
}

@media (min-width: 1024px) {
  .content-wrapper {
    flex-direction: row;
  }
}

/* Brand panel styling */
.brand-panel {
  flex: 1;
  display: none;
  position: relative;
  padding: 4rem 2rem;
}

@media (min-width: 1024px) {
  .brand-panel {
    display: flex;
    align-items: center;
    justify-content: center;
  }
}

.brand-content {
  max-width: 480px;
  opacity: 0;
  animation: fadeSlideUp 0.8s ease-out forwards;
  animation-delay: 0.2s;
}

.logo-container {
  display: flex;
  align-items: center;
  margin-bottom: 2rem;
}

.logo-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 3.5rem;
  height: 3.5rem;
  border-radius: 12px;
  background: linear-gradient(135deg, rgba(101, 39, 190, 0.8), rgba(39, 10, 101, 0.8));
  box-shadow: 
    0 10px 25px rgba(101, 39, 190, 0.2),
    0 0 0 1px rgba(101, 39, 190, 0.1);
  margin-right: 1rem;
}

.logo-svg {
  width: 1.8rem;
  height: 1.8rem;
  stroke: white;
  stroke-width: 2;
  fill: none;
}

.logo-text {
  font-size: 2.25rem;
  font-weight: 700;
  letter-spacing: 0.05em;
  background: linear-gradient(90deg, #fff, #a594ff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.brand-tagline {
  font-size: 1.25rem;
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 3rem;
  font-weight: 300;
  line-height: 1.6;
}

.feature-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.feature-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.feature-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 2.5rem;
  height: 2.5rem;
  border-radius: 10px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  flex-shrink: 0;
}

.feature-svg {
  width: 1.25rem;
  height: 1.25rem;
  stroke: rgba(255, 255, 255, 0.9);
  stroke-width: 2;
  fill: none;
}

.feature-text h3 {
  font-size: 1rem;
  font-weight: 600;
  margin-bottom: 0.25rem;
  color: rgba(255, 255, 255, 0.9);
}

.feature-text p {
  font-size: 0.875rem;
  color: rgba(255, 255, 255, 0.6);
  line-height: 1.5;
}

/* Login panel styling */
.login-panel {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 2rem;
}

.login-card {
  width: 100%;
  max-width: 450px;
  background: rgba(17, 17, 27, 0.8);
  backdrop-filter: blur(16px);
  border-radius: 1.5rem;
  padding: 2.5rem;
  box-shadow: 
    0 25px 50px rgba(0, 0, 0, 0.2),
    0 0 0 1px rgba(255, 255, 255, 0.05);
  opacity: 0;
  animation: fadeSlideUp 0.8s ease-out forwards;
  animation-delay: 0.4s;
  transform: perspective(1000px) rotateX(0deg);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.login-card:hover {
  transform: perspective(1000px) rotateX(2deg) translateY(-5px);
  box-shadow: 
    0 30px 60px rgba(0, 0, 0, 0.3),
    0 0 0 1px rgba(255, 255, 255, 0.08);
}

.login-header {
  text-align: center;
  margin-bottom: 2.5rem;
}

.login-header h2 {
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  background: linear-gradient(90deg, #fff, #a594ff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.login-header p {
  font-size: 0.95rem;
  color: rgba(255, 255, 255, 0.6);
}

.login-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  margin-bottom: 0;
}

.form-group {
  position: relative;
}

.label-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.form-group label {
  display: block;
  font-size: 0.875rem;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 0.5rem;
  transition: color 0.2s ease;
}

.form-group.focused label {
  color: rgba(255, 255, 255, 1);
}

.input-wrapper {
  position: relative;
}

.form-group input {
  width: 100%;
  background-color: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 0.75rem;
  padding: 0.875rem 1rem 0.875rem 2.75rem;
  font-size: 0.95rem;
  color: white;
  transition: all 0.2s ease;
  outline: none;
}

.form-group input::placeholder {
  color: rgba(255, 255, 255, 0.3);
}

.form-group input:focus {
  background-color: rgba(255, 255, 255, 0.06);
  border-color: rgba(101, 39, 190, 0.6);
  box-shadow: 0 0 0 3px rgba(101, 39, 190, 0.1);
}

.input-icon {
  position: absolute;
  left: 0.75rem;
  top: 50%;
  transform: translateY(-50%);
}

.input-icon svg {
  width: 1.25rem;
  height: 1.25rem;
  fill: rgba(255, 255, 255, 0.4);
}

.form-group.focused .input-icon svg {
  fill: rgba(255, 255, 255, 0.7);
}

.password-toggle {
  position: absolute;
  right: 0.75rem;
  top: 50%;
  transform: translateY(-50%);
  background: transparent;
  border: none;
  color: rgba(255, 255, 255, 0.4);
  cursor: pointer;
  transition: color 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.password-toggle:hover {
  color: rgba(255, 255, 255, 0.7);
}

.password-toggle svg {
  width: 1.25rem;
  height: 1.25rem;
  fill: currentColor;
}

.forgot-link {
  font-size: 0.75rem;
  color: rgba(255, 255, 255, 0.5);
  text-decoration: none;
  transition: color 0.2s ease;
}

.forgot-link:hover {
  color: #a594ff;
  text-decoration: underline;
}

.sign-in-button {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  padding: 0.875rem 1.5rem;
  background: linear-gradient(135deg, #6527be, #9254de);
  color: white;
  font-weight: 600;
  font-size: 0.95rem;
  border: none;
  border-radius: 0.75rem;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 5px 15px rgba(101, 39, 190, 0.2);
  overflow: hidden;
  margin-top: 1.5rem;
}

.sign-in-button:hover {
  background: linear-gradient(135deg, #7433d4, #a56cf0);
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(101, 39, 190, 0.3);
}

.sign-in-button:active {
  transform: translateY(0);
  box-shadow: 0 3px 10px rgba(101, 39, 190, 0.2);
}

.button-icon {
  width: 1.25rem;
  height: 1.25rem;
  margin-left: 0.5rem;
  stroke: white;
  stroke-width: 2;
  fill: none;
}

.alternate-actions {
  text-align: center;
  margin-top: 1.5rem;
  font-size: 0.875rem;
  color: rgba(255, 255, 255, 0.6);
}

.alternate-actions a {
  color: rgba(255, 255, 255, 0.9);
  text-decoration: none;
  font-weight: 500;
  transition: color 0.2s ease;
}

.alternate-actions a:hover {
  color: #a594ff;
  text-decoration: underline;
}

/* Animations */
@keyframes fadeSlideUp {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Responsive adjustments */
@media (max-width: 1023px) {
  .login-panel {
    min-height: auto;
  }
  
  .login-card {
    padding: 2rem;
    margin: 2rem 0;
  }
}

@media (max-width: 640px) {
  .login-card {
    padding: 1.5rem;
  }
}

/* Autofill styling */
input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus,
input:-webkit-autofill:active {
  -webkit-box-shadow: 0 0 0 30px #1a1a2e inset !important;
  -webkit-text-fill-color: white !important;
  caret-color: white;
}

/* Remove login divider and social buttons since we're removing OAuth */
.login-divider,
.social-login {
  display: none;
}

/* Content transition */
.content-wrapper {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.8s ease 0.3s, transform 0.8s ease 0.3s;
}

.content-visible {
  opacity: 1;
  transform: translateY(0);
}

/* Modal Styling */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  backdrop-filter: blur(8px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 1rem;
  animation: fadeIn 0.3s ease-out;
}

.modal-container {
  width: 100%;
  max-width: 500px;
  background: rgba(17, 17, 27, 0.95);
  border-radius: 1.5rem;
  padding: 2.5rem;
  position: relative;
  box-shadow: 
    0 25px 50px rgba(0, 0, 0, 0.3),
    0 0 0 1px rgba(255, 255, 255, 0.05);
  animation: modalSlideUp 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  max-height: 90vh;
  overflow-y: auto;
}

.modal-close {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  width: 2rem;
  height: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.05);
  transition: all 0.2s ease;
}

.modal-close:hover {
  background: rgba(255, 255, 255, 0.1);
}

.modal-close svg {
  width: 1.25rem;
  height: 1.25rem;
  stroke: rgba(255, 255, 255, 0.7);
  stroke-width: 2;
  fill: none;
}

.modal-header {
  text-align: center;
  margin-bottom: 2rem;
}

.modal-header h2 {
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  background: linear-gradient(90deg, #fff, #a594ff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.modal-header p {
  font-size: 0.95rem;
  color: rgba(255, 255, 255, 0.6);
}

.modal-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.password-requirements {
  margin-top: 0.5rem;
  font-size: 0.75rem;
  color: rgba(255, 255, 255, 0.5);
}

.terms-checkbox {
  margin-top: 0.5rem;
}

.checkbox-container {
  display: flex;
  align-items: center;
  position: relative;
  cursor: pointer;
  font-size: 0.875rem;
  color: rgba(255, 255, 255, 0.7);
  user-select: none;
}

.checkbox-container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: relative;
  height: 20px;
  width: 20px;
  background-color: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 4px;
  margin-right: 10px;
  transition: all 0.2s ease;
}

.checkbox-container:hover input ~ .checkmark {
  background-color: rgba(255, 255, 255, 0.1);
}

.checkbox-container input:checked ~ .checkmark {
  background-color: #7c3aed;
  border-color: #7c3aed;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.checkbox-container input:checked ~ .checkmark:after {
  display: block;
}

.checkbox-container .checkmark:after {
  left: 7px;
  top: 3px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
}

.checkbox-label {
  line-height: 1.5;
}

.checkbox-label a {
  color: #a594ff;
  text-decoration: none;
  transition: all 0.2s ease;
}

.checkbox-label a:hover {
  text-decoration: underline;
}

.sign-up-button {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  padding: 0.875rem 1.5rem;
  background: linear-gradient(135deg, #6527be, #9254de);
  color: white;
  font-weight: 600;
  font-size: 0.95rem;
  border: none;
  border-radius: 0.75rem;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 5px 15px rgba(101, 39, 190, 0.2);
  margin-top: 1rem;
}

.sign-up-button:hover:not(:disabled) {
  background: linear-gradient(135deg, #7433d4, #a56cf0);
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(101, 39, 190, 0.3);
}

.sign-up-button:active:not(:disabled) {
  transform: translateY(0);
  box-shadow: 0 3px 10px rgba(101, 39, 190, 0.2);
}

.sign-up-button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

@keyframes modalSlideUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Responsive adjustments for the modal */
@media (max-width: 640px) {
  .modal-container {
    padding: 1.5rem;
  }
}
</style>
