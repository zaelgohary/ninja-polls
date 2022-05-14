<script>
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte'
	import Tabs from './shared/Tabs.svelte'
	import CreatePollForm from './components/CreatePollForm.svelte'
	import PollList from './components/PollList.svelte'

	let items = ['Current Polls', 'Create a Poll'];
	let activeItem = 'Current Polls'
	
	const tabChange = (e) => {
		activeItem = e.detail
	}

	const handleAdd = () => {
		activeItem = 'Current Polls'
	}

</script>

<Header />

<main>
	<Tabs {items} {activeItem} on:tabChange={tabChange} />
	{#if activeItem === 'Current Polls'}
		<PollList />
	{:else if activeItem === 'Create a Poll'} 
		<CreatePollForm on:add={handleAdd} />
	{/if}
</main>

<Footer />

<style>

main{
	width: 100%;
	max-width: 960px;
	margin: 40px auto;
}


</style>