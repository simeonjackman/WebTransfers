<script>
import { onMount } from "svelte";
let players = [];
onMount(async () => {
	console.log("Getting players")
    await fetch(`http://premierleaguefantasy.site/players`,{
		mode: 'cors',
	})
	.then(response => response.json())
	.then(
		(data) => {
			players = data
			console.log(players[10])
		})
  })
</script>

<style>
	
</style>

<svelte:head>
	<title>Premier League Fantasy Transfers</title>
</svelte:head>


<div class="flex flex-col">
	<div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
		<div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
			<div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
				<table class="min-w-full divide-y divide-gray-200">
				<thead>
					<tr>
					<th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
						Name
					</th>
					<th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
						Cost
					</th>
					<th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
						Transfers
					</th>
					<th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
						Goals
					</th>
					<th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
						Assists
					</th>
					<th class="px-6 py-3 bg-gray-50"></th>
					</tr>
				</thead>
					<tbody class="bg-white divide-y divide-gray-200">
						{#each players as player}
							<tr>
							<td class="px-6 py-4 whitespace-no-wrap">
								<div class="flex items-center">
								<div class="flex-shrink-0 h-10 w-10">
									<img class="h-10 w-10 rounded-full" src={'https://resources.premierleague.com/premierleague/photos/players/40x40/p' + player.code + ".png"} alt="">
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