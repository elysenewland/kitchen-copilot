<script>
    let userIngredients = []; 
    let hasSearched = false;
    let isLoading = false;

    // Create checkbox array of ingredients for user
    let ingredients = [
      { value: "flour", name: "Flour" },
      { value: "oats", name: "Oats" },
      { value: "cornmeal", name: "Cornmeal" },
      { value: "sugar", name: "Sugar" },
      { value: "brown_sugar", name: "Brown Sugar" },
      { value: "honey", name: "Honey" },
      { value: "baking_powder", name: "Baking Powder" },
      { value: "baking_soda", name: "Baking Soda" },
      { value: "cornstarch", name: "Cornstarch" },
      { value: "cocoa", name: "Cocoa" },
      { value: "yeast", name: "Yeast" },
      { value: "milk", name: "Milk" },
      { value: "butter", name: "Butter" },
      { value: "eggs", name: "Eggs" },
      { value: "cheese", name: "Cheese" },
      { value: "cinnamon", name: "Cinnamon" },
      { value: "cloves", name: "Cloves" },
      { value: "nutmeg", name: "Nutmeg" },
      { value: "banana", name: "Bananas" },
      { value: "apples", name: "Apples" },
      { value: "pineapple", name: "Pineapple" },
      { value: "coconut", name: "Coconut" },
      { value: "strawberries", name: "Strawberries" },
      { value: "blueberries", name: "Blueberries" },
      { value: "lemon", name: "Lemon" },
      { value: "walnuts", name: "Walnuts" },
      { value: "pecans", name: "Pecans" },
      { value: "cashews", name: "Cashews" },
      { value: "peanuts", name: "Peanuts" },
      { value: "chocolate_chips", name: "Chocolate Chips" },
    ];

    // Create recipe array to store recipes in
    let recipes = [] 

    // Fetch recipes from spoonacular API based on user's checked boxes 
    // and put them in recipes array
    async function fetchRecipes() {
        if (userIngredients.length === 0) {
            console.log("Error");
            alert("Please select at least one ingredient");
        } else { 
            isLoading = true;
            const response = await fetch(`https://api.spoonacular.com/recipes/findByIngredients?ingredients=${userIngredients.join(',')}&apiKey=d9b9b7cd4a264da1bbf4e83c3302b689`)
            recipes = await response.json();
            isLoading = false;
            hasSearched = true;
        }
    }

</script>

<div class="hero">
    <h2>Discover Delicious Recipes with Ingredients Already in Your Kitchen</h2>
</div>

<!-- Prompt user to click check boxes of ingredients -->
<div class="ingredients">
    <h2>What ingredients do you have?</h2>
    <ul class="ingredient-list">
        {#each ingredients as checkbox}
        <li>
            <label>
                <input class="checkbox" type="checkbox" name="options" value={checkbox.value} bind:group={userIngredients}>
                {checkbox.name}
            </label>
        </li>
        {/each}
    </ul>

    <!-- Button to find recipes based on clicked check boxes -->
    <button on:click={fetchRecipes}>Find Recipes</button>
</div>
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

