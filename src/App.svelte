<script>
  import { onMount } from 'svelte'

  const deck = [
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
  ]

  let duals = $state([])
	let complete = $state([])
	let board = $state([])

  function shuffle () {
		duals = [[], [], [], []]
		complete = [[], [], [], []]
    board = [[], [], [], [], [], [], [], []]
    let pack = deck.toSorted(() => Math.random() - 0.5)
		pack.forEach((card, index) => {
			const idx = index % board.length
			board[idx].push(card)
		})
  }

	function simulate (pick, chunkindex) {
		if (pick[1] == 'A') {
			let idx = 0
			for (const slot of complete) {
				if (!slot[0]) {
					complete[idx] = pick
					board[chunkindex].pop()
					break 
				}
				idx++
			}
			return 
		}
		let idx = 0
		for (const slot of duals) {
			if (!slot[0]) {
				duals[idx] = pick
				board[chunkindex].pop()
				break
			}
			idx++
		}
	}

  onMount(() => {
    shuffle()
  })

</script>

<div class="flex flex-wrap gap-4 p-4 justify-between">
  {#each duals as card}
		<div class="px-1 border">
			<div class="font-semibold">{card[1]}</div>
			<div class="text-4xl">{card[0]}</div>
		</div>
  {/each}
	<div>
		<button class="text-4xl text-red-400 hover:text-red-600" onclick={() => { 
			shuffle() 
		}}>
			⟳
		</button>
	</div>
  {#each complete as card}
		<div class="px-1 border">
			<div class="font-semibold">{card[1]}</div>
			<div class="text-4xl">{card[0]}</div>
		</div>
  {/each}
</div>

<div class="flex flex-wrap gap-4 p-4">
  {#each board as chunk, chunkindex}
		{@const card = chunk.at(-1)}
		<div class="">
			{#each chunk.slice(0, -1) as card}
				<div class="px-1 border-t border-x cursor-default">
					<span class="font-semibold">{card[1]}</span>
					<span class="text-2xl">{card[0]}</span>
				</div>
			{/each}
			<button class="block w-full px-1 border cursor-pointer" onclick={() => {
				simulate(card, chunkindex)
			}}>
				<span class="block text-left font-semibold">{card[1]}</span>
				<span class="block text-4xl">{card[0]}</span>
			</button>
		</div>
  {/each}
</div>
