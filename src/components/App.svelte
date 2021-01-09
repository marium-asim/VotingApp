<script>
   import Header from './Header.svelte';
   import Footer from './Footer.svelte';
    import PollList from './PollList.svelte';
   import CreatePollForm from './CreatePollForm.svelte';
 
    import Tabs from '../shared/Tabs.svelte';

   //tabs
   let items =['Current Polls', 'Add New Poll'];
   let activeItem ='Current Polls';

   const tabChange = (e) => {
	   activeItem = e.detail;
   }
  

   const handleAdd = (e) =>
   {
	   activeItem = 'Current Polls';
	   
   };

</script>

<Header />
<main>
	<Tabs {activeItem} {items}  on:tabChange={tabChange}   />
	{#if activeItem === 'Current Polls'}
	<PollList  /> 
	{:else if activeItem === 'Add New Poll'}
	<CreatePollForm on:add={handleAdd} />
	{/if}
</main>
<Footer />
<style>
	main {
		max-width: 960 px;
		margin:40px auto;
	}



</style>