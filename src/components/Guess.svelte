<script lang="ts">
    export let guess: number = 0;
    export let position: number = 0;

    let guess_1: number = Math.floor(guess / 100);
    let guess_2: number = Math.floor((guess % 100) / 10);
    let guess_3: number = guess % 10;

    let position_1: number = Math.floor(position / 10000);
    let position_2: number = Math.floor((position % 10000) / 100);
    let position_3: number = position % 100;    

    import GuessBox from "./GuessBox.svelte";

</script>
<style>
  .main {
    padding: 0em;
    margin: 0em;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
  }
</style>

<div>
    <slot>
        <div class="main">
            <GuessBox guess={guess_1} position={position_1}/>
            <GuessBox guess={guess_2} position={position_2}/>
            <GuessBox guess={guess_3} position={position_3}/>
        </div>
    </slot>
</div>