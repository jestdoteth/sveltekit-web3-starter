# sveltekit-web3-starter

Everything you need to build a Web3 Svelte project, powered by [`ethers`](https://www.npmjs.com/package/ethers), [`walletconnect`](https://www.npmjs.com/package/@walletconnect/web3-provider), [`web3modal`](https://www.npmjs.com/package/web3modal), and [`create-svelte`](https://github.com/sveltejs/kit/tree/master/packages/create-svelte);

## Getting started
By default, this project expects a walletconnect provider and infura ID.
Before you can run this project locally, you need to create a `.env` file with the following:
```env
VITE_INFURA_ID="<YOUR-INFURA-ID-HERE>"
```
Once present, you can start and build the project like any other [`SvelteKit`](https://kit.svelte.dev/) project

## What's here?

Currently this is just a basic example of a Web3 connector component.
Look at [`src/lib/Web3.svelte`](src/lib/Web3.svelte) and [`src/routes/index.svelte`](src/routes/index.svelte) for more details.

## Future

If this project sees any interest I will continue expanding on the examples, develop some convenience components for tailwind, unocss, etc..., and look into supporting [`svelte-add`](https://github.com/svelte-add/svelte-add) and/or [`degit`](https://github.com/Rich-Harris/degit) or something. Just let me know what you want to see.
