<template>
  <div class="code-block-wrapper">
    <div class="code-header" :class="{ 'no-title': !title }">
      <div v-if="title" class="code-title">
        <span class="file-icon">📄</span>
        <span class="file-name">{{ title }}</span>
      </div>
      <div class="code-actions">
        <div v-if="language && !title" class="code-language">{{ language }}</div>
        <button
          @click="copyCode"
          class="copy-button"
          :class="{ 'copied': isCopied }"
        >
          <span v-if="!isCopied">📋 Copy</span>
          <span v-else>✓ Copied!</span>
        </button>
      </div>
    </div>
    <div class="code-content" :class="{ 'has-header': title }" ref="codeContentRef">
      <slot />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

defineProps({
  title: {
    type: String,
    default: ''
  },
  language: {
    type: String,
    default: ''
  }
});

const codeContentRef = ref(null);
const isCopied = ref(false);

const copyCode = async () => {
  if (!codeContentRef.value) return;

  // Extract text from the code element
  const codeElement = codeContentRef.value.querySelector('code');
  if (!codeElement) return;

  const codeText = codeElement.innerText || codeElement.textContent;

  try {
    await navigator.clipboard.writeText(codeText);
    isCopied.value = true;
    setTimeout(() => {
      isCopied.value = false;
    }, 2000);
  } catch (err) {
    console.error('Failed to copy code:', err);
  }
};
</script>

<style scoped>
.code-block-wrapper {
  margin: 0.75rem 0;
  border-radius: 0.5rem;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  background: #1f2937;
  border: 1px solid #374151;
}

.code-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.5rem 1rem;
  background: #111827;
  border-bottom: 1px solid #374151;
}

.code-header.no-title {
  justify-content: flex-end;
}

.code-title {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #e5e7eb;
  font-size: 0.875rem;
  font-weight: 600;
  font-family: 'JetBrains Mono', monospace;
}

.file-icon {
  font-size: 1rem;
}

.file-name {
  color: #60a5fa;
}

.code-actions {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.code-language {
  font-size: 0.75rem;
  color: #9ca3af;
  font-family: 'JetBrains Mono', monospace;
  text-transform: uppercase;
  background: #374151;
  padding: 0.25rem 0.5rem;
  border-radius: 0.25rem;
  font-weight: 600;
}

.copy-button {
  display: flex;
  align-items: center;
  gap: 0.25rem;
  font-size: 0.75rem;
  font-weight: 600;
  font-family: 'Inter', sans-serif;
  color: #9ca3af;
  background: #374151;
  border: 1px solid #4b5563;
  padding: 0.375rem 0.75rem;
  border-radius: 0.375rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.copy-button:hover {
  background: #4b5563;
  color: #e5e7eb;
  border-color: #6b7280;
}

.copy-button.copied {
  background: #10b981;
  color: white;
  border-color: #10b981;
}

.copy-button:active {
  transform: scale(0.95);
}

.code-content {
  max-height: min(35vh, 300px);
  overflow-y: auto;
  overflow-x: auto;
  background: #1f2937;
}

.code-content.has-header {
  max-height: min(30vh, 280px);
}

/* Scrollbar styling */
.code-content::-webkit-scrollbar {
  width: 10px;
  height: 10px;
}

.code-content::-webkit-scrollbar-track {
  background: #111827;
  border-radius: 4px;
}

.code-content::-webkit-scrollbar-thumb {
  background: #4b5563;
  border-radius: 4px;
}

.code-content::-webkit-scrollbar-thumb:hover {
  background: #6b7280;
}

.code-content::-webkit-scrollbar-corner {
  background: #111827;
}

/* Style for code inside */
.code-content :deep(pre) {
  margin: 0 !important;
  padding: 1rem !important;
  background: #1f2937 !important;
  border: none !important;
  border-radius: 0 !important;
  box-shadow: none !important;
}

.code-content :deep(pre::before) {
  display: none;
}

.code-content :deep(code) {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.85rem;
  line-height: 1.6;
}

/* Line numbers support */
.code-content :deep(.line-number) {
  color: #6b7280;
  margin-right: 1rem;
  user-select: none;
}

/* Syntax highlighting enhancement */
.code-content :deep(.shiki) {
  background: #1f2937 !important;
}
</style>
