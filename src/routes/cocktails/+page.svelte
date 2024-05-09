<script lang=ts>
    import IngredientCard from "./IngredientCard.svelte";
    import RecipeCard from "./RecipeCard.svelte";
    import type { RecipeType } from './CocktailTypes.ts';

    let ingredients: string[] = [];
    let recipes: RecipeType[] = [];

    function addIngredientField() {
        ingredients = [...ingredients, ''];
    }

    $: console.log(ingredients);

    function removeIngredient(index: number) {
        ingredients = ingredients.filter((_, i) => i !== index);
    }

    async function fetchCocktails() {
        try {
            const response = await fetch(
                `https://api.api-ninjas.com/v1/cocktail?ingredients=${ingredients.join(',')}`, 
                {
                    headers: { 'X-Api-Key': 'W+y19BJkxOROkRuXSumxeg==gTF60d4rnpVEv6mx' }
                }
            );
            if (!response.ok) {
                throw new Error('Network response was not ok');
            }
            recipes = await response.json();
            console.log(recipes);
        } catch (error) {
            console.error('Fetch error:', error);
            recipes = [];
        }
    }
</script>

<span class="button-options">
    <button on:click={addIngredientField}>Add ingredient</button>
    <button on:click={async () => await fetchCocktails()}>Fetch cocktails</button>    
</span>

<div class="grid-container">
    {#each ingredients as ingredient, i}
        <IngredientCard bind:ingredient={ingredient} {i} {removeIngredient} />
    {/each}
</div>

{#if recipes.length === 0}
    <p>No recipes found</p>
{:else}
    <p>Recipes found!</p>
{/if}

{#each recipes as recipe, i}
    <RecipeCard {recipe} key={`cocktail-recipe-${i}`}/>
{/each}

<style>
    .button-options {
        display: flex;
        justify-content: space-between;
        margin: 10px;
        max-width: 256px;
    }

    icon {
        width: 50px;
        height: 50px;
        background-color: #ffffff;
    }

    p {
        margin: 0;
    }

    div {
        display: flex;
        align-items: center;
    }

    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
        gap: 10px;
    }

    button {
        background-color: #00fa15d7;
        color: #ffffff;
        border: none;
        padding: 10px;
        cursor: pointer;
        max-width: min-content;
    }

</style>
