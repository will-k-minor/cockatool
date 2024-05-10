<script lang=ts >
    import type { RecipeType } from '../CocktailTypes.js';

    export let recipe: RecipeType;
</script>

<div class="card">
    <h2 class="recipe-name"> {recipe.name.toUpperCase()} </h2>
    <ul>
    {#each recipe.ingredients as ingredient, i}
        <li>{ingredient}</li>
    {/each}
    </ul>
    <h3>Instructions</h3>
    <p>{recipe.instructions}</p>
</div>

<style>
    .card {
        border: 1px solid #ccc;
        border-radius: 8px;
        padding: 1em;
        margin: 1em;
        background-color: #f9f9f9;
        box-shadow: #ccc 2px 2px 5px;
    }

    .recipe-name {
        margin: 0;
        font-weight: bold;
        font-size: x-large;
    }
</style>
