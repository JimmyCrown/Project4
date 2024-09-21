<script setup>
    const props = defineProps({
        totalCost: Number,
        totalCalories: Number
    });
</script>

<template>
  <section class="totals">
    <h3>Total Cost: ${{ totalCost.toFixed(2) }}</h3>
    <h3>Total Calories: {{ totalCalories }}</h3>
  </section>
</template>