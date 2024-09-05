<template>
  <div ref="scrollContainerRef" class="scroll-container">
    <div class="flex-container">
      <div
        v-for="(section, index) in sections"
        :key="index"
        :class="['card', { 'expanded': expandedStates[index] }]"
        @click="handleExpand(index)"
        :style="{ backgroundImage: `url(${section.image})` }"
      >
        <div class="content">
          <h1 class="title">{{ section.title }}</h1>
          <p class="text">{{ section.content }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue';

const sections = [
  { title: "THE ROARING TWENTIES", content: "A decade of economic growth...", image: "/assets/img/mona.png" },
  { title: "THE JAZZ AGE", content: "A period in the 1920s...", image: "/assets/img/monita.png" },
  { title: "ART DECO", content: "A style of visual arts...", image: "/assets/img/marmol.png" },
  { title: "THE LOST GENERATION", content: "The generation that came...", image: "/assets/img/nuda.png" }
];

const scrollContainerRef = ref(null);
const expandedStates = reactive(Array(sections.length).fill(false));

const handleExpand = (index) => {
  expandedStates[index] = !expandedStates[index];
};

onMounted(() => {
  const scrollContainer = scrollContainerRef.value;
  if (scrollContainer) {
    const handleWheel = (e) => {
      if (e.deltaY !== 0) {
        e.preventDefault();
        scrollContainer.scrollLeft += e.deltaY;
      }
    };
    scrollContainer.addEventListener('wheel', handleWheel, { passive: false });
    return () => scrollContainer.removeEventListener('wheel', handleWheel);
  }
});
</script>

<style scoped>
.scroll-container {
  height: 100vh;
  width: 100vw;
  overflow-x: scroll;
  overflow-y: hidden;
  white-space: nowrap;
  position: relative;
  background-color: #ffebcd; /* Background color for the container */
}

.flex-container {
  display: flex;
  height: 100%;
}

.card {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  width: 100vw;
  height: 100vh;
  background-size: cover;
  background-position: center;
  transition: all 0.3s ease-in-out;
  position: relative;
  cursor: pointer;
}

.card.expanded {
  width: 50vw; /* Expands to 50% of the viewport width */
}

.content {
  color: white;
  text-align: center;
  z-index: 1;
}

.title {
  font-size: 3rem;
  font-weight: bold;
}

.text {
  font-size: 1.5rem;
}

.card::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5); /* Dark overlay */
}
</style>
