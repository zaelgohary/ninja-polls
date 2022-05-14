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

	let polls =[
    {
      id: 1,
      question: 'Python or JavaScript?',
      answerA: 'Python',
      answerB: 'JavaScript',
      votesA: 9,
      votesB: 15,
    },
	]
	const handleAdd = (e) => {
		const poll = e.detail
		polls = [poll, ...polls]
		activeItem = 'Current Polls'
		console.log(polls);
	}

	const handleVote = (e) => {
		console.log(e.detail);
		const {id, option} = e.detail
		let copiedPolls = [...polls]
		let upvotedPoll = copiedPolls.find((poll)=> poll.id == id)
		
		if(option === 'a'){
			upvotedPoll.votesA ++
		}

		if(option === 'b'){
			upvotedPoll.votesB++
		}

		polls = copiedPolls
	}
</script>

<Header />

<main>
	<Tabs {items} {activeItem} on:tabChange={tabChange} />
	{#if activeItem === 'Current Polls'}
		<PollList {polls} on:vote={handleVote} />
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