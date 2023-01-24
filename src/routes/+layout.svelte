<script>
    const d = new Date();
	let year = d.getFullYear();
</script>

<header>
    <h1><a href="/">Kitchen Copilot</a></h1>
</header>

<main>
    <!-- page content -->
    <slot></slot>
</main>

<footer>
    <p>Kitchen Copilot &ndash; Copyright &copy; {year}</p>
</footer>

<style>
    header {
        display: flex;
        justify-content: center;
    }
    footer {
        text-align: center;
    }
</style>