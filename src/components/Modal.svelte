<script lang="ts">
    export let showModal: boolean;
    export let clicked: boolean = false;

    let dialog: HTMLDialogElement;

    $: if (dialog && showModal) {
        dialog.showModal();
    } else if (dialog) {
        dialog.close();
    }
</script>

<!-- svelte-ignore a11y-click-events-have-key-events a11y-no-noninteractive-element-interactions -->
<dialog
bind:this={dialog}
on:close={() => (showModal = false)}
on:click|self={() => {{dialog.close(); clicked = false;}}}
>
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <div on:click|stopPropagation style="align-items: right;">
        <slot name="header" />
        <hr />
        <slot />
        <hr />
        <!-- svelte-ignore a11y-autofocus -->
        <button autofocus on:click={() => {{dialog.close(); clicked = false;}}}>close</button>
    </div>
</dialog>

<style>
    dialog {
		max-width: 24em;
		border-radius: 0.5em;
		border: none;
		padding: 0;
	}
	dialog::backdrop {
		background: rgba(0, 0, 0, 0.3);
	}
	dialog > div {
		padding: 1em;
	}
	dialog[open] {
		animation: zoom 0.25s cubic-bezier(0.34, 1.56, 0.64, 1);
	}
	@keyframes zoom {
		from {
			transform: scale(0.92);
		}
		to {
			transform: scale(1);
		}
	}
	dialog[open]::backdrop {
		animation: fade 0.25s ease-out;
	}
	@keyframes fade {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
	button {
		display: block;
	}
</style>