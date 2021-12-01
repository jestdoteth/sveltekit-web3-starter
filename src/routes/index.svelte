<script>
	import Web3 from '$lib/Web3.svelte';
</script>

<Web3 let:connect let:address let:avatar let:balance let:displayName let:connecting>
	{#if address}
		<p>Your address is {address}</p>
		{#if displayName}
			<p>Your ENS name is {displayName}</p>
			{#if avatar}
				<img height="128" alt={displayName} src={avatar} />
			{:else}
				<p>No avatar NFT found</p>
			{/if}
		{:else}
			<p>No ENS name found for your address</p>
		{/if}
		{#if balance}
			<p>Your balance is {Number(balance).toFixed(3)}ETH</p>
		{/if}
	{:else if connecting}
		<p>Connecting...</p>
	{:else}
		<button on:click={connect}>Connect</button>
	{/if}
</Web3>
