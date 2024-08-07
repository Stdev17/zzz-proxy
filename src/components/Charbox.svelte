<script lang="ts">
  import Char from './Char.svelte';

  export let props: { src: string; name: string; selected: number };

  export let charnum: number;
  export let selected: number;

  export let showModal: boolean;
  export let i18n: string = "en";

  const i18nKR: Record<string, string> = {
    "Zhu Yuan": "주연",
    "Ellen": "엘렌",
    "Grace": "그레이스",
    "Rina": "리나",
    "Koleda": "콜레다",
    "Nekomata": "네코마타",
    "Soldier 11": "11호",
    "Lycaon": "리카온",
    "Anby": "엔비",
    "Nicole": "니콜",
    "Corine": "코린",
    "Billy": "빌리",
    "Anton": "앤톤",
    "Ben": "벤",
    "Soukaku": "소우카쿠",
    "Lucy": "루시",
    "Piper": "파이퍼",
  };

  const i18nJP: Record<string, string> = {
    "Zhu Yuan": "朱鳶",
    "Ellen": "エレン",
    "Grace": "グレース",
    "Rina": "リナ",
    "Koleda": "クレタ",
    "Nekomata": "猫又",
    "Soldier 11": "１１号",
    "Lycaon": "ライカン",
    "Anby": "アンビー",
    "Nicole": "ニコ",
    "Corine": "カリン",
    "Billy": "ビリー",
    "Anton": "アンドー",
    "Ben": "ベン",
    "Soukaku": "蒼角",
    "Lucy": "ルーシー",
    "Piper": "パイパー",
  };

</script>

<style>
  .charbox {
    padding: 0rem;
    width: var(--width, auto);
    height: var(--height, auto);
    margin: 0.4rem;
    background-color: #fcfcfc;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
  }
</style>

<div class="charbox">
  <slot>
    <Char src={props.src} bind:charname={props.name} props={props} bind:charnum={charnum} bind:selected={selected} charid={charnum} bind:showModal={showModal} --width="3.6rem" --height="4.8em"/>
    {#if i18n == "en"}
      <p>{props.name}</p>
    {:else if i18n == "kr"}
      <p>{i18nKR[props.name]}</p>
    {:else if i18n == "jp"}
      <p>{i18nJP[props.name]}</p>
    {/if}
  </slot>
</div>
