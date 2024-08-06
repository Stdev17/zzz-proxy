<script lang="ts">
  import Char from './Char.svelte';

  export let props: { src: string; name: string; selected: number };

  export let charnum: number;
  export let selected: number;

  export let showModal: boolean;

</script>

<style>
  .charbox {
    padding: 0em;
    width: var(--width, 5em);
    height: var(--height, 11em);
    margin: 1em;
    background-color: #fcfcfc;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
  }
</style>

<div class="charbox">
  <slot>
    <Char src={props.src} bind:charname={props.name} props={props} bind:charnum={charnum} bind:selected={selected} charid={charnum} bind:showModal={showModal} --width="5em" --height="6.5em"/>
    <p>{props.name}</p>
  </slot>
</div>
