<script>
  import Char from './Char.svelte';

  export let props;
</script>

<style>
  .charbox {
    padding: 0em;
    width: var(--width, auto);
    height: var(--height, auto);
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
    <Char src={props.src} char={props.name} --width="5em" --height="6.5em"/>
    <p>{props.name}</p>
  </slot>
</div>
