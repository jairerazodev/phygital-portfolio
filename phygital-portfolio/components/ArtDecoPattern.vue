<template>
    <svg class="art-deco-pattern" xmlns="http://www.w3.org/2000/svg">
      <defs>
        <pattern :id="patternId" x="0" y="0" width="40" height="40" patternUnits="userSpaceOnUse">
          <path :d="patterns[patternId]" fill="none" :stroke="color" stroke-width="0.5" stroke-opacity="0.3"/>
        </pattern>
      </defs>
      <rect width="100%" height="100%" :fill="'url(#' + patternId + ')'"/>
    </svg>
  </template>
  
  <script setup>
  const patterns = {
    pattern1: "M0 0L20 20L40 0M20 0L40 20M0 20L20 40",
    pattern2: "M0 40L40 0M0 20L20 0M20 40L40 20",
    pattern3: "M20 0L0 20L20 40L40 20L20 0Z",
    pattern4: "M0 0L40 40M40 0L0 40M20 0V40M0 20H40"
  };
  
  const props = defineProps({
    patternId: String,
    color: String
  });
  </script>
  
  <style scoped>
  .art-deco-pattern {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
  }
  </style>
  