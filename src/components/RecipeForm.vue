<script setup>
    import { ref } from 'vue';

    
    const props = defineProps({
    recipeName: String,
    });

    const emit = defineEmits(['update:recipeName', 'addIngredient', 'addDirection']);

    const newIngredient = ref('');
    const newCost = ref(0);
    const newCalories = ref(0);
    const newDirection = ref('');

    const updateRecipeName = (event) => {
        emit('update:recipeName', event.target.value);
    };

    const addIngredient = () => {
        if (newIngredient.value.trim()) {
            emit('addIngredient', newIngredient.value, newCost.value, newCalories.value);
            newIngredient.value = '';
            newCost.value = 0;
            newCalories.value = 0;
        }
    };

    const addDirection = () => {
        if (newDirection.value.trim()) {
            emit('addDirection', newDirection.value);
            newDirection.value = '';
        }
    };
</script>

<template>
  <section class="create-recipe">
    <h3>Create a Recipe</h3>

    <h4>What's the name of your recipe?</h4>
    <input type="text" :value="recipeName" @input="updateRecipeName" placeholder="e.g., Pizza"/>

    <h4>Add Ingredient</h4>
    <input type="text" v-model="newIngredient" placeholder="e.g., Tomatoes" />
    <h4>Price of Ingredient</h4>
    <input type="number" v-model="newCost" placeholder="Cost" />
    <h4>How many Calories?</h4>
    <input type="number" v-model="newCalories" placeholder="Calories?" />
    <button @click="addIngredient">Add Ingredient</button>

    <h4>Add Direction</h4>
    <input type="text" v-model="newDirection" placeholder="e.g., Blend the tomatoes" />
    <button @click="addDirection">Add Direction</button>
  </section>
</template>