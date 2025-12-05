<template>
  <div class="glass-card page-card">
    <div class="header">
      <h1 class="page-title">Tại sao chọn <span class="highlight">Nuxt</span>?</h1>
      <p class="sub-text">Bấm vào từng tính năng để xem Code ví dụ thực tế</p>
    </div>

    <!-- Grid các thẻ lợi ích -->
    <div class="grid-benefits">
      <div 
        class="card-item" 
        v-for="(item, index) in benefits" 
        :key="index" 
        @click="openModal(item)"
        :style="{ animationDelay: index * 0.1 + 's' }"
      >
        <div class="icon-box">{{ item.icon }}</div>
        <h3>{{ item.title }}</h3>
        <p>{{ item.desc }}</p>
        <div class="tap-hint">Xem ví dụ &rarr;</div>
      </div>
    </div>

    <div class="footer-nav">
      <NuxtLink to="/" class="btn-home">Về trang chủ</NuxtLink>
      <NuxtLink to="/about" class="btn-next">Xem so sánh &rarr;</NuxtLink>
    </div>

    <!-- 
      QUAN TRỌNG: Dùng Teleport để đưa Modal ra ngoài body
      Giúp thoát khỏi cái khung vuông đen xấu xí 
    -->
    <Teleport to="body">
      <Transition name="tech-modal">
        <div v-if="selectedItem" class="modal-overlay" @click="closeModal">
          <div class="modal-card" @click.stop>
            <!-- Header Modal -->
            <div class="modal-header">
              <div class="modal-icon">{{ selectedItem.icon }}</div>
              <div class="modal-titles">
                <span class="tech-tag">FEATURE DEMO</span>
                <h2>{{ selectedItem.title }}</h2>
              </div>
              <button class="close-btn" @click="closeModal">&times;</button>
            </div>

            <!-- Body Modal -->
            <div class="modal-body">
              <p class="full-desc">{{ selectedItem.fullDesc }}</p>

              <!-- Khung Code Ví dụ -->
              <div class="code-block">
                <div class="code-header">
                  <div class="dots">
                    <span></span><span></span><span></span>
                  </div>
                  <span class="file-name">{{ selectedItem.fileName }}</span>
                </div>
                <pre><code><span v-html="selectedItem.codeExample"></span></code></pre>
              </div>
            </div>
          </div>
        </div>
      </Transition>
    </Teleport>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const benefits = [
  { 
    icon: '🚀', 
    title: 'Siêu Tốc Độ (SSR)', 
    desc: 'Nuxt render sẵn HTML giúp web tải tức thì và chuẩn SEO.',
    fullDesc: 'Với Server-Side Rendering (SSR), Nuxt xử lý trang web trên server và gửi về HTML hoàn chỉnh. Người dùng không phải chờ tải JavaScript để thấy nội dung.',
    fileName: 'nuxt.config.ts',
    codeExample: `<span class="kwd">export</span> <span class="kwd">default</span> defineNuxtConfig({
  <span class="prop">ssr</span>: <span class="bool">true</span>, 
  <span class="cmt">// Chỉ 1 dòng config để bật chế độ siêu tốc</span>
  <span class="prop">nitro</span>: {
    <span class="prop">preset</span>: <span class="str">'node-server'</span>
  }
})`
  },
  { 
    icon: '📂', 
    title: 'File System Routing', 
    desc: 'Tự động tạo đường dẫn dựa trên cấu trúc thư mục.',
    fullDesc: 'Bạn không cần file router.js phức tạp. Chỉ cần tạo file trong thư mục "pages", Nuxt sẽ tự động biến nó thành đường dẫn website.',
    fileName: 'Folder Structure',
    codeExample: `pages/
├── <span class="file">index.vue</span>        <span class="cmt">// -> /</span>
├── <span class="file">about.vue</span>        <span class="cmt">// -> /about</span>
└── <span class="dir">users/</span>
    └── <span class="file">[id].vue</span>    <span class="cmt">// -> /users/1, /users/2...</span>`
  },
  { 
    icon: '🔍', 
    title: 'SEO Friendly', 
    desc: 'Tích hợp sẵn các thẻ Meta giúp Google lên Top dễ dàng.',
    fullDesc: 'Nuxt cung cấp bộ công cụ "useSeoMeta" cực mạnh. Bạn có thể định nghĩa tiêu đề, ảnh chia sẻ Facebook (OG Image) ngay trong component.',
    fileName: 'app.vue',
    codeExample: `<span class="func">useSeoMeta</span>({
  <span class="prop">title</span>: <span class="str">'Trang chủ tuyệt đẹp'</span>,
  <span class="prop">description</span>: <span class="str">'Web chạy nhanh như gió'</span>,
  <span class="prop">ogImage</span>: <span class="str">'/banner.png'</span>
})`
  },
  { 
    icon: '📦', 
    title: 'Auto Imports', 
    desc: 'Không cần import thủ công các hàm phổ biến của Vue.',
    fullDesc: 'Nuxt tự động quét và import các hàm như ref, computed, watch... Bạn chỉ việc dùng, giúp code gọn gàng hơn 30%.',
    fileName: 'counter.vue',
    codeExample: `<span class="tag">&lt;script setup&gt;</span>
  <span class="cmt">// Không cần import { ref } from 'vue' !!!</span>
  <span class="kwd">const</span> count = <span class="func">ref</span>(0)
  
  <span class="cmt">// Tự động nhận diện components</span>
  <span class="cmt">// Không cần import MyButton</span>
<span class="tag">&lt;/script&gt;</span>`
  }
]

const selectedItem = ref(null)

const openModal = (item) => { selectedItem.value = item }
const closeModal = () => { selectedItem.value = null }
</script>

<style scoped>
/* --- GIỮ STYLE CŨ CỦA TRANG CHÍNH --- */
.glass-card {
  background: rgba(0, 0, 0, 0.6); backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.15); border-radius: 32px;
  padding: 40px; max-width: 900px; width: 100%;
  box-shadow: 0 20px 40px rgba(0,0,0,0.4);
}
.header { text-align: center; margin-bottom: 40px; }
.page-title { font-size: 2.5rem; margin: 0; color: white; font-weight: 800; }
.highlight { color: #00dc82; text-shadow: 0 0 20px rgba(0, 220, 130, 0.4); }
.sub-text { color: #94a3b8; margin-top: 10px; font-size: 1rem; }

.grid-benefits { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; }
.card-item {
  background: rgba(255, 255, 255, 0.05); border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 25px; border-radius: 20px; text-align: center;
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
  cursor: pointer; position: relative; overflow: hidden;
  animation: fadeUp 0.6s backwards;
}
@keyframes fadeUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
.card-item:hover { background: rgba(0, 220, 130, 0.1); border-color: #00dc82; transform: translateY(-8px); box-shadow: 0 10px 30px -10px rgba(0, 220, 130, 0.3); }
.icon-box { font-size: 2.5rem; margin-bottom: 15px; transition: 0.3s; }
.card-item:hover .icon-box { transform: scale(1.2); }
.card-item h3 { margin: 0 0 10px; color: #ffffff; font-size: 1.2rem; font-weight: 700; }
.card-item p { margin: 0; color: #cbd5e1; font-size: 0.9rem; line-height: 1.5; }
.tap-hint { margin-top: 15px; font-size: 0.8rem; color: #00dc82; font-weight: bold; opacity: 0; transform: translateY(10px); transition: 0.3s; }
.card-item:hover .tap-hint { opacity: 1; transform: translateY(0); }

/* --- STYLE MODAL ĐÃ SỬA (FIX LỖI NỀN ĐEN VUÔNG) --- */
.modal-overlay {
  position: fixed; 
  top: 0; left: 0; 
  width: 100vw; height: 100vh; /* Phủ toàn màn hình */
  
  /* Chỉnh nền mờ nhẹ hơn, không đen kịt */
  background: rgba(0, 0, 0, 0.6); 
  backdrop-filter: blur(10px); /* Làm mờ toàn bộ trang web phía sau */
  
  display: flex; justify-content: center; align-items: center; 
  z-index: 9999; /* Luôn nằm trên cùng */
  padding: 20px;
}

.modal-card {
  background: #0f172a; width: 100%; max-width: 600px;
  border-radius: 20px; border: 1px solid #1e293b;
  box-shadow: 0 25px 100px rgba(0,0,0,0.8); /* Đổ bóng sâu hơn */
  overflow: hidden;
  position: relative;
}
.modal-card::before { content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 4px; background: linear-gradient(90deg, #00dc82, #3b82f6); }

.modal-header { padding: 25px; display: flex; align-items: center; gap: 20px; background: rgba(255,255,255,0.02); border-bottom: 1px solid rgba(255,255,255,0.05); }
.modal-icon { font-size: 2.5rem; }
.tech-tag { font-size: 0.7rem; color: #3b82f6; font-weight: 900; letter-spacing: 1px; background: rgba(59, 130, 246, 0.1); padding: 4px 8px; border-radius: 4px; }
.modal-titles h2 { margin: 5px 0 0; color: white; font-size: 1.5rem; }
.close-btn { margin-left: auto; background: none; border: none; color: #64748b; font-size: 2rem; cursor: pointer; transition: 0.2s; }
.close-btn:hover { color: white; transform: rotate(90deg); }

.modal-body { padding: 30px; }
.full-desc { color: #cbd5e1; line-height: 1.6; margin-bottom: 25px; font-size: 1rem; }

/* CODE BLOCK */
.code-block { background: #020617; border-radius: 12px; border: 1px solid #1e293b; overflow: hidden; font-family: 'Consolas', monospace; }
.code-header { background: #1e293b; padding: 10px 15px; display: flex; align-items: center; }
.dots { display: flex; gap: 6px; margin-right: 15px; }
.dots span { width: 10px; height: 10px; border-radius: 50%; background: #475569; }
.dots span:nth-child(1) { background: #ef4444; }
.dots span:nth-child(2) { background: #eab308; }
.dots span:nth-child(3) { background: #22c55e; }
.file-name { color: #94a3b8; font-size: 0.8rem; font-style: italic; }
pre { margin: 0; padding: 20px; overflow-x: auto; white-space: pre-wrap; color: #e2e8f0; font-size: 0.9rem; line-height: 1.5; }

/* Syntax Color */
:deep(.kwd) { color: #c084fc; }
:deep(.str) { color: #4ade80; }
:deep(.func) { color: #60a5fa; }
:deep(.cmt) { color: #64748b; font-style: italic; }
:deep(.prop) { color: #93c5fd; }
:deep(.bool) { color: #f472b6; }
:deep(.tag) { color: #f87171; }
:deep(.file) { color: #facc15; }
:deep(.dir) { color: #38bdf8; font-weight: bold; }

/* Footer */
.footer-nav { margin-top: 40px; display: flex; justify-content: center; gap: 20px; }
.btn-home { color: #e2e8f0; text-decoration: none; padding: 10px 20px; font-weight: 600; border-radius: 10px; transition: 0.3s; }
.btn-home:hover { background: rgba(255,255,255,0.1); }
.btn-next { background: #00dc82; color: #020617; padding: 10px 25px; border-radius: 10px; text-decoration: none; font-weight: bold; transition: 0.3s; }
.btn-next:hover { box-shadow: 0 0 20px rgba(0, 220, 130, 0.4); transform: scale(1.05); }

/* Animation Modal */
.tech-modal-enter-active, .tech-modal-leave-active { transition: all 0.3s ease; }
.tech-modal-enter-from, .tech-modal-leave-to { opacity: 0; transform: scale(0.95) translateY(10px); }
</style>