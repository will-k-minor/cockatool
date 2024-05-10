
<script lang=ts>
    import './Ingredients.css'
    export let ingredient: string;
    export let removeIngredient: Function;
</script>

<button class="ingredient-card" >
    <div class="card-header">
        <button class="x-button" on:click={() => removeIngredient()}>-</button>
    </div>
    <img src="src/assets/bottle.png" alt="bottle" class="icon-image"/>
    <input 
        type="text"
        bind:value={ingredient}
    />
</button>