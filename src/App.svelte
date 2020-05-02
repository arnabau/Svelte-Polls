<script>
  import Header from './components/Header.svelte';
  import Footer from './components/Footer.svelte';
  import PollList from './components/PollList.svelte';
  import CreatePollForm from './components/CreatePollForm.svelte';
  import Tabs from './shared/Tabs.svelte';

  // Tabs
  let items = ['Current Polls', 'Add new poll'];
  let activeItem = 'Current Polls';

  const tabChange = e => {
    activeItem = e.detail;
  };

  const handleAdd = e => {
    activeItem = 'Current Polls';
  };
</script>

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>

<Header />
<main>
  <Tabs {activeItem} {items} on:tabChange={tabChange} />
  {#if activeItem === 'Current Polls'}
    <PollList />
  {:else if activeItem === 'Add new poll'}
    <CreatePollForm on:add={handleAdd} />
  {/if}
</main>
<Footer />
