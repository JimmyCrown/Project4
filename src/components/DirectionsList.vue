<script setup>

  const emit = defineEmits(['removeDirection']);

  const props = defineProps({
    directions: Array
  });

  const removeDirection = (index) => {
    emit('removeDirection', index);
  };
</script>

<template>
  <section class="direction-list">
    <h3>Directions</h3>
    <div v-for="(item, index) in directions" :key="index" class="direction-item">
      <div class="direction-content">
        <strong>Step {{ index + 1 }}:</strong> {{ item.direction }}
      </div>
      <button class="remove-button" @click="removeDirection(index)">Remove</button>
    </div>
  </section>
</template>