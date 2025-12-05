<!-- <script>
  import { createEventDispatcher } from 'svelte';
  export let chapterNumber = 1;
  
  const dispatch = createEventDispatcher();
  
  // Creates array [1, 2, ... 47]
  let verses = Array.from({ length: 47 }, (_, i) => i + 1);

  function playVerse(verse) {
    dispatch('play', { verse });
  }
</script>

<div class="container">
  <div class="breadcrumb">
    <button on:click={() => dispatch('back')}>&lt; Back</button>
  </div>

  <h2 class="chapter-title">CHAPTER {chapterNumber}</h2>
  
  <div class="tabs-line">
    <div class="tab">Verse</div>
  </div>

  <div class="grid">
    <div class="scroll-item" on:click={() => playVerse('whole')} role="button" tabindex="0">
      <div class="scroll-content">
        <span class="label text-bold">Whole<br>Chapter</span>
        <div class="play-icon">
          <i class="fa fa-play-circle"></i>
        </div>
      </div>
    </div>

    {#each verses as verse}
      <div class="scroll-item" on:click={() => playVerse(verse)} role="button" tabindex="0">
        <div class="scroll-content">
          <span class="label">{verse}</span>
          <div class="play-icon">
            <i class="fa fa-play-circle"></i>
          </div>
        </div>
      </div>
    {/each}

    <div class="scroll-item" on:click={() => playVerse('end')} role="button" tabindex="0">
      <div class="scroll-content">
        <span class="label text-bold">End of<br>Chapter</span>
        <div class="play-icon">
          <i class="fa fa-play-circle"></i>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  .container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 2rem;
    text-align: center;
  }

  .breadcrumb button {
    text-decoration: underline;
    color: #bd003c;
    cursor: pointer;
    padding-left: 5%;
    background: none;
    border: none;
    font-weight: bold;
    font-size: 0.9rem;
    float: left;
  }

  .chapter-title {
    color: var(--primary-burgundy);
    font-size: 1.8rem;
    border-bottom: 2px solid var(--primary-burgundy);
    display: inline-block;
    padding-bottom: 5px;
    margin-bottom: 1.5rem;
    text-transform: uppercase;
  }

  .tabs-line {
    border-top: 1px solid var(--primary-burgundy);
    border-bottom: 1px solid var(--primary-burgundy);
    padding: 0.5rem 2rem;
    text-align: left;
    margin-bottom: 2rem;
    background: rgba(153, 27, 27, 0.05);
    color: var(--primary-burgundy);
    font-weight: bold;
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 2rem 1rem;
    justify-items: center;
  }

  .scroll-item {
    background-image: url('/images/scroll_bg.png');
    background-size: 100% 100%;
    background-repeat: no-repeat;
    width: 130px; 
    height: 180px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: transform 0.2s;
    filter: drop-shadow(0 5px 5px rgba(0,0,0,0.2));
  }

  .scroll-item:hover {
    transform: translateY(-5px);
  }

  .scroll-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 10px;
    padding-top: 10px;
  }

  .label {
    font-size: 1.5rem;
    color: #4a3b2a;
    font-family: serif;
    line-height: 1.1;
  }
  
  .text-bold {
    font-weight: bold;
  }

  .play-icon {
    font-size: 2rem;
    color: #8b0000;
  }

  .play-icon i {
    cursor: pointer;
  }

  .play-icon i:hover {
    color: #a00000;
  }
</style> -->

<script>
  import { createEventDispatcher, onMount } from 'svelte';
  export let chapterNumber = 1;
  
  const dispatch = createEventDispatcher();
  
  let verses = [];
  let loading = true;
  let error = null;

  // Fetch verses from API when component mounts or chapter changes
  async function fetchVerses() {
    loading = true;
    error = null;
    try {
      // Use proxy to avoid CORS issues
      const response = await fetch(`/api/geeta.php?q=${chapterNumber}`);
      if (!response.ok) {
        throw new Error('Failed to fetch verses');
      }
      const result = await response.json();
      
      // API returns: {"status":200,"message":"Data Listed","data":[...]}
      if (result.status === 200 && result.data && Array.isArray(result.data)) {
        // Filter verses with shlok_no > 0 (exclude chapter intro at shlok_no=0)
        // Also exclude shlok_no=99 which appears to be an end marker in the API data
        const verseData = result.data.filter(item => {
          const verseNum = parseInt(item.shlok_no);
          return item.shlok_no && verseNum > 0 && verseNum < 99;
        });
        // Get unique verse numbers
        const uniqueVerses = [...new Set(verseData.map(item => parseInt(item.shlok_no)))].sort((a, b) => a - b);
        verses = uniqueVerses;
        console.log(`Loaded ${verses.length} verses for chapter ${chapterNumber}`);
      } else {
        throw new Error('Invalid API response format');
      }
    } catch (err) {
      console.error('Error fetching verses:', err);
      error = err.message;
      // Fallback to default verse counts if API fails
      const verseCountPerChapter = [47, 72, 43, 42, 29, 47, 30, 28, 34, 42, 55, 20, 34, 27, 20, 24, 28, 78];
      const verseCount = verseCountPerChapter[chapterNumber - 1] || 47;
      verses = Array.from({ length: verseCount }, (_, i) => i + 1);
    } finally {
      loading = false;
    }
  }

  onMount(() => {
    fetchVerses();
  });

  // Refetch when chapter changes
  $: if (chapterNumber) {
    fetchVerses();
  }

  function playVerse(verse) {
    dispatch('play', { verse, chapterNumber });
  }
</script>

<div class="shlok_main">
  <div class="back_chapter" on:click={() => dispatch('back')} role="button" tabindex="0">
    &lt; Back
  </div>

  <div class="shlok_head">
    <p>CHAPTER {chapterNumber}</p>
  </div>
  
  <div class="shlok_sort">
    <div class="shlok_h">
      <p>Verse</p>
    </div>
  </div>

  {#if loading}
    <div class="loading-message">Loading verses...</div>
  {:else if error}
    <div class="error-message">Error loading verses. Showing default layout.</div>
  {/if}

  <div class="shlok_container">
    <div class="shlok_area">
        <div class="shlok_img" on:click={() => playVerse('whole')} role="button" tabindex="0">
            <img src="/images/scroll_bg.png" alt="Scroll Background">
            <div class="shlok_num">
                <p>Whole<br>Chapter</p>
            </div>
            <div class="shlok_play">
                <img src="/images/play_button.png" alt="Play Button">
            </div>
        </div>

        {#each verses as verse}
            <div class="shlok_img" on:click={() => playVerse(verse)} role="button" tabindex="0">
                <img src="/images/scroll_bg.png" alt="Scroll Background">
                <div class="shlok_num">
                    <p>{verse}</p>
                </div>
                <div class="shlok_play">
                    <img src="/images/play_button.png" alt="Play Button">
                </div>
            </div>
        {/each}

        <div class="shlok_img" on:click={() => playVerse('end')} role="button" tabindex="0">
            <img src="/images/scroll_bg.png" alt="Scroll Background">
            <div class="shlok_num">
                <p>End of<br>Chapter</p>
            </div>
            <div class="shlok_play">
                <img src="/images/play_button.png" alt="Play Button">
            </div>
        </div>
    </div>
  </div>
</div>

<style>
  .shlok_main {
    width: 100%;
    float: left;
    padding-bottom: 3em; /* Added padding for breathing room */
  }

  /* Back Button */
  .back_chapter {
    text-decoration: underline;
    color: #bd003c;
    cursor: pointer;
    padding-left: 5%;
    font-size: 16px; 
    margin-bottom: 10px;
  }

  /* Chapter Title */
  .shlok_head p {
    text-align: center;
    padding: 1em 0em;
    font-size: 24px;
    color: #bd003c;
    font-weight: 500;
    letter-spacing: 1px;
    position: relative;
    margin: 0;
    text-transform: uppercase;
  }

  .shlok_head p::after {
    content: '';
    width: 9%;
    height: 2px;
    background-color: #bd003c;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: 50%;
    margin-top: 18px;
  }

  /* Sort Bar */
  .shlok_sort {
    width: 100%;
    position: relative;
    margin-bottom: 2em;
    border-top: 1px solid #bd003c;
    border-bottom: 1px solid #bd003c;
    background-color: rgba(189, 0, 60, 0.05);
  }

  .shlok_h p {
    padding: 1em 0;
    margin-left: 10%;
    color: #bd003c;
    letter-spacing: 1px;
    font-size: 15px;
    font-weight: bold;
    margin-bottom: 0;
  }

  /* Container */
  .shlok_container {
    width: 100%;
    float: left;
    position: relative;
  }

  .shlok_area {
    width: 100%;
    float: left;
    margin-top: 2em;
    margin-bottom: 2em;
    /* Use standard flow instead of flex to match 'float: left' behavior precisely if preferred, 
       but flex wrap usually behaves better responsively. 
       We will use block flow with floats to exactly match the CSS provided. */
    display: block; 
  }

  /* THE SCROLL ITEM - Exact CSS match */
  .shlok_img {
    width: 12%; /* Matches sanskrit.css line 1184 */
    float: left;
    margin-left: 6.5%; /* Matches sanskrit.css line 1186 */
    position: relative;
    cursor: pointer;
    margin-bottom: 30px; /* Vertical spacing */
    transition: transform 0.2s;
  }

  .shlok_img:hover {
    transform: translateY(-5px);
  }

  .shlok_img img {
    width: 100%;
    display: block;
  }

  /* Number Overlay */
  .shlok_num {
    position: absolute;
    background-color: transparent;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 78%;
    height: 68%;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .shlok_num p {
    color: #4a3b2a; /* Brown text color */
    font-size: 23px; /* Matches sanskrit.css line 1202 */
    font-weight: bold;
    text-align: center;
    margin: 0;
    line-height: 1.2;
    /* Visual tweak to move number slightly up into the paper area */
    margin-bottom: 15px; 
  }

  /* Play Button */
  .shlok_play {
    width: 23%; /* Matches sanskrit.css line 1211 */
    position: absolute;
    top: 75%; /* Matches sanskrit.css line 1213 */
    left: 50%;
    transform: translate(-50%, -50%);
  }

  .shlok_play img {
    width: 100%;
    filter: drop-shadow(0 2px 2px rgba(0,0,0,0.2));
  }

  /* Responsive Adjustments based on your CSS file */
  @media only screen and (max-width: 992px) {
    .shlok_img {
        width: 17%; /* Larger scrolls on tablets */
    }
  }

  @media only screen and (max-width: 768px) {
    .shlok_img {
        width: 30%; /* Much larger on mobile */
        margin-left: 15%; /* Centered spacing */
    }
    .shlok_num p {
        font-size: 30px;
    }
  }

  /* Loading and Error Messages */
  .loading-message,
  .error-message {
    text-align: center;
    padding: 2rem;
    font-size: 1.2rem;
    color: #bd003c;
  }

  .error-message {
    color: #d9534f;
  }
</style>