<script>
import { onMount } from "svelte";
let searchFilter = "";
let players = [];
$: currentPlayers = players.filter(item => item.first_name.toLowerCase().includes(searchFilter) || item.second_name.toLowerCase().includes(searchFilter.toLowerCase()));

onMount(async () => {
	console.log("Getting players")
    await fetch(`http://premierleaguefantasy.site/players?sort_by=transfers_in_event`,{
		mode: 'cors',
	})
	.then(response => response.json())
	.then(
		(data) => {
			players = data
			currentPlayers = players
			console.log(players[10])
		})
  })
let sortDict = {};

function sortPlayers(key) {
	if (key in sortDict){
		sortDict[key] = sortDict[key] * -1 // invert sort order
	} else {
		sortDict[key] = 1
	}
	const direction = sortDict[key]
	currentPlayers = currentPlayers.sort(function(a, b) {
	// direction is used for reverse sort
	let keyA = a[key];
	let keyB = b[key];
	// Compare the 2 keys
	if (keyA < keyB) return -1 * direction;
	if (keyA > keyB) return 1 * direction;
	return 0;
	}).reverse();
	}

</script>

<style>
	
</style>

<svelte:head>
	<title>Premier League Fantasy Transfers</title>
</svelte:head>





<div class="flex flex-col">

	<input bind:value={searchFilter} class="px-6 py-3 bg-gray-50 text-left font-medium text-blue-500 uppercase tracking-wider rounded-full" type="text" placeholder="Search...">

	<div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
		<div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
			<div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
				<table class="min-w-full divide-y divide-gray-200">
				<thead>
					<tr>
					<th on:click={() => sortPlayers("second_name")} class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
						Name
					</th>
					<th on:click={() => sortPlayers("now_cost")} class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
						Cost
					</th>
					<th on:click={() => sortPlayers("transfers_in_event")} class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
						Transfers
					</th>
					<th on:click={() => sortPlayers("goals_scored")} class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
						Goals
					</th>
					<th on:click={() => sortPlayers("assists")} class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
						Assists
					</th>
					<th on:click={() => sortPlayers("total_points")} class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
						Total Points
					</th>
					<th class="px-6 py-3 bg-gray-50"></th>
					</tr>
				</thead>
					<tbody class="bg-white divide-y divide-gray-200">
						{#each currentPlayers.reverse() as player}
							<tr>
							<td class="px-6 py-4 whitespace-no-wrap">
								<div class="flex items-center">
								<div class="flex-shrink-0 h-10 w-10">
									<!-- <img class="h-10 w-10 rounded-full" src={'https://resources.premierleague.com/premierleague/photos/players/40x40/p' + player.code + ".png"} alt=""> -->
								</div>
								<div class="ml-4">
									<div class="text-sm leading-5 font-medium text-gray-900">
									{player.first_name} {player.second_name}
									</div>
									<div class="text-sm leading-5 text-gray-500">
									{player.selected_by_percent} %
									</div>
								</div>
								</div>
							</td>
							<td class="px-6 py-4 whitespace-no-wrap">
								<span class="px-2 inline-flex leading-5 rounded-full text-gray-900">
								{player.now_cost / 10}
								</span>
							</td>
							<td class="px-6 py-4 whitespace-no-wrap">
								<div class="text-sm leading-5 text-gray-900">+{player.transfers_in_event}</div>
								<div class="text-sm leading-5 text-gray-500">-{player.transfers_out_event}</div>
							</td>
							<td class="px-6 py-4 whitespace-no-wrap">
								<span class="px-2 inline-flex leading-5 rounded-full text-gray-900">
								{player.goals_scored}
								</span>
							</td>
							<td class="px-6 py-4 whitespace-no-wrap">
								<span class="px-2 inline-flex leading-5 rounded-full text-gray-900">
								{player.assists}
								</span>
							</td>
							<td class="px-6 py-4 whitespace-no-wrap">
								<span class="px-2 inline-flex leading-5 rounded-full text-gray-900">
								{player.total_points}
								</span>
							</td>
							<td class="px-6 py-4 whitespace-no-wrap text-right text-sm leading-5 font-medium">
								<a href="#" class="text-indigo-600 hover:text-indigo-900">Select</a>
							</td>
							</tr>
						{/each}
					</tbody>
				</table>
			</div>
		</div>
	</div>
</div>