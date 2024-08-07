<script lang="ts">
    export let props: { src: string; name: string; selected: number };
    export let i18n: string = "en";
    const chars: string[] = [
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
    export let charnum: number = 0;
    export let selected: number = 0;
    export let clicked: boolean = false;

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

<Modal bind:showModal={showModal} bind:clicked={clicked}>
    <div slot="header">
        {#if i18n === "en"}
            <h2>Agent Select</h2>
        {:else if i18n === "kr"}
            <h2>에이전트 선택</h2>
        {/if}
    </div>
    <slot>
        <ol class="grid">
            {#each chars as char, i}
                <Char src={char + ".png"} charname={char} props={props} bind:clicked={clicked} bind:charnum bind:selected charid={i} bind:showModal={showModal} --width="4em" --height="5.2em" --margin="0.5em"/>
            {/each}
        </ol>
    </slot>
</Modal>