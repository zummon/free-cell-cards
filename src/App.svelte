<script>
  import { onMount } from 'svelte'

  let deck = $state([
    ["♢", "A"],
    ["♢", "2"],
    ["♢", "3"],
    ["♢", "4"],
    ["♢", "5"],
    ["♢", "6"],
    ["♢", "7"],
    ["♢", "8"],
    ["♢", "9"],
    ["♢", "10"],
    ["♢", "J"],
    ["♢", "Q"],
    ["♢", "K"],
    ["♡", "A"],
    ["♡", "2"],
    ["♡", "3"],
    ["♡", "4"],
    ["♡", "5"],
    ["♡", "6"],
    ["♡", "7"],
    ["♡", "8"],
    ["♡", "9"],
    ["♡", "10"],
    ["♡", "J"],
    ["♡", "Q"],
    ["♡", "K"],
    ["♣", "A"],
    ["♣", "2"],
    ["♣", "3"],
    ["♣", "4"],
    ["♣", "5"],
    ["♣", "6"],
    ["♣", "7"],
    ["♣", "8"],
    ["♣", "9"],
    ["♣", "10"],
    ["♣", "J"],
    ["♣", "Q"],
    ["♣", "K"],
    ["♠", "A"],
    ["♠", "2"],
    ["♠", "3"],
    ["♠", "4"],
    ["♠", "5"],
    ["♠", "6"],
    ["♠", "7"],
    ["♠", "8"],
    ["♠", "9"],
    ["♠", "10"],
    ["♠", "J"],
    ["♠", "Q"],
    ["♠", "K"]
  ]);
  let duals = $state([[], []]);

  function shuffle () {
    duals = duals.map((dual) => {
      dual.forEach((card) => {
        deck.push(card);
      });
      return [];
    });
    deck.sort(() => Math.random() - 0.5);
  }

  onMount(() => {
    shuffle();
  })

</script>

<div class="p-4">
  <div class="mx-auto w-fit">
    <button class="block w-24 h-32 rounded bg-zinc-100 text-zinc-900 overflow-hidden text-4xl" onclick={() => { shuffle(); }}>
      ⟳
    </button>
  </div>
</div>
<div class="flex flex-wrap gap-4 p-4">
  {#each duals as dual, index}
    <div class="bg-zinc-700 p-1">
      <div class="font-semibold border-b">Player {index + 1}</div>
      <div class="flex divide-x">
        {#each dual as card}
          <div class="px-1">
            <div class="font-semibold">{card[1]}</div>
            <div class="text-4xl">{card[0]}</div>
          </div>
        {/each}
        <div class="">
          <button class="text-4xl text-green-300" onclick={() => { dual.push(deck.pop()); }}>✜</button>
        </div>
      </div>
    </div>
  {/each}
  <div class="">
    <button class="text-4xl text-green-300" onclick={() => { duals.push([]); }}>✜</button>
  </div>
</div>
<div class="flex flex-wrap gap-4 p-4">
  {#each deck as card}
    <div class="px-1">
      <div class="font-semibold">{card[1]}</div>
      <div class="text-4xl">{card[0]}</div>
    </div>
  {/each}
</div>

