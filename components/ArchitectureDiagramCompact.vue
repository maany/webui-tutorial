<template>
  <div class="architecture-diagram-compact">
    <h2 class="diagram-title">🏗️ Architecture Overview</h2>

    <div class="main-container">
      <!-- Left Side: Vertical Flow -->
      <div class="flow-section">
        <div
          v-for="(layer, index) in layers"
          :key="index"
          class="flow-item"
          :style="{ animationDelay: `${index * 0.1}s` }"
        >
          <div :class="['layer-card', layer.className]">
            <div class="card-icon">{{ layer.icon }}</div>
            <div class="card-content">
              <div class="card-title">{{ layer.title }}</div>
              <div class="card-subtitle">{{ layer.subtitle }}</div>
            </div>
          </div>

          <div v-if="index < layers.length - 1" class="vertical-arrow">
            <svg width="24" height="40" viewBox="0 0 24 40" class="arrow-svg">
              <path d="M 12 0 L 12 35 M 8 30 L 12 35 L 16 30"
                    stroke="currentColor"
                    stroke-width="2.5"
                    fill="none"
                    stroke-linecap="round"
                    stroke-linejoin="round"/>
            </svg>
            <div class="arrow-label">{{ layer.arrow }}</div>
          </div>
        </div>
      </div>

      <!-- Right Side: Principles -->
      <div class="principles-section">
        <h3 class="principles-title">Key Principles</h3>
        <div
          v-for="(principle, index) in principles"
          :key="index"
          class="principle-card"
          :style="{ animationDelay: `${0.6 + index * 0.1}s` }"
        >
          <div class="principle-number">{{ index + 1 }}</div>
          <div class="principle-content">
            <div class="principle-title">{{ principle.title }}</div>
            <div class="principle-description">{{ principle.description }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const layers = [
  { icon: '🎨', title: 'React Components', subtitle: 'UI Layer', className: 'ui-layer', arrow: 'fetch()' },
  { icon: '🔌', title: 'API Routes', subtitle: 'HTTP Layer', className: 'ui-layer', arrow: 'execute()' },
  { icon: '⚙️', title: 'Controller', subtitle: 'Infrastructure', className: 'infra-layer', arrow: 'execute()' },
  { icon: '💼', title: 'UseCase', subtitle: 'Business Logic', className: 'core-layer', arrow: 'call()' },
  { icon: '🚪', title: 'Gateway', subtitle: 'Infrastructure', className: 'infra-layer', arrow: 'fetch()' },
  { icon: '📡', title: 'Endpoint', subtitle: 'HTTP Client', className: 'infra-layer', arrow: '' }
];

const principles = [
  { title: 'Dependency Inversion', description: 'Core defines interfaces' },
  { title: 'Separation of Concerns', description: 'Single responsibility' },
  { title: 'Testability', description: 'Mock gateways' },
  { title: 'Streaming Support', description: 'NDJSON for large data' }
];
</script>

<style scoped>
.architecture-diagram-compact {
  padding: 0.25rem;
  min-height: 550px;
  height: 100%;
  display: flex;
  flex-direction: column;
  animation: fadeIn 0.6s ease-out;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

.diagram-title {
  text-align: center;
  font-size: 2rem;
  font-weight: 700;
  color: #111827;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95) 0%, rgba(249, 250, 251, 0.95) 100%);
  padding: 0.5rem 1.5rem;
  border-radius: 0.75rem;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12);
  border: 2px solid #6366f1;
  display: inline-block;
}

.main-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  flex: 1;
  align-items: center;
}

.flow-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.flow-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  animation: slideInLeft 0.6s ease-out backwards;
}

@keyframes slideInLeft {
  from {
    opacity: 0;
    transform: translateX(-30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.layer-card {
  min-width: 240px;
  min-height: 65px;
  padding: 0.85rem 1.25rem;
  border-radius: 0.65rem;
  display: flex;
  align-items: center;
  gap: 0.85rem;
  box-shadow: 0 3px 5px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.layer-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg, rgba(255,255,255,0.8) 0%, rgba(255,255,255,0.4) 100%);
}

.layer-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
}

.ui-layer {
  background: linear-gradient(135deg, #e0f2fe 0%, #bae6fd 100%);
}

.core-layer {
  background: linear-gradient(135deg, #dcfce7 0%, #bbf7d0 100%);
}

.infra-layer {
  background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);
}

.card-icon {
  font-size: 1.85rem;
  filter: drop-shadow(0 2px 4px rgba(0,0,0,0.1));
}

.card-content {
  flex: 1;
}

.card-title {
  font-weight: 700;
  font-size: 0.95rem;
  color: #1f2937;
  margin-bottom: 0.1rem;
}

.card-subtitle {
  font-size: 0.75rem;
  color: #4b5563;
  font-weight: 700;
}

.vertical-arrow {
  display: flex;
  align-items: center;
  gap: 0.35rem;
  margin: 0.3rem 0;
}

.arrow-svg {
  color: #1f2937;
}

.arrow-label {
  font-size: 0.7rem;
  color: #1f2937;
  font-family: 'JetBrains Mono', monospace;
  font-weight: 700;
  background: white;
  padding: 0.25rem 0.5rem;
  border-radius: 0.375rem;
  box-shadow: 0 1px 2px 0 rgb(0 0 0 / 0.05);
}

.principles-section {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  padding: 2rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.8) 0%, rgba(249, 250, 251, 0.8) 100%);
  border-radius: 1rem;
  backdrop-filter: blur(10px);
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1);
}

.principles-title {
  font-size: 1.5rem;
  font-weight: 700;
  color: #1f2937;
  margin-bottom: 0.5rem;
  text-align: center;
}

.principle-card {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1rem;
  background: white;
  border-radius: 0.75rem;
  box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1);
  transition: all 0.3s ease;
  animation: slideInRight 0.6s ease-out backwards;
}

@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.principle-card:hover {
  transform: translateX(4px);
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1);
}

.principle-number {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 1rem;
  flex-shrink: 0;
  box-shadow: 0 2px 4px rgba(102, 126, 234, 0.3);
}

.principle-content {
  flex: 1;
}

.principle-title {
  font-weight: 700;
  font-size: 0.95rem;
  color: #1f2937;
  margin-bottom: 0.25rem;
}

.principle-description {
  font-size: 0.8rem;
  color: #374151;
  line-height: 1.4;
  font-weight: 500;
}
</style>
