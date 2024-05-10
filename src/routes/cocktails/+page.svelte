<script lang=ts>
    import "./Page.css"
    import IngredientCard from "./Ingredients/IngredientCard.svelte";
    import RecipeCard from "./Recipes/RecipeCard.svelte";
    import type { RecipeType } from './CocktailTypes.ts';

    //useState
    let ingredients: string[] = [];
    let recipes: RecipeType[] = [];
    let loading = false;

    function addIngredientField() {
        ingredients = [...ingredients, ''];
    }

    // useEffect
    $: console.log(ingredients);

    function removeIngredient(index: number) {
        ingredients = ingredients.filter((_, i) => i !== index);
    }

    async function fetchCocktails() {
        loading = true;
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
        } finally {
            loading = false;
        }
    }
</script>

<span class="button-options">
    <button on:click={async () => await fetchCocktails()}>
        <img src={'src/assets/cocktail.png'} alt='cocktail' class="icon-image"/>
        Fetch cocktails
    </button>    
</span>

<div class="grid-container">
    {#each ingredients as ingredient, i}
        <IngredientCard bind:ingredient={ingredient} removeIngredient={() => removeIngredient(i) }/>
    {/each}
    <div class="add-ingredient-card">
        <button class="add-ingredient-button" on:click={addIngredientField}>+</button>
    </div>
</div>

{#if loading }
    <p>Loading... </p>
{:else if recipes.length === 0}
    <p>No recipes found</p>
{:else}
    <p>Recipes found: {recipes.length}</p>
{/if}

{#each recipes as recipe, i}
    <RecipeCard {recipe} />
{/each}
