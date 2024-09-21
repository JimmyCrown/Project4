<script setup>
const props = defineProps({
  ingredients: Array
});

const emit = defineEmits(['removeIngredient']);

const removeIngredient = (index) => {
  emit('removeIngredient', index);
};
</script>

<template>
  <section class="ingredient-list">
    <h3>Ingredients</h3>
    <div v-for="(item, index) in ingredients" :key="index" class="ingredient-item">
      <div class="ingredient-content">
        <strong>{{ item.ingredient }}</strong> - ${{ item.cost.toFixed(2) }} | {{ item.calories }} Calories
      </div>
      <button class="remove-button" @click="removeIngredient(index)">Remove</button>
    </div>
  </section>
</template>