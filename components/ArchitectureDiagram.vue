<template>
  <div class="architecture-diagram">
    <h2 class="diagram-title">🏗️ Architecture Overview</h2>
    <p class="diagram-subtitle">Clean Architecture Flow</p>

    <div class="diagram-container">
      <div class="layer-flow">
        <div
          v-for="(layer, index) in layers"
          :key="index"
          class="layer-wrapper"
        >
          <div :class="['layer', layer.className]">
            <div class="layer-icon">{{ layer.icon }}</div>
            <div class="layer-content">
              <div class="layer-title">{{ layer.title }}</div>
              <div class="layer-subtitle">{{ layer.subtitle }}</div>
              <div class="layer-path">{{ layer.path }}</div>
            </div>
          </div>

          <div v-if="index < layers.length - 1" class="arrow-connector">
            <div class="arrow-label">{{ layer.arrow }}</div>
            <svg width="50" height="24" viewBox="0 0 50 24" class="arrow-svg">
              <path d="M 0 12 L 40 12 M 35 8 L 40 12 L 35 16"
                    stroke="currentColor"
                    stroke-width="2"
                    fill="none"
                    stroke-linecap="round"
                    stroke-linejoin="round"/>
            </svg>
          </div>
        </div>
      </div>
    </div>

    <div class="legend">
      <div class="legend-item">
        <span class="legend-dot ui-layer"></span>
        <span class="legend-text">UI Layer</span>
      </div>
      <div class="legend-item">
        <span class="legend-dot core-layer"></span>
        <span class="legend-text">Core (Business Logic)</span>
      </div>
      <div class="legend-item">
        <span class="legend-dot infra-layer"></span>
        <span class="legend-text">Infrastructure</span>
      </div>
    </div>
  </div>
</template>

<script setup>
const layers = [
  {
    icon: '🎨',
    title: 'React Components',
    subtitle: 'UI Layer',
    path: 'component-library/pages',
    className: 'ui-layer',
    arrow: 'fetch()'
  },
  {
    icon: '🔌',
    title: 'API Routes',
    subtitle: 'HTTP Layer',
    path: 'app/api/feature/*',
    className: 'ui-layer',
    arrow: 'execute()'
  },
  {
    icon: '⚙️',
    title: 'Controller',
    subtitle: 'Infrastructure',
    path: 'Maps HTTP → UseCase',
    className: 'infra-layer',
    arrow: 'execute()'
  },
  {
    icon: '💼',
    title: 'UseCase',
    subtitle: 'Business Logic',
    path: 'Validate → Process',
    className: 'core-layer',
    arrow: 'call()'
  },
  {
    icon: '🚪',
    title: 'Gateway',
    subtitle: 'Infrastructure',
    path: 'Delegates to Endpoints',
    className: 'infra-layer',
    arrow: 'fetch()'
  },
  {
    icon: '📡',
    title: 'Endpoint',
    subtitle: 'HTTP Client',
    path: 'Calls Rucio Server',
    className: 'infra-layer',
    arrow: ''
  }
];
</script>

<style scoped>
.architecture-diagram {
  padding: 0;
  min-height: 520px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  animation: fadeIn 0.6s ease-out;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

.diagram-title {
  text-align: center;
  font-size: 2rem;
  font-weight: 700;
  color: #111827;
  margin-bottom: 0.5rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95) 0%, rgba(249, 250, 251, 0.95) 100%);
  padding: 0.5rem 1.5rem;
  border-radius: 0.75rem;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12);
  border: 2px solid #6366f1;
  display: inline-block;
}

.diagram-subtitle {
  text-align: center;
  font-size: 0.9rem;
  color: #111827;
  margin-bottom: 1rem;
  font-weight: 700;
  background: rgba(255, 255, 255, 0.9);
  padding: 0.35rem 0.75rem;
  border-radius: 0.375rem;
  display: inline-block;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
}

.diagram-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex: 1;
  overflow-x: auto;
  padding: 1rem 0;
}

.layer-flow {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem;
}

.layer-wrapper {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  animation: slideIn 0.6s ease-out backwards;
}

.layer-wrapper:nth-child(1) { animation-delay: 0.1s; }
.layer-wrapper:nth-child(2) { animation-delay: 0.2s; }
.layer-wrapper:nth-child(3) { animation-delay: 0.3s; }
.layer-wrapper:nth-child(4) { animation-delay: 0.4s; }
.layer-wrapper:nth-child(5) { animation-delay: 0.5s; }
.layer-wrapper:nth-child(6) { animation-delay: 0.6s; }

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.layer {
  min-width: 160px;
  min-height: 160px;
  padding: 1rem;
  border-radius: 0.75rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  box-shadow: 0 6px 12px -2px rgb(0 0 0 / 0.1), 0 3px 5px -3px rgb(0 0 0 / 0.1);
  border: 2px solid transparent;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.layer::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg, rgba(255,255,255,0.8) 0%, rgba(255,255,255,0.4) 100%);
}

.layer:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
}

.ui-layer {
  background: linear-gradient(135deg, #e0f2fe 0%, #bae6fd 100%);
  border-color: #38bdf8;
}

.core-layer {
  background: linear-gradient(135deg, #dcfce7 0%, #bbf7d0 100%);
  border-color: #22c55e;
}

.infra-layer {
  background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);
  border-color: #f59e0b;
}

.layer-icon {
  font-size: 2rem;
  filter: drop-shadow(0 2px 4px rgba(0,0,0,0.1));
}

.layer-content {
  text-align: center;
}

.layer-title {
  font-weight: 700;
  font-size: 0.9rem;
  color: #1f2937;
  margin-bottom: 0.2rem;
}

.layer-subtitle {
  font-size: 0.75rem;
  color: #6b7280;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-bottom: 0.5rem;
}

.layer-path {
  font-size: 0.7rem;
  color: #4b5563;
  font-family: 'JetBrains Mono', monospace;
  background: rgba(255, 255, 255, 0.7);
  padding: 0.25rem 0.5rem;
  border-radius: 0.375rem;
  font-weight: 600;
}

.arrow-connector {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.25rem;
  margin: 0 0.5rem;
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

.arrow-svg {
  color: #1f2937;
}

.legend {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-top: 2rem;
  padding: 1rem;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 0.75rem;
  backdrop-filter: blur(10px);
  box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1);
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.legend-dot {
  width: 20px;
  height: 20px;
  border-radius: 0.375rem;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.legend-text {
  font-size: 0.875rem;
  color: #374151;
  font-weight: 500;
}
</style>
