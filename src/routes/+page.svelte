<script>
    let userIngredients = []; 
    let hasSearched = false;
    let isLoading = false;

    // Create checkbox array of ingredients for user
    let ingredients = [
      { value: "flour", name: "Flour" },
      { value: "sugar", name: "Sugar" },
      { value: "brown_sugar", name: "Brown Sugar" },
      { value: "salt", name: "Salt" },
      { value: "baking_powder", name: "Baking Powder" },
      { value: "baking_soda", name: "Baking Soda" },
      { value: "yeast", name: "Yeast" },
      { value: "cinnamon", name: "Cinnamon" },
      { value: "milk", name: "Milk" },
      { value: "oats", name: "Oats" },
    ];

    // Create recipe array to store recipes in
    let recipes = [] 

    // Fetch recipes from spoonacular API based on user's checked boxes 
    // and put them in recipes array
    async function fetchRecipes() {
        if (userIngredients.length === 0) {
            console.log("Error");
            alert("Hold up, please select at least one ingredient");
        } else { 
            isLoading = true;
            const response = await fetch(`https://api.spoonacular.com/recipes/findByIngredients?ingredients=${userIngredients.join(',')}&apiKey=d9b9b7cd4a264da1bbf4e83c3302b689`)
            recipes = await response.json();
            isLoading = false;
            hasSearched = true;
        }
    }

</script>

  <!-- Prompt user to click check boxes of ingredients -->
<h2>What ingredients do you have?</h2>
<div id="ingredients">
    {#each ingredients as checkbox}
        <label>
            <input type="checkbox" name="options" value={checkbox.value} bind:group={userIngredients}>
            {checkbox.name}
        </label>
      <br>
    {/each}
</div>

<!-- Button to find recipes based on clicked check boxes -->
<button on:click={fetchRecipes}>Find Recipes</button>

<!-- If page is loading, return loading state -->
{#if isLoading}
    <p>Loading…</p>
{/if} 

<!-- Return recipes listed with name and image (if available) -->
{#if hasSearched && !isLoading}    
    <h3>Recipes</h3>
    {#each recipes as recipe}
        <div style="border: 1px solid gray; padding: 10px; display: flex; gap: 20px; margin: 10px">
            <img src="{recipe.image}" alt="{recipe.title}" style="max-width: 100px;">
            <h2><a href="/recipe-{recipe.id}">{recipe.title}</a></h2>
        </div>
    {/each}
{/if}

