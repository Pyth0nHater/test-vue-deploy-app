<script setup lang="ts">
import { ref, onMounted } from 'vue'

const steps = [
  { icon: '📦', label: 'Репозиторий склонирован' },
  { icon: '🐳', label: 'Dockerfile сгенерирован' },
  { icon: '🔨', label: 'Docker-образ собран' },
  { icon: '🚀', label: 'Контейнер запущен' },
  { icon: '🌐', label: 'Traefik маршрут активен' },
]

const info = [
  { label: 'Фреймворк', value: 'Vue 3' },
  { label: 'Сборщик', value: 'Vite 8' },
  { label: 'Сервер', value: 'Nginx alpine' },
  { label: 'Роутер', value: 'Traefik v3' },
  { label: 'Статус', value: '200 OK' },
]

const done = ref(0)
onMounted(() => {
  const t = setInterval(() => {
    done.value++
    if (done.value >= steps.length) clearInterval(t)
  }, 450)
})
</script>

<template>
  <div class="page">
    <div class="blob b1" />
    <div class="blob b2" />

    <div class="card">
      <div class="tags">
        <span class="tag green">Vue 3</span>
        <span class="tag blue">Vite 8</span>
        <span class="tag yellow">deploy-service</span>
      </div>

      <div class="fw-label">VUE</div>
      <h1>Тестовый<br /><em>деплой</em></h1>
      <p>
        Тестовая страница для проверки работы deploy-service.<br />
        Приложение собрано в Docker-образ и доступно через Traefik.
      </p>

      <div class="steps">
        <div
          v-for="(s, i) in steps"
          :key="i"
          class="step"
          :class="{ done: i < done }"
        >
          <span>{{ i < done ? '✅' : s.icon }}</span>
          <span>{{ s.label }}</span>
        </div>
      </div>
    </div>

    <div class="grid">
      <div v-for="item in info" :key="item.label" class="info-cell">
        <span class="ilabel">{{ item.label }}</span>
        <span class="ivalue">{{ item.value }}</span>
      </div>
    </div>

    <footer>vue + vite + nginx + traefik — всё работает 🎉</footer>
  </div>
</template>

<style scoped>
.page {
  min-height: 100vh;
  background: #0d1117;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem 1rem;
  font-family: system-ui, sans-serif;
  gap: 1.25rem;
  position: relative;
  overflow: hidden;
}

.blob {
  position: fixed;
  border-radius: 50%;
  filter: blur(90px);
  opacity: 0.15;
  pointer-events: none;
}
.b1 { width: 450px; height: 450px; background: #41b883; top: -120px; left: -120px; }
.b2 { width: 300px; height: 300px; background: #34d399; bottom: -80px; right: -80px; }

.fw-label {
  font-size: 6rem;
  font-weight: 900;
  color: #41b883;
  text-shadow: 0 0 60px rgba(65,184,131,.45);
  letter-spacing: -0.02em;
  line-height: 1;
  margin-bottom: .5rem;
  font-family: monospace;
}

.card {
  max-width: 540px;
  width: 100%;
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(65,184,131,0.2);
  border-radius: 20px;
  padding: 2.25rem;
  backdrop-filter: blur(16px);
  position: relative;
  z-index: 1;
}

.tags { display: flex; gap: .5rem; flex-wrap: wrap; margin-bottom: 1.5rem; }
.tag {
  font-size: .7rem;
  font-weight: 700;
  padding: 3px 10px;
  border-radius: 20px;
  text-transform: uppercase;
  letter-spacing: .05em;
}
.green { background: rgba(65,184,131,.12); color: #41b883; border: 1px solid rgba(65,184,131,.35); }
.blue  { background: rgba(100,108,255,.12); color: #818cf8; border: 1px solid rgba(100,108,255,.35); }
.yellow{ background: rgba(251,191,36,.1);  color: #fbbf24; border: 1px solid rgba(251,191,36,.3);  }

h1 {
  font-size: 2.8rem;
  font-weight: 800;
  color: #f0fdf4;
  margin: 0 0 .9rem;
  line-height: 1.1;
}
h1 em { color: #41b883; font-style: normal; }

p {
  color: #64748b;
  font-size: .9rem;
  line-height: 1.7;
  margin-bottom: 1.75rem;
}

.steps { display: flex; flex-direction: column; gap: .5rem; }
.step {
  display: flex;
  align-items: center;
  gap: .75rem;
  padding: .6rem .9rem;
  border-radius: 10px;
  background: rgba(255,255,255,.02);
  border: 1px solid rgba(255,255,255,.06);
  font-size: .88rem;
  color: #334155;
  transition: all .25s;
}
.step.done {
  background: rgba(65,184,131,.07);
  border-color: rgba(65,184,131,.2);
  color: #a7f3d0;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: .65rem;
  max-width: 540px;
  width: 100%;
  z-index: 1;
}
.info-cell {
  background: rgba(255,255,255,.03);
  border: 1px solid rgba(255,255,255,.07);
  border-radius: 12px;
  padding: .85rem 1rem;
  display: flex;
  flex-direction: column;
  gap: .3rem;
}
.ilabel { font-size: .68rem; color: #334155; text-transform: uppercase; letter-spacing: .06em; }
.ivalue { font-size: .92rem; color: #e2e8f0; font-weight: 600; }

footer { color: #1e293b; font-size: .8rem; z-index: 1; }
</style>
