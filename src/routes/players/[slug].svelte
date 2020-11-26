<script context="module">
	export async function preload({ params }) {
		const { slug } = params;
		console.log(slug)
		const res = await this.fetch(`http://premierleaguefantasy.site/players?sort_by=transfers_in_event&id=${slug}`);
		const data = await res.json();

		if (res.status === 200) {
			return { player: data[0] };
		} else {
			this.error(res.status, data.message);
		}
	}
</script>

<script>
	export let player;
</script>


<svelte:head>
	<title>Players</title>
</svelte:head>

<h1 class="px-6 py-3 bg-gray-900 text-center text-xl leading-4 font-medium text-gray-500 uppercase tracking-wider">{player.first_name} {player.second_name}</h1>

<div class="content flex items-center w-full justify-between mt-4">
		<div class="flex-shrink-0 h-10 w-10">
			<img class="h-10 w-10 rounded-full" src={'https://resources.premierleague.com/premierleague/photos/players/40x40/p' + player.code + ".png"} alt="">
		</div>
			<div class="text-sm leading-5 font-medium text-gray-900">
			{player.first_name} {player.second_name}
			</div>
			<div class="text-sm leading-5 text-gray-900">
			{player.selected_by_percent} %
			</div>
		<span class="text-sm leading-5 text-gray-900">
		cost: {player.now_cost / 10}
		</span>
		<div class="text-sm leading-5 text-gray-900"> Transfers in: {player.transfers_in_event}</div>
		<div class="text-sm leading-5 text-gray-900"> Transfers out: {player.transfers_out_event}</div>
		<span class="text-sm leading-5 text-gray-900">
		Goals scored: {player.goals_scored}
		</span>
		<span class="text-sm leading-5 text-gray-900">
		Assists: {player.assists}
		</span>
		<span class="text-sm leading-5 text-gray-900">
		Total points {player.total_points}
		</span>
</div>
