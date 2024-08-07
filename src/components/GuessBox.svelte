<script lang="ts">

    export let guess: number;
    export let position: number;

    let path: string = "";
    let ePath: string = "";
    let alt: string = "";

    if (Math.floor(position / 10) == 1) {
        path = "Attack.png";
        alt = "You guessed Attack and";
    } else if (Math.floor(position / 10) == 2) {
        path = "Stun.png";
        alt = "You guessed Stun and";
    } else if (Math.floor(position / 10) == 3) {
        path = "Anomaly.png";
        alt = "You guessed Anomaly and";
    } else if (Math.floor(position / 10) == 4) {
        path = "Support.png";
        alt = "You guessed Support and";
    } else if (Math.floor(position / 10) == 5) {
        path = "Defense.png";
        alt = "You guessed Defense and";
    }

    if (position % 10 == 1) {
        ePath = "Physical.png";
        alt += " Physical agent.";
    } else if (position % 10 == 2) {
        ePath = "Fire.png";
        alt += " Fire agent.";
    } else if (position % 10 == 3) {
        ePath = "Ice.png";
        alt += " Ice agent.";
    } else if (position % 10 == 4) {
        ePath = "Electric.png";
        alt += " Electric agent.";
    } else if (position % 10 == 5) {
        ePath = "Ether.png";
        alt += " Ether agent.";
    }

    if (guess == 4) {
        alt += " You guessed correctly!";
    }
</script>
  
<style>
.slot {
    margin: 1em;
    width: 4em;
    height: 4em;
    border: 1px solid black;
    border-radius: 0.5em;
    display: flex;
}
.img {
    width: 4em;
    height: 4em;
    background-size: cover;
    background-position: center;
}
</style>

{#if guess == 0}
<div class="slot" style="background-color: #f01010;">
    <slot>
    </slot>
</div>
{/if}
{#if guess == 1}
<div class="slot" style="background-color: #f0f010;">
    <slot>
        <img src={path} class="img" alt={alt} />
    </slot>
</div>
{/if}
{#if guess == 2}
<div class="slot" style="background-color: #f0f010;">
    <slot>
        <img src={ePath} class="img" alt={alt} />
    </slot>
</div>
{/if}
{#if guess == 3}
<div class="slot" style="background-color: #f0f010;">
    <slot>
    </slot> 
</div>
{/if}
{#if guess == 4}
<div class="slot" style="background-color: #10f010;">
    <slot>
    </slot>
</div>
{/if}