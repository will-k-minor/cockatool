<script lang=ts >
    import type { RecipeType } from './CocktailTypes.ts';

    export let recipe: RecipeType;
    export let key: string;
</script>

<div class="card" key={key}>
    <h2> {recipe.name} </h2>
    <p>{recipe.ingredients}</p>
    <h3> Instructions </h3>
    <p>{recipe.instructions}</p>
</div>

<style>
    .card {
        border: 1px solid #ccc;
        border-radius: 4px;
        padding: 1em;
        margin: 1em;
        background-color: #f9f9f9;
        box-shadow: #ccc 2px 2px 5px;
    }
</style>
