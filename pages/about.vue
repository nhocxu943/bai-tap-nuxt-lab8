<template>
  <div class="glass-card page-card">
    <div class="header">
      <h1 class="page-title">So sánh <span class="highlight">Core</span></h1>
      <p class="page-desc">Bấm vào từng ô để xem chi tiết kỹ thuật</p>
    </div>

    <div class="comparison-container">
      <!-- HÀNG 1: RENDERING -->
      <div class="compare-item">
        <div class="criteria">Rendering</div>
        <div class="vs-row">
          <div class="box nuxt clickable" @click="showDetail('ssr')">
            <span class="tag">Nuxt</span>
            <strong>SSR</strong> (Server-Side)
            <p>Bấm để xem chi tiết</p>
          </div>
          <div class="divider">VS</div>
          <div class="box vue clickable" @click="showDetail('csr')">
            <span class="tag">Vue</span>
            <strong>CSR</strong> (Client-Side)
            <p>Bấm để xem chi tiết</p>
          </div>
        </div>
      </div>

      <!-- HÀNG 2: ROUTING -->
      <div class="compare-item">
        <div class="criteria">Routing</div>
        <div class="vs-row">
          <div class="box nuxt clickable" @click="showDetail('auto-route')">
            <strong>Tự động</strong>
            <p>File System Routing</p>
          </div>
          <div class="divider">VS</div>
          <div class="box vue clickable" @click="showDetail('manual-route')">
            <strong>Thủ công</strong>
            <p>Vue Router Config</p>
          </div>
        </div>
      </div>
    </div>

    <div class="footer-nav">
      <NuxtLink to="/" class="btn-back">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 12H5M12 19l-7-7 7-7"/></svg>
        Quay về
      </NuxtLink>
    </div>

    <!-- 
      QUAN TRỌNG: Thêm Teleport to="body"
      Để Modal thoát khỏi thẻ glass-card và phủ toàn màn hình 
    -->
    <Teleport to="body">
      <Transition name="modal-pop">
        <div v-if="selectedInfo" class="modal-overlay" @click="closeModal">
          <div class="modal-card" :class="selectedInfo.type" @click.stop>
            
            <!-- Header đẹp có icon -->
            <div class="modal-header">
              <div class="icon-circle">
                <span v-if="selectedInfo.type === 'nuxt'">💚</span>
                <span v-else>🧩</span>
              </div>
              <div class="header-text">
                <span class="badge">{{ selectedInfo.type === 'nuxt' ? 'Nuxt Framework' : 'Vue Library' }}</span>
                <h2>{{ selectedInfo.title }}</h2>
              </div>
              <button class="close-btn" @click="closeModal">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 6L6 18M6 6l12 12"/></svg>
              </button>
            </div>

            <!-- Nội dung -->
            <div class="modal-body">
              <p class="summary">{{ selectedInfo.summary }}</p>
              
              <div class="detail-grid">
                <div v-for="(item, index) in selectedInfo.details" :key="index" class="detail-item">
                  <div class="check-icon">✓</div>
                  <span>{{ item }}</span>
                </div>
              </div>
            </div>

            <!-- Footer trang trí -->
            <div class="modal-footer">
              <button class="btn-got-it" @click="closeModal">Đã hiểu</button>
            </div>
          </div>
        </div>
      </Transition>
    </Teleport>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const dataMap = {
  'ssr': {
    type: 'nuxt',
    title: 'Server-Side Rendering',
    summary: 'SSR render HTML ngay trên Server trước khi gửi về. Đây là lý do chính khiến các website Nuxt có SEO cực tốt và load cực nhanh.',
    details: [
      'Tối ưu SEO tuyệt đối cho Google.',
      'Tăng tốc độ tải trang lần đầu (FCP).',
      'Hiển thị đầy đủ hình ảnh khi chia sẻ link.',
      'Giảm tải xử lý cho máy người dùng.'
    ]
  },
  'csr': {
    type: 'vue',
    title: 'Client-Side Rendering',
    summary: 'CSR là mặc định của Vue thuần. Trình duyệt tải trang trắng về rồi mới chạy JS để vẽ giao diện. Mượt mà nhưng SEO kém.',
    details: [
      'Trải nghiệm chuyển trang mượt như App.',
      'Server nhẹ gánh, chỉ cần gửi file tĩnh.',
      'SEO kém hơn do bot thấy trang trắng trước.',
      'Phù hợp Dashboard nội bộ, Admin.'
    ]
  },
  'auto-route': {
    type: 'nuxt',
    title: 'File System Routing',
    summary: 'Quên đi việc cấu hình router thủ công! Với Nuxt, cấu trúc thư mục của bạn chính là đường dẫn website.',
    details: [
      'Tự động tạo route từ tên file.',
      'Hỗ trợ Dynamic Route dễ dàng ([id].vue).',
      'Code gọn gàng, không cần file config dài.',
      'Tránh lỗi sai đường dẫn do con người.'
    ]
  },
  'manual-route': {
    type: 'vue',
    title: 'Manual Routing',
    summary: 'Trong Vue thuần, bạn nắm quyền kiểm soát 100% nhưng phải tự tay khai báo từng đường dẫn một trong file config.',
    details: [
      'Phải tạo file router/index.js.',
      'Import thủ công từng component.',
      'Tốn thời gian setup ban đầu.',
      'Dễ lỗi nếu quên import component.'
    ]
  }
}

const selectedInfo = ref(null)

const showDetail = (key) => { selectedInfo.value = dataMap[key] }
const closeModal = () => { selectedInfo.value = null }
</script>

<style scoped>
/* --- GIỮ LẠI STYLE CŨ CỦA TRANG --- */
.glass-card { background: rgba(0, 0, 0, 0.6); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.15); border-radius: 32px; padding: 40px; max-width: 800px; width: 100%; }
.header { text-align: center; margin-bottom: 40px; }
.page-title { font-size: 2.5rem; margin: 0; color: white; }
.highlight { color: #00dc82; }
.page-desc { color: #e2e8f0; margin-top: 10px; font-size: 1.1rem; }
.comparison-container { display: flex; flex-direction: column; gap: 20px; }
.compare-item { background: rgba(255, 255, 255, 0.05); border-radius: 20px; padding: 20px; border: 1px solid rgba(255, 255, 255, 0.1); }
.criteria { font-size: 0.9rem; text-transform: uppercase; letter-spacing: 2px; color: #94a3b8; margin-bottom: 15px; font-weight: 800; text-align: center;}
.vs-row { display: flex; align-items: center; gap: 15px; }
.box { flex: 1; padding: 20px; border-radius: 16px; background: rgba(0, 0, 0, 0.3); text-align: center; transition: all 0.3s; border: 1px solid transparent; cursor: pointer; position: relative; overflow: hidden; }
.box:hover { background: rgba(255, 255, 255, 0.1); border-color: #00dc82; transform: translateY(-5px); }
.box strong { display: block; font-size: 1.2rem; color: #ffffff; margin-bottom: 5px; }
.box p { margin: 0; font-size: 0.95rem; color: #e2e8f0; }
.tag { font-size: 0.7rem; padding: 2px 8px; border-radius: 4px; margin-bottom: 8px; display: inline-block; font-weight: bold; }
.box.nuxt .tag { background: rgba(0, 220, 130, 0.2); color: #00dc82; }
.box.vue .tag { background: rgba(66, 184, 131, 0.2); color: #42b883; }
.divider { font-weight: 900; font-style: italic; color: #64748b; }
.footer-nav { margin-top: 30px; text-align: center; }
.btn-back { color: #e2e8f0; text-decoration: none; display: inline-flex; align-items: center; gap: 8px; font-weight: 600; transition: 0.3s; }
.btn-back:hover { color: #00dc82; transform: translateX(-5px); }

/* --- STYLE MODAL ĐÃ FIX LỖI --- */
.modal-overlay {
  position: fixed; 
  top: 0; left: 0; 
  width: 100vw; height: 100vh; /* Phủ toàn màn hình */
  background: rgba(0, 0, 0, 0.7); /* Nền tối mờ phía sau */
  backdrop-filter: blur(10px); /* Hiệu ứng kính mờ cho background */
  display: flex; justify-content: center; align-items: center;
  z-index: 9999; /* Luôn nằm trên cùng */
  padding: 20px;
}

.modal-card {
  background: linear-gradient(145deg, #1e293b, #0f172a);
  width: 100%; max-width: 550px;
  border-radius: 24px;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
  overflow: hidden;
  border: 1px solid rgba(255,255,255,0.1);
  position: relative;
}

/* Màu sắc chủ đạo theo loại */
.modal-card.nuxt { border-top: 4px solid #00dc82; box-shadow: 0 10px 40px -10px rgba(0, 220, 130, 0.3); }
.modal-card.vue { border-top: 4px solid #42b883; box-shadow: 0 10px 40px -10px rgba(66, 184, 131, 0.3); }

.modal-header {
  padding: 30px 30px 20px;
  display: flex; align-items: center; gap: 15px;
  border-bottom: 1px solid rgba(255,255,255,0.05);
  background: rgba(255,255,255,0.02);
}

.icon-circle {
  width: 50px; height: 50px;
  border-radius: 50%;
  background: rgba(255,255,255,0.05);
  display: flex; align-items: center; justify-content: center;
  font-size: 1.5rem;
}

.header-text h2 { margin: 0; font-size: 1.5rem; color: white; }
.badge { font-size: 0.75rem; text-transform: uppercase; letter-spacing: 1px; font-weight: 700; opacity: 0.7; }
.nuxt .badge { color: #00dc82; }
.vue .badge { color: #42b883; }

.close-btn {
  margin-left: auto; background: rgba(255,255,255,0.05); border: none;
  width: 36px; height: 36px; border-radius: 50%;
  color: #94a3b8; cursor: pointer; display: flex; align-items: center; justify-content: center;
  transition: 0.2s;
}
.close-btn:hover { background: rgba(239, 68, 68, 0.2); color: #ef4444; }

.modal-body { padding: 30px; }
.summary { font-size: 1.05rem; line-height: 1.6; color: #cbd5e1; margin-bottom: 25px; }

.detail-grid { display: flex; flex-direction: column; gap: 12px; }

/* Item chi tiết dạng thẻ */
.detail-item {
  background: rgba(255,255,255,0.03);
  padding: 15px; border-radius: 12px;
  display: flex; gap: 15px; align-items: center;
  border: 1px solid rgba(255,255,255,0.05);
  transition: 0.2s;
}
.detail-item:hover { background: rgba(255,255,255,0.06); transform: translateX(5px); }

.check-icon {
  width: 24px; height: 24px; border-radius: 50%;
  background: rgba(255,255,255,0.1); color: white;
  display: flex; align-items: center; justify-content: center;
  font-size: 0.8rem; flex-shrink: 0;
}
.nuxt .check-icon { background: #00dc82; color: #002e1f; }
.vue .check-icon { background: #42b883; color: #002e1f; }

.detail-item span { color: #e2e8f0; font-size: 0.95rem; }

.modal-footer {
  padding: 20px 30px;
  text-align: right;
  background: rgba(0,0,0,0.2);
}

.btn-got-it {
  padding: 10px 24px; border-radius: 8px; border: none;
  font-weight: 600; cursor: pointer; color: white;
  transition: 0.3s;
}
.nuxt .btn-got-it { background: #00dc82; color: #0f172a; }
.nuxt .btn-got-it:hover { background: #00ff95; box-shadow: 0 0 15px rgba(0,220,130,0.4); }

.vue .btn-got-it { background: #42b883; color: #0f172a; }
.vue .btn-got-it:hover { background: #5cefa0; box-shadow: 0 0 15px rgba(66,184,131,0.4); }

/* Animation Pop */
.modal-pop-enter-active, .modal-pop-leave-active { transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
.modal-pop-enter-from, .modal-pop-leave-to { opacity: 0; transform: scale(0.8) translateY(20px); }
</style>