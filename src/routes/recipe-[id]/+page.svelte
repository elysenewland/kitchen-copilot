<script>
    import { page } from '$app/stores';
    import { onMount } from 'svelte';
    let recipeId = $page.params.id;
    let hasloaded = false;

    // Declare initial recipe array
    let recipe = [];

    // Declare checked array for unduplicated ingredient return
    let uniqueIngredients = [];

    // Fetch data from Spoonacular API, return via recipe array, then set page status to loaded
    onMount(async () => {
        const res = await fetch(`https://api.spoonacular.com/recipes/${recipeId}/information?includeNutrition=false&apiKey=d9b9b7cd4a264da1bbf4e83c3302b689`);
        recipe = await res.json();
        hasloaded = true;
        
        // Create a temporary object to check for unique ingredient names
        let temp = {};

        // If the name is not present, we add the name to the uniqueIngredients array
        recipe.extendedIngredients.forEach(item => {
        if (!temp[item.original]) {
            uniqueIngredients.push(item);
            temp[item.original] = true;
        }
    });
});
</script>

<!-- Add loading state -->
{#if !hasloaded}
    <p>Loading…</p>
    
{:else}

    <!-- Display recipe title, image and how long (minutes) til ready -->
    <article>
        <h1>{recipe.title}</h1>
        <img src="{recipe.image}" alt="Submitted photo of {recipe.title}">
        
        <p>Ready in <strong>{@html recipe.readyInMinutes} minutes.</strong></p>

        <!-- Display ingredients -->
        <h2><strong>Ingredients:</strong></h2>
        <ul>
        {#each uniqueIngredients as recipe}
            <li>{recipe.original}</li>
        {/each}
        </ul>

        <!-- Display instructions -->
        <h2><strong>Instructions:</strong></h2>
        <p>{@html recipe.instructions}</p>
        
    </article>
{/if}
