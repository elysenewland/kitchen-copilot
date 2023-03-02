<script>
    const d = new Date();
	let year = d.getFullYear();
    import "@fontsource/poppins/400.css";
    import "@fontsource/poppins/800.css";
</script>

<header class="app-header">
    <div class="app-header-container">
        <h1><a href="/">Kitchen Copilot</a></h1>
    </div>
</header>

<main>
    <!-- page content -->
    <slot></slot>
</main>

<footer>
    <p>Kitchen Copilot &ndash; Copyright &copy; {year}</p>
</footer>