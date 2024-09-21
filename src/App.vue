<script setup>
  import { ref, computed, onMounted, watch } from 'vue';
  import RecipeForm from './components/RecipeForm.vue';
  import IngredientsList from './components/IngredientsList.vue';
  import DirectionsList from './components/DirectionsList.vue';
  import RecipeTotals from './components/RecipeTotals.vue';

  const recipeName = ref('');
  const ingredients = ref([]);
  const directions = ref([]);

  const addIngredient = (ingredient, cost, calories) => {
    ingredients.value.push({
      ingredient,
      cost: parseFloat(cost),
      calories: parseFloat(calories),
    });
  };

  const addDirection = (direction) => {
    directions.value.push({ direction });
  };

  const removeIngredient = (index) => {
    ingredients.value.splice(index, 1);
  };

  const removeDirection = (index) => {
    directions.value.splice(index, 1);
  };

  const totalCost = computed(() => {
    return ingredients.value.reduce((acc, item) => acc + item.cost, 0);
  });

  const totalCalories = computed(() => {
    return ingredients.value.reduce((acc, item) => acc + item.calories, 0);
  });

  onMounted(() => {
    recipeName.value = localStorage.getItem('recipeName') || '';
    ingredients.value = JSON.parse(localStorage.getItem('ingredients')) || [];
    directions.value = JSON.parse(localStorage.getItem('directions')) || [];
  });

  watch(recipeName, (newVal) => {
    localStorage.setItem('recipeName', newVal);
  });

  watch(ingredients, (newVal) => {
    localStorage.setItem('ingredients', JSON.stringify(newVal));
  }, { deep: true });

  watch(directions, (newVal) => {
    localStorage.setItem('directions', JSON.stringify(newVal));
  }, { deep: true });
</script>

<template>
  <main class="app">
    <section>
      <h2>Welcome to Recipe Builder</h2>
    </section>

    <RecipeForm :recipeName="recipeName" @update:recipeName="recipeName = $event" @addIngredient="addIngredient" @addDirection="addDirection"/>

    <IngredientsList :ingredients="ingredients" @removeIngredient="removeIngredient"/>
    <DirectionsList :directions="directions" @removeDirection="removeDirection"/>
  
  </main>
</template>