# Kitchen Copilot
## Video Demo:  <URL HERE>
## Description:

Kitchen Copilot is a recipe website that allows users to check off ingredients they already have in their pantry or fridge and returns a list of recipes based on those checked ingredients. The choice to create a recipe website came from my personal experience as an avid home chef and baker. I like to challenge myself to make meals/baked goods with only the ingredients I have on hand.
I utilized Svelte, a Javascript-based framework, due to its increasing popularity amongst web developers and to challenge myself with something new. 

### Files
#### /routes/layout.svelte
Per Svelte documentation, the +layout.svelte file under routes describes the layout applied to every page. For my project, the header and footer style remained the same on each page and thus coded on +layout.svelte. In addition, I chose to dynamically code the copyright year using JS so that it would automatically update.  

#### /routes/+page.svelte 
Also, per Svelete documentation, the +page.svelte component is used to denote a page of the website. The +page.svelte file directly in the routes folder is the website's landing page. I opened with a JS script tag to establish variables, an array containing each ingredient included in the checkbox list, and an array to hold the recipes fetched from an API. 
I utilized the Spoonacular API (https://spoonacular.com/food-api), which holds a significant amount of food-related information. I reviewed the variables within the API to learn how to access the ingredient and recipe information. 
I wrote code to ensure the user checked at least one checkbox. If the user attempts to click the "Find Recipes" button without doing so, the code returns an alert error. 
In my HTML, I created a checkbox label and used Svelte's {#each}{/each} to check and see which ingredients were checked from the recipe array. I used Svelte's bind: group directive to group the checkbox inputs. This way, when the user checks multiple checkboxes, all inputs will be used to fetch the data from the API. Finally, I called the fetchRecipes function on the "Find Recipes" button click and coded a loading state to occur when that button is clicked (fetching data from API).
I again used Svelte's {#each}{/each} to produce each recipe result from the API data based on the checked checkboxes with both the name and image of the recipe displayed below the "Find Recipes" button.

#### /recipes-[id]/+page.svelte
When the user clicks on a recipe from the list of recipes on the homepage, they are taken to the second page. The second fetch request to the Spoonacular API is processed and returns the recipe title, image, time to make, list of ingredients, ingredient amounts, and recipe instructions when the information has loaded. Otherwise, a loading state occurs.
I found when testing my site that the API had duplicate ingredients listed. To fix this, I had to code a temporary object to check each ingredient against before returning the unique ingredient names to a new array. I also utilized @html within my paragraph tags to render the HTML within the API database.

### Design Choices
I used an established API to fetch data rather than create hardcoded JSON recipe files. This took significantly less time and taught me how to get and display data from an API, which I've never worked with before. 
I decided to display the recipe title, image, time to make, ingredient names/amounts, and instructions based on what I've seen on other popular recipe websites. 