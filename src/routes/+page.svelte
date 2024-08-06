<script lang="ts">
  import '../app.css';
  import Box from '../components/Box.svelte';
  import Button from '../components/Button.svelte';
  import Charbox from '../components/Charbox.svelte';

	import SelectModal from '../components/SelectModal.svelte';
  import Guess from '../components/Guess.svelte';

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
  const specialties: Record<string, string> = {
    "Zhu Yuan": "Attack",
    "Ellen": "Attack",
    "Grace": "Anomaly",
    "Rina": "Support",
    "Koleda": "Stun",
    "Nekomata": "Attack",
    "Soldier 11": "Attack",
    "Lycaon": "Stun",
    "Anby": "Stun",
    "Nicole": "Support",
    "Corine": "Attack",
    "Billy": "Attack",
    "Anton": "Attack",
    "Ben": "Defense",
    "Soukaku": "Support",
    "Lucy": "Support",
    "Piper": "Anomaly",
  };
  const elements: Record<string, string> = {
    "Zhu Yuan": "Ether",
    "Ellen": "Ice",
    "Grace": "Electric",
    "Rina": "Electric",
    "Koleda": "Fire",
    "Nekomata": "Physical",
    "Soldier 11": "Fire",
    "Lycaon": "Ice",
    "Anby": "Electric",
    "Nicole": "Ether",
    "Corine": "Physical",
    "Billy": "Physical",
    "Anton": "Electric",
    "Ben": "Fire",
    "Soukaku": "Ice",
    "Lucy": "Fire",
    "Piper": "Physical",
  };

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
    name1 = charname;
    clicked = false;
  } else if (selected == 2 && clicked) {
    props2 = {
      name: charname,
      src: path + charname + ".png",
      selected: 2,
    };
    name2 = charname;
    clicked = false;
  } else if (selected == 3 && clicked) {
    props3 = {
      name: charname,
      src: path + charname + ".png",
      selected: 3,
    };
    name3 = charname;
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

  let newGuess: string[] = [name1, name2, name3];
  let guess_verdict: number[] = [];
  let pos_guessed: number[] = [];
  const correct = ["Zhu Yuan", "Anby", "Nicole"];
  const onGuess = () => {
    if (guess_verdict.length >= 4) {
      return;
    }
    newGuess = [name1, name2, name3];
    let guess: number = 0;
    let position: number = 0;
    let tmp_position: number = 0;
    for (let i: number = 0; i <= 2; i++) {
      guess *= 10;
      position *= 100;
      // calc position
      if (specialties[newGuess[i]] == "Attack") {
        tmp_position = 1;
      } else if (specialties[newGuess[i]] == "Stun") {
        tmp_position = 2;
      } else if (specialties[newGuess[i]] == "Anomaly") {
        tmp_position = 3;
      } else if (specialties[newGuess[i]] == "Support") {
        tmp_position = 4;
      } else if (specialties[newGuess[i]] == "Defense") {
        tmp_position = 5;
      }
      position += tmp_position * 10;
      if (elements[newGuess[i]] == "Physical") {
        tmp_position = 1;
      } else if (elements[newGuess[i]] == "Fire") {
        tmp_position = 2;
      } else if (elements[newGuess[i]] == "Ice") {
        tmp_position = 3;
      } else if (elements[newGuess[i]] == "Electric") {
        tmp_position = 4;
      } else if (elements[newGuess[i]] == "Ether") {
        tmp_position = 5;
      }
      position += tmp_position;
      if (specialties[correct[i]] == specialties[newGuess[i]]) {
        guess++;
      }
      if (elements[correct[i]] == elements[newGuess[i]]) {
        guess += 2;
      }
      // check if the guess is correct
      if (correct[i] == newGuess[i]) {
        guess = 10 * Math.floor(guess / 10) + 4;
      }
    }
    guess_verdict = [...guess_verdict, guess];
    pos_guessed = [...pos_guessed, position];
    if (guess_verdict.length == 4) {
      // result
    }
  }
</script>

<style>
  .main {
    padding: 0;
    margin: 0;
    background-image: url('../../static/Background.png');
    background-size: contain;
    background-repeat: no-repeat;
    background-attachment: fixed;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  .guess {
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
</style>

<div class="main">
  <Box --width="30em" --height="65em" --border="1em">
    <h1>ZZZ Agent Wordle</h1>
    <p>Guess the party which is used in Shiyu Defense.</p>
    <!--Now flex the items in a row-->
    <div style="display: flex; flex-direction: row;">
      <Charbox --width="5em" --height="10em" props={props1} charnum={charnum} bind:selected={selected} bind:showModal={showModal} />
      <Charbox --width="5em" --height="10em" props={props2} charnum={charnum} bind:selected={selected} bind:showModal={showModal} />
      <Charbox --width="5em" --height="10em" props={props3} charnum={charnum} bind:selected={selected} bind:showModal={showModal} />
      <Button on:click={() => onGuess()} class="primary sm" style="margin-top: 3.5em; margin-left: 1em;">
        Guess!
      </Button>
    </div>
    <SelectModal --width="32em" --height="32em" props={sprops} bind:clicked bind:charnum bind:showModal={showModal}/>
    <!--Append the new items by onGuess()-->
    <ol class="guess">
      {#each guess_verdict as guess, i}
          <p>Guess {i+1}</p>
          <Guess guess={guess} position={pos_guessed[i]} />
      {/each}
    </ol>
  </Box>
</div>