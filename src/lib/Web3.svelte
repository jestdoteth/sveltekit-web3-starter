<script context="module">
	import { ethers } from 'ethers';
	import Web3Modal from 'web3modal';
	import WalletConnectProvider from '@walletconnect/web3-provider/dist/umd/index.min.js';
	import { writable } from 'svelte/store';

	export const store = writable({
		modal: null,
		provider: null,
		web3: null,
		address: null,
		avatar: null,
		displayName: null,
		balance: null,
		balanceRaw: null,
		connecting: false
	});
</script>

<script>
	import { onMount } from 'svelte';

	export let cacheProvider = true;
	export let network = 'mainnet';

	onMount(async () => {
		$store.modal = new Web3Modal({
			network,
			cacheProvider,
			providerOptions: {
				walletconnect: {
					package: WalletConnectProvider,
					options: {
						infuraId: import.meta.env.VITE_INFURA_ID
					}
				}
			}
		});

		if ($store.modal.cachedProvider) {
			await connect();
		}
	});

	export async function connect() {
		$store.connecting = true;
		$store.provider = await $store.modal.connect();
		$store.web3 = new ethers.providers.Web3Provider($store.provider);
		await getAddress();
		$store.connecting = false;
	}

	export async function getAddress() {
		const accounts = await $store.web3.listAccounts();
		if (accounts) {
			$store.address = accounts[0];
			$store.displayName = await $store.web3.lookupAddress($store.address);
			if ($store.displayName) $store.avatar = await $store.web3.getAvatar($store.displayName);
			$store.balanceRaw = await $store.web3.getBalance($store.address);
			$store.balance = ethers.utils.formatEther($store.balanceRaw);
		}
	}
</script>

<slot
	{connect}
	{store}
	address={$store.address}
	avatar={$store.avatar}
	balance={$store.balance}
	displayName={$store.displayName}
	connecting={$store.connecting}
	web3={$store.web3}
/>
