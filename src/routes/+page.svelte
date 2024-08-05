<script lang="ts">
  import '../app.css';
  import Box from '../components/Box.svelte';
  import Button from '../components/Button.svelte';
  import Charbox from '../components/Charbox.svelte';

  type Image = {
    name: string;
    src: string;
  }

  const path = "";
  let name1 = "Ellen";
  let name2 = "Lycaon";
  let name3 = "Soukaku";
  let props1: Image = {
    name: name1,
    src: "",
  }
  let props2: Image = {
    name: name2,
    src: "",
  }
  let props3: Image = {
    name: name3,
    src: "",
  }
  $: props1 = {
    name: name1,
    src: path + name1 + ".png",
  };
  $: props2 = {
    name: name2,
    src: path + name2 + ".png",
  };
  $: props3 = {
    name: name3,
    src: path + name3 + ".png",
  };
  name1 = "Ellen";
  name2 = "Lycaon";
  name3 = "Soukaku";
</script>

<style>
  .main {
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
</style>

<div class="main">
  <Box --width="30em" --height="60em" --border="1em">
    <h1>ZZZ Agent Wordle</h1>
    <p>Guess the party which is used in Shiyu Defense.</p>
    <!--Now flex the items in a row-->
    <div style="display: flex; flex-direction: row;">
      <Charbox --width="5em" --height="11em" props={props1} />
      <Charbox --width="5em" --height="11em" props={props2} />
      <Charbox --width="5em" --height="11em" props={props3} />
      <Button class="primary sm" style="margin-top: 3.5em;">
        Guess!
      </Button>
    </div>
  </Box>
</div>
