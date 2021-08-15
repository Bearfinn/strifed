<script lang="ts">
	import Input from '$lib/Input.svelte';

	let tokenAName = 'Token A';
	let tokenBName = 'Token B';
	let liquidityValue = 0;

	let tokenAPrice = 0;
	let tokenBPrice = 0;

	let tokenANewPrice = 0;
	let tokenBNewPrice = 0;

	const toPercent = (value: number) => {
		return (value * 100).toFixed(2) + '%';
	};

	$: r0 = tokenBPrice === 0 ? 0 : tokenAPrice / tokenBPrice;
	$: r1 = tokenBNewPrice === 0 ? 0 : tokenANewPrice / tokenBNewPrice;
	$: d0 = tokenAPrice === 0 ? 0 : tokenANewPrice / tokenAPrice;
	$: d1 = tokenBPrice === 0 ? 0 : tokenBNewPrice / tokenBPrice;
	$: p = r1 === 0 ? 0 : r0 / r1;
	$: q = d0 === 0 ? 0 : d1 / d0;

	$: il = p ? 2 * (Math.sqrt(p) / (p + 1)) - 1 : 0;
</script>

<div class="bg-gradient-to-r from-yellow-500 to-yellow-600 h-60 flex items-center text-white">
	<div class="container mx-auto px-8">
		<div class="h-16">
			<h1 class="text-2xl">Welcome to Strifed</h1>
			<h2 class="text-lg">Learn DeFi the simple way</h2>
		</div>
		<button
			class="bg-white text-gray-800 px-4 py-2 rounded-md border-2 border-white hover:bg-transparent hover:text-white transition"
		>
			Let's go!
		</button>
	</div>
</div>
<div>
	<div class="container mx-auto px-8">
		<div class="my-4">
			<h2>Impermanent loss calculator</h2>
			<div class="text-gray-400">
				Impermanent loss is the percentage of value in loss from providing liquidity compared to
				just holding.
			</div>
		</div>

		<div class="border p-4">
			<div class="flex items-center flex-wrap space-x-4">
				<div class="text-lg my-2 font-semibold">Providing liquidity of</div>
				<Input name="tokenAName" label="" bind:value={tokenAName} />
				<div>and</div>
				<Input name="tokenBName" label="" bind:value={tokenBName} />
				<div>worth</div>
				<Input name="tokenBName" label="" bind:value={liquidityValue} class="text-right" />
                <div>USD</div>
			</div>

            <hr class="my-4" />

			<div class="md:flex space-y-4 md:space-x-4 items-center flex-wrap">
				<div class="flex-1">
					<div class="text-lg my-2 font-semibold">When I provide liquidity</div>
					<Input name="tokenA" label={`${tokenAName} price`} bind:value={tokenAPrice} />
					<Input name="tokenA" label={`${tokenBName} price`} bind:value={tokenBPrice} />
				</div>

				<div class="flex-1">
					<div class="text-lg my-2 font-semibold">Currently</div>
					<Input name="tokenA" label={`${tokenAName} price`} bind:value={tokenANewPrice} />
					<Input name="tokenA" label={`${tokenBName} price`} bind:value={tokenBNewPrice} />
				</div>

				<div>
					<div>Price change of A</div>
					<div class={d0 > 0 ? "text-green-600" : "text-red-600"}>{toPercent(d0)}</div>
                    <div>Price change of B</div>
					<div class={d0 > 0 ? "text-green-600" : "text-red-600"}>{toPercent(d1)}</div>
				</div>
			</div>
		</div>

		<div class="mt-4 p-4 rounded bg-yellow-100 text-center">
			<div class="text-4xl font-bold text-yellow-600">{toPercent(il)}</div>
			<div>Impermanent loss</div>
		</div>
	</div>
</div>

<style>
	@import '../assets/css/tailwind.css';
</style>
