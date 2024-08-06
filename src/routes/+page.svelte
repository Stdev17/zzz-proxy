<script lang="ts">
  import '../app.css';
  import Box from '../components/Box.svelte';
  import Button from '../components/Button.svelte';
  import Charbox from '../components/Charbox.svelte';

	import SelectModal from '../components/SelectModal.svelte';

  let showModal = false;

  type Image = {
    name: string;
    src: string;
    selected: number;
  }

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

  const path = ""; // static path to images
  let name1 = "Ellen";
  let name2 = "Lycaon";
  let name3 = "Soukaku";
  let charnum: number = 0;
  let selected = 0;
  let charname: string = "";
  let clicked = false;
  let props1: Image = {
    name: name1,
    src: path + name1 + ".png",
    selected: 1,
  }
  let props2: Image = {
    name: name2,
    src: path + name2 + ".png",
    selected: 2,
  }
  let props3: Image = {
    name: name3,
    src: path + name3 + ".png",
    selected: 3,
  }
  let sprops: Image = {
    name: charname,
    src: path + charname + ".png",
    selected: 0,
  }
  $: if (selected == 1 && clicked) {
    props1 = {
      name: charname,
      src: path + charname + ".png",
      selected: 1,
    };
    clicked = false;
  } else if (selected == 2 && clicked) {
    props2 = {
      name: charname,
      src: path + charname + ".png",
      selected: 2,
    };
    clicked = false;
  } else if (selected == 3 && clicked) {
    props3 = {
      name: charname,
      src: path + charname + ".png",
      selected: 3,
    };
    clicked = false;
  }
  $: charname = chars[charnum];
  $: sprops = {
    name: charname,
    src: path + charname + ".png",
    selected: selected,
  }
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
      <Charbox --width="5em" --height="11em" props={props1} charnum={charnum} bind:selected={selected} bind:showModal={showModal} />
      <Charbox --width="5em" --height="11em" props={props2} charnum={charnum} bind:selected={selected} bind:showModal={showModal} />
      <Charbox --width="5em" --height="11em" props={props3} charnum={charnum} bind:selected={selected} bind:showModal={showModal} />
      <Button class="primary sm" style="margin-top: 3.5em; margin-left: 1em;">
        Guess!
      </Button>
    </div>
    <SelectModal --width="32em" --height="32em" props={sprops} bind:clicked bind:charnum bind:showModal={showModal}/>
  </Box>
</div>
