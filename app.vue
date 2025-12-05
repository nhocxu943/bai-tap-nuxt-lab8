<template>
  <div class="main-layout">
    <div class="aurora-bg">
      <div class="blob blob-1"></div>
      <div class="blob blob-2"></div>
      <div class="blob blob-3"></div>
    </div>
    <div class="content-wrapper">
      <NuxtPage />
    </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Be+Vietnam+Pro:wght@300;400;500;600;700;900&display=swap');

body {
  margin: 0; padding: 0;
  background-color: #020617; /* Nền đen sâu hơn */
  font-family: 'Be Vietnam Pro', sans-serif;
  color: #ffffff; /* Chữ mặc định màu trắng tinh */
  overflow-x: hidden;
  -webkit-font-smoothing: antialiased;
}

.page-enter-active, .page-leave-active { transition: all 0.4s ease-in-out; }
.page-enter-from { opacity: 0; transform: translateY(20px); }
.page-leave-to { opacity: 0; transform: translateY(-20px); }

.main-layout { position: relative; min-height: 100vh; width: 100%; overflow: hidden; }
.aurora-bg { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; background: #000000; }

.blob {
  position: absolute; border-radius: 50%; filter: blur(90px);
  opacity: 0.3; /* GIẢM TỪ 0.6 XUỐNG 0.3 ĐỂ NỀN TỐI HƠN, DỄ ĐỌC CHỮ */
  animation: float 10s infinite alternate;
}

.blob-1 { top: -10%; left: -10%; width: 50vw; height: 50vw; background: #00dc82; }
.blob-2 { bottom: -10%; right: -10%; width: 40vw; height: 40vw; background: #3b82f6; animation-delay: -5s; }
.blob-3 { top: 40%; left: 40%; width: 30vw; height: 30vw; background: #8b5cf6; animation-delay: -2s; }

@keyframes float {
  0% { transform: translate(0, 0) scale(1); }
  100% { transform: translate(30px, 50px) scale(1.1); }
}

.content-wrapper { position: relative; z-index: 1; min-height: 100vh; display: flex; justify-content: center; align-items: center; padding: 20px; }
</style>