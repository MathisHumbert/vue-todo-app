<script setup>
import { defineProps, defineEmits } from 'vue';

const emit = defineEmits(['deleteTodo', 'toggleCompletion']);

const { item } = defineProps(['item']);
</script>

<template>
  <article class="item">
    <div class="item__container">
      <svg
        @click="emit('toggleCompletion', item.id)"
        class="item__icon"
        xmlns="http://www.w3.org/2000/svg"
        width="100%"
        height="100%"
        viewBox="0 0 24 24"
        fill="none"
      >
        <circle
          class="item__icon__classic__circle"
          :style="{ opacity: item.completed ? 0 : 1 }"
          cx="12"
          cy="12"
          r="11.5"
          stroke="#393A4B"
        />
        <circle
          class="item__icon__color__circle"
          :style="{ opacity: item.completed ? 0 : 1 }"
          cx="12"
          cy="12"
          r="11.5"
          stroke="url(#paint0_linear_0_155)"
        />
        <g :style="{ opacity: item.completed ? 1 : 0 }">
          <circle cx="12" cy="12" r="12" fill="url(#paint1_linear_0_155)" />
          <path d="M8 12.3041L10.6959 15L16.6959 9" stroke="white" />
        </g>
        <defs>
          <linearGradient
            id="paint0_linear_0_155"
            x1="-12"
            y1="12"
            x2="12"
            y2="36"
            gradientUnits="userSpaceOnUse"
          >
            <stop stop-color="#55DDFF" />
            <stop offset="1" stop-color="#C058F3" />
          </linearGradient>
          <linearGradient
            id="paint1_linear_0_155"
            x1="-12"
            y1="12"
            x2="12"
            y2="36"
            gradientUnits="userSpaceOnUse"
          >
            <stop stop-color="#55DDFF" />
            <stop offset="1" stop-color="#C058F3" />
          </linearGradient>
        </defs>
      </svg>
      <p
        @click="emit('toggleCompletion', item.id)"
        class="item__text"
        :class="{ active: item.completed }"
      >
        {{ item.text }}
      </p>
    </div>
    <svg
      @click="emit('deleteTodo', item.id)"
      class="item__close"
      xmlns="http://www.w3.org/2000/svg"
      width="100%"
      height="100%"
      viewBox="0 0 18 18"
      fill="none"
    >
      <path
        fill-rule="evenodd"
        clip-rule="evenodd"
        d="M17.6777 0.707107L16.9706 0L8.83883 8.13173L0.707107 0L0 0.707107L8.13173 8.83883L0 16.9706L0.707106 17.6777L8.83883 9.54594L16.9706 17.6777L17.6777 16.9706L9.54594 8.83883L17.6777 0.707107Z"
        fill="#5B5E7E"
      />
    </svg>
  </article>
</template>

<style scoped>
.item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px 24px;
  border-bottom: 1px solid var(--text-border-color);
}

.item__container {
  display: flex;
  align-items: center;
  gap: 24px;
}

.item__icon {
  width: 24px;
  height: 24px;
  cursor: pointer;
}

.item__icon__classic__circle {
  opacity: 1 !important;
  stroke: var(--text-border-color);
}

.item__icon__color__circle {
  opacity: 0 !important;
}

.item__icon:hover .item__icon__classic__circle {
  opacity: 0 !important;
}

.item__icon:hover .item__icon__color__circle {
  opacity: 1 !important;
}

.item__text {
  font-size: 18px;
  line-height: normal;
  letter-spacing: -0.25px;
  cursor: pointer;
}

.item__text.active {
  color: var(--text-active-color);
  text-decoration: line-through;
}

.item__close {
  width: 18px;
  height: 18px;
  cursor: pointer;
  opacity: 0;
}

.item:hover .item__close {
  opacity: 1;
}

@media (max-width: 768px) {
  .item {
    padding: 16px 20px;
  }
  .item__icon {
    width: 20px;
    height: 20px;
  }

  .item__container {
    gap: 12px;
  }

  .item__text {
    font-size: 12px;
    letter-spacing: -0.167px;
  }
}
</style>
