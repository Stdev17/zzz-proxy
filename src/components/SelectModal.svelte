<script lang="ts">
    const chars = [
        "Zhu Yuan",
        "Ellen",
        "Grace",
        "Rina",
        "Koleda",
        "Nekomata",
        "Soldier 11",
        "Lycaon",
        "Anby",
        "Nicole",
        "Corine",
        "Billy",
        "Anton",
        "Ben",
        "Soukaku",
        "Lucy",
        "Piper",
    ];
    import Char from './Char.svelte';
    import Modal from './Modal.svelte';

    export let showModal: boolean;
</script>
<style>
  .grid {
    padding: 1em;
    margin: 0;
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-template-rows: repeat(3, 1fr);
  }
</style>

<Modal showModal={showModal}>
    <div slot="header">
        <h2>Agent Select</h2>
    </div>
    <slot>
        <ol class="grid">
            {#each chars as char}
                <Char src={char + ".png"} name={char} bind:showModal={showModal} --width="4em" --height="5.2em" --margin="0.5em"/>
            {/each}
        </ol>
    </slot>
</Modal>