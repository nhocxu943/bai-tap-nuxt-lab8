<template>
  <div class="glass-card home-card">
    <div class="logo-container">
      <svg class="nuxt-logo" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
         <path d="M2.5 12L12 21.5L21.5 12L12 2.5L2.5 12Z" stroke="#00DC82" stroke-width="2" stroke-linejoin="round"/>
         <path d="M12 2.5V21.5" stroke="#00DC82" stroke-width="2" stroke-linejoin="round"/>
      </svg>
      <div class="glow-effect"></div>
    </div>

    <h1 class="main-title">
      Mastering <span class="gradient-text">Nuxt.js</span>
    </h1>

    <p class="subtitle">
      Khám phá sức mạnh của <strong>SSR</strong> và <strong>SPA</strong> với Framework Vue.js hiện đại nhất.
      Trải nghiệm phát triển web chưa bao giờ mượt mà đến thế.
    </p>

    <div class="button-row">
      <NuxtLink to="/about" class="btn btn-glow">
        <span>So sánh vs Vue.js</span>
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
      </NuxtLink>
      
      <NuxtLink to="/benefits" class="btn btn-glass">
        <span>Lợi ích nổi bật</span>
      </NuxtLink>
    </div>
  </div>
</template>

<style scoped>
/* NỀN ĐEN MỜ (High Contrast) */
.glass-card {
  background: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
  border-radius: 32px;
  padding: 60px 40px;
  text-align: center;
  max-width: 600px;
  width: 100%;
  animation: slideUp 0.8s cubic-bezier(0.2, 0.8, 0.2, 1);
}

@keyframes slideUp { from { opacity: 0; transform: translateY(40px); } to { opacity: 1; transform: translateY(0); } }

.logo-container { position: relative; width: 80px; height: 80px; margin: 0 auto 30px; }
.nuxt-logo { width: 100%; height: 100%; filter: drop-shadow(0 0 10px #00dc82); animation: spinLogo 20s linear infinite; }
.glow-effect { position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); width: 120%; height: 120%; background: #00dc82; filter: blur(40px); opacity: 0.2; border-radius: 50%; z-index: -1; }

@keyframes spinLogo { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }

.main-title { font-size: 3.5rem; font-weight: 800; line-height: 1.1; margin-bottom: 20px; letter-spacing: -1px; color: white; }
.gradient-text { background: linear-gradient(135deg, #00dc82 0%, #36e4da 100%); -webkit-background-clip: text; background-clip: text; -webkit-text-fill-color: transparent; }

/* CHỮ MÔ TẢ: Sáng hơn */
.subtitle { font-size: 1.1rem; color: #e2e8f0; line-height: 1.6; margin-bottom: 40px; }
.subtitle strong { color: #ffffff; font-weight: 600; }

.button-row { display: flex; gap: 20px; justify-content: center; flex-wrap: wrap; }
.btn { display: flex; align-items: center; gap: 10px; padding: 14px 28px; border-radius: 16px; font-weight: 600; text-decoration: none; transition: all 0.3s ease; }
.btn svg { width: 20px; height: 20px; transition: transform 0.3s; }

.btn-glow { background: linear-gradient(135deg, #00dc82 0%, #00a86b 100%); color: #002e1f; box-shadow: 0 0 20px rgba(0, 220, 130, 0.3); }
.btn-glow:hover { transform: translateY(-3px); box-shadow: 0 10px 30px rgba(0, 220, 130, 0.5); }
.btn-glow:hover svg { transform: translateX(5px); }

.btn-glass { background: rgba(255, 255, 255, 0.1); color: white; border: 1px solid rgba(255, 255, 255, 0.2); }
.btn-glass:hover { background: rgba(255, 255, 255, 0.2); transform: translateY(-3px); border-color: white; }
</style>