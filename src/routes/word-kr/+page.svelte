<script lang="ts">
  import '../../app.css';
  import Box from '../../components/Box.svelte';
  import Button from '../../components/Button.svelte';
  import Charbox from '../../components/Charbox.svelte';

	import SelectModal from '../../components/SelectModal.svelte';
  import Guess from '../../components/Guess.svelte';
  import { chars, specialties, elements, parties } from '../../components/Data.ts';
  import { SvelteToast, toast } from '@zerodevx/svelte-toast';

  let showModal = false;

  type Image = {
    name: string;
    src: string;
    selected: number;
  }

  const path = ""; // static path to images
  const i18n = "kr";
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
  let guessComplete: boolean = false;
  let guessResult: boolean = false;
  let share: string = "젠레스 존 제로 워들: 시유 방어전 파티를 맞췄어요!";
  const correct = parties[Math.floor(Math.random()*parties.length)];
  const onGuess = () => {
    if (guess_verdict.length >= 5) {
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
    if (!guessComplete) {
      guess_verdict = [...guess_verdict, guess];
      pos_guessed = [...pos_guessed, position];
    }
    if (guess == 444) {
      guessComplete = true;
      guessResult = true;
      share += '\n';
      for (let i = 0; i < guess_verdict.length; i++) {
        let tmp = "";
        for (let j = 2; j >= 0; j--) {
          // calc guess from guess(444)
          let tmp_guess = Math.floor(guess_verdict[i] / Math.pow(10, j)) % 10;
          if (tmp_guess == 0) {
            tmp += '🔴';
            continue;
          }
          if (tmp_guess == 1) {
            if (Math.floor(pos_guessed[i] / Math.pow(10, 2*j+1)) % 10 == 1) {
              tmp += '⚔️';
            } else if (Math.floor(pos_guessed[i] / Math.pow(10, 2*j+1)) % 10 == 2) {
              tmp += '🔨';
            } else if (Math.floor(pos_guessed[i] / Math.pow(10, 2*j+1)) % 10 == 3) {
              tmp += '☢️';
            } else if (Math.floor(pos_guessed[i] / Math.pow(10, 2*j+1)) % 10 == 4) {
              tmp += '🚀';
            } else if (Math.floor(pos_guessed[i] / Math.pow(10, 2*j+1)) % 10 == 5) {
              tmp += '🛡️';
            }
          }
          if (tmp_guess == 2) {
            if (Math.floor(pos_guessed[i] / Math.pow(10, 2*j)) % 10 == 1) {
              tmp += '💥';
            } else if (Math.floor(pos_guessed[i] / Math.pow(10, 2*j)) % 10 == 2) {
              tmp += '🔥';
            } else if (Math.floor(pos_guessed[i] / Math.pow(10, 2*j)) % 10 == 3) {
              tmp += '❄️';
            } else if (Math.floor(pos_guessed[i] / Math.pow(10, 2*j)) % 10 == 4) {
              tmp += '⚡';
            } else if (Math.floor(pos_guessed[i] / Math.pow(10, 2*j)) % 10 == 5) {
              tmp += '💫';
            }
          }
          if (tmp_guess == 3) {
            tmp += '🟡';
            continue;
          }
          if (tmp_guess == 4) {
            tmp += '🟢';
            continue;
          }
        }
        tmp += '\n';
        share += tmp;
      }
      share += "zzz.shelby.moe/word-kr";
    }
    if (!guessComplete && guess_verdict.length == 5) {
      guessComplete = true;
    }
    if (guessComplete) {
      // result
      if (guessResult) {
        // share
      } else {
        // failed
      }
    }
  }
</script>

<style>
  @font-face {
    font-family: 'Impact';
    src: url('https://act.hoyolab.com/app/mihoyo-zzz-game-record/fonts/Impact.ttf') format('opentype');
    font-weight: 400;
  }
  .back {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-image: url('../../../static/Background.png');
    background-size: contain;
    background-repeat: no-repeat;
    background-position: top;
    background-attachment: scroll;
    overflow-y: hidden;
  }
  .main {
    padding: 0;
    margin: 0;
    font-family: 'inpin hongmengti', sans-serif;
    font-weight: 400;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    overflow-y: auto;
  }
  .guess {
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  :root {
    --toastContainerTop: auto;
    --toastContainerRight: auto;
    --toastContainerBottom: 4rem;
    --toastContainerLeft: calc(50vw - 8rem);
  }
</style>

<svelte:head>
	<title>젠레스 에이전트 워들</title>
	<meta name="robots" content="noindex nofollow" />
	<html lang="kr" />
</svelte:head>

<div class="back"></div>
<div class="main">
  <Box --width="30em" --height="75em" --border="1em">
    <h1>젠레스 에이전트 워들</h1>
    <p>시유 방어전에 채용된 파티 구성을 맞춰 보세요.</p>
    <!--Now flex the items in a row-->
    <div style="display: flex; flex-direction: row;">
      <Charbox --width="5em" --height="10em" props={props1} charnum={charnum} i18n={i18n} bind:selected={selected} bind:showModal={showModal} />
      <Charbox --width="5em" --height="10em" props={props2} charnum={charnum} i18n={i18n} bind:selected={selected} bind:showModal={showModal} />
      <Charbox --width="5em" --height="10em" props={props3} charnum={charnum} i18n={i18n} bind:selected={selected} bind:showModal={showModal} />
      <Button on:click={() => onGuess()} class="primary sm" style="margin-top: 3.5em; margin-left: 1em;">
           확인!  
      </Button>
    </div>
    <SelectModal --width="32em" --height="32em" props={sprops} i18n={i18n} bind:clicked bind:charnum bind:showModal={showModal}/>
    <!--Append the new items by onGuess()-->
    <ol class="guess">
      {#each guess_verdict as guess, i}
          <p>시도 {i+1}/5</p>
          <Guess guess={guess} position={pos_guessed[i]} />
      {/each}
    </ol>
    {#if guessComplete && !guessResult}
      <h1>다음 기회에!</h1>
    {/if}
    {#if guessComplete && guessResult}
    <div style="display: flex; flex-direction: row; margin: 1em;">
      <a href={"https://twitter.com/intent/tweet?text="+encodeURI(share)} target="_blank" style="width: 64px; height: 64px;">
        <img src="Twitter.png" alt="Twitter." style="width: 100%; height: 100%;" />
      </a>
      <div style="width: 2em;"></div>
      <!-- svelte-ignore a11y-invalid-attribute a11y-click-events-have-key-events a11y-no-static-element-interactions a11y-missing-attribute -->
      <a class="button-style" on:click={() => {
        navigator.clipboard.writeText(share);
        toast.push('복사되었습니다!', {duration: 2000, reversed: true, intro: { y: 192 }, theme: {
          '--toastBarHeight': 0
        }});
      }}>
        <img src="Link.png" alt="Copy the result." width="64" height="64" />
      </a>
    </div>
    <SvelteToast/>
    {/if}
  </Box>
</div>