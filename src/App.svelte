<script>
  import Header from './lib/Header.svelte';
  import GitaPage from './lib/GitaPage.svelte';
  import Footer from './lib/Footer.svelte';
  import { onMount } from 'svelte';

  let showScrollTop = false;

  onMount(() => {
    const handleScroll = () => {
      showScrollTop = window.scrollY > 300;
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  });
</script>

<main>
  <Header />
  <GitaPage />
  <Footer />
</main>

{#if showScrollTop}
  <button id="return-to-top" on:click={() => window.scrollTo({top:0, behavior:'smooth'})}>
      <i class="fa fa-chevron-up"></i>
  </button>
{/if}

<style>
/* Global Styles from sanskrit.css */
:global(body) {
    margin: 0;
    padding: 0;
    overflow-x: hidden;
}

#return-to-top {
    position: fixed;
    bottom: 20px;
    right: 20px;
    z-index: 9999;
    background: rgba(62, 73, 57, 0.8);
    width: 50px;
    height: 50px;
    border-radius: 10px;
    border: none;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
}
#return-to-top i { color: #fff; font-size: 19px; position: relative; top: 0; left: 0; }
#return-to-top:hover { background: rgba(62, 73, 57, 0.95); }
</style>