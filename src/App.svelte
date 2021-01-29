<script>
	import Navbar from './Components/Navbar.svelte'
	import Input from './Components/Input.svelte'
	import Profile from './Components/Profile.svelte'
	import Stats from './Components/Stats.svelte'
	
	import { userNameQuery } from './Stores/searchTerm';

	let userData = {}
	let searched = true;
	let userNameQuery_value = '';

	let prof_url = `https://api.chess.com/pub/player/`
	let stats = `https://api.chess.com/pub/player/watch_zero/stats`

	const sub = userNameQuery.subscribe(val => {
		userNameQuery_value = val;
	})

	let toggleSearched = () => {
		searched = !searched
	}
	
	const fetchAll = async () => {
		let profData = await fetch(`${prof_url}${userNameQuery_value}`).then(res => res.json()).catch("no user found")
		let statsData = await fetch(`${prof_url}${userNameQuery_value}/stats`).then(res => res.json()).catch("no user found")
		return {profile: profData, stats: statsData}
	}

</script>

<Navbar />
<main>
	{#if searched}
		<Input toggleSearched={toggleSearched}/>
	{:else}
		{#await fetchAll()}
			<p>Loading the profile...</p>
		{:then chessData}
			{#if chessData.profile.code === 0}
				<h1>User Could Not Be Found</h1>
				<p>Go back, and make sure to enter the username correctly</p>
			{:else}
				{#if chessData.profile.name === undefined}
					<h1>Problem Loading the Profile</h1>
				{:else}
					<Profile 
						name={chessData.profile.name === undefined ? "Account Deleted" : chessData.profile.name} 
						img={chessData.profile.avatar}
						streams={chessData.profile.is_streamer}
					/>
					{#if chessData.stats.fide === 0}
						<h3>No Statistical Data Found</h3>
					{:else}
						<Stats obj={chessData.stats}/>
					{/if}
				{/if}
			{/if}
			<a href="/">
				<h3>Go Back</h3>
			</a>
		{/await}
	{/if}
</main>

<style>
	a{
		color: rgb(255, 255, 255);
	}

	main {
		text-align: center;
		margin: 0 auto;
		padding: 1rem 0;	
	}

	h1, h3, h4, p {
		color: white;
	}
	h3 {
		font-weight: 400;
	}
</style>