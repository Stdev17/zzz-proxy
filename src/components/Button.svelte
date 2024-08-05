<script>
	let buttonProps = {
	  ...$$restProps,
	};
  </script>
<button on:click
	on:mouseenter
	on:mouseleave
	{...buttonProps}
>
	<slot/>
</button>

<style>
	.primary{
		color: solid black;
	}
	.sm {
		font-size:1em;
		padding:0.2em;
		height: 2em;
	}
	.lg {
    font-size:2em;
    padding:0.3em;
	}
</style>
