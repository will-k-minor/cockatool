
<script lang=ts>
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

<style>
    .ingredient-card {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        padding: 4px;
        margin: 10px;
        min-width: 150;
        min-height: 250;
        max-width: fit-content;
        max-height: fit-content;
        border: 1px solid #000000;
        border-radius: 8px;
        background-color: #00aeff;
    }

    .card-header {
        display: flex;
        justify-content: right;
        width: 100%;
    }

    .icon-image {
        width: 50px;
        height: 50px;
        object-fit: contain;
    }

    input {
        padding: 5px;
        margin: 10px;
        border-radius: 12px;
    }

    .x-button {
        background-color: #ff0000d7;
        color: #ffffff;
        border: none;
        padding: 10px;
        cursor: pointer;
        max-width: min-content;
    }
</style>