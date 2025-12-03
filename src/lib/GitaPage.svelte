<script>
  import AudioPopup from './AudioPopup.svelte';
  import VerseGrid from './VerseGrid.svelte';

  // State
  let view = 'chapters'; // 'chapters' or 'verses'
  let selectedChapter = 1;
  

  // Popup State
  let showPopup = false;
  let currentLyrics = "";
  let currentSong = "";

  function viewChapter(chapter) {
    selectedChapter = chapter;
    view = 'verses';
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }

  function goBack() {
    view = 'chapters';
  }

  function handlePlay(event) {
    const { verse } = event.detail;
    // Mock data for audio
    currentLyrics = verse === 'whole' ? 'Full chapter audio...' : 
                    verse === 'end' ? 'Ending...' : 
                    `Verse ${verse} Sanskrit text here...`;
    currentSong = verse === 'whole' ? '/audio/chapter_full.mp3' :
                  verse === 'end' ? '/audio/end.mp3' :
                  `/audio/verse_${verse}.mp3`;
    showPopup = true;
  }

</script>

<div class="inner_background inner-pad" style="background-image: url('/images/gita_banner.png'); background-size: cover; background-position: top center; background-attachment: scroll; padding-bottom: 0;">
  <h1 class="inner_head">BHAGAVAD GITA</h1>
  <div class="container border_bg hero-container16" style="margin-bottom: 0;">
  </div>
</div>

<div class="inner_background shlok_inner" style="z-index: 1; margin-top: 0; padding-top: 0; background-image: url('/images/pic1.jpg'); background-size: cover; background-position: center center; background-attachment: fixed;">
  <div class="book_img" style="position: relative; top: -20px; margin-bottom: -150px; z-index: 999;">
    <img src="/images/gita_open.png" alt="Gita Book">
  </div>
  
  {#if view === 'chapters'}
    <section class="chapter_main" style="margin-top: 0; padding-top: 0; background: transparent;">
        <div class="chapter_head">
            <p>GITA CHAPTERS</p>
        </div>
        <div class="chapter_container">
            {#each Array(18) as _, i}
                <div class="chapter" on:click={() => viewChapter(i + 1)}>
                    <div class="chapter_img">
                        <img src="/images/gita_book.jpg" alt="Chapter {i+1}">
                    </div>
                    <div class="chapter_num">
                        <p>{i + 1}</p>
                    </div>
                </div>
            {/each}
        </div>
    </section>
  {/if}

  {#if view === 'verses'}
    <section class="chapter_main" style="background-image: url('/images/pic1.jpg'); background-size: cover; background-position: center center; background-attachment: fixed; padding-top: 3rem; padding-bottom: 4rem;">
      <VerseGrid 
        chapterNumber={selectedChapter} 
        on:back={goBack}
        on:play={handlePlay}
      />
    </section>
  {/if}
</div>

<AudioPopup 
  show={showPopup} 
  lyrics={currentLyrics} 
  songUrl={currentSong} 
  on:close={() => showPopup = false} 
/>

<style>
/* CSS from sanskrit.css specific to Gita Page */

/* Banner */
.inner_background { background: url(/images/inner_background.jpeg) fixed top center no-repeat; width: 100%; position: relative; float: left; min-height: 35em; background-size: cover; transform: translate(0px, 0px);}
.inner-pad { padding: 8em 0 0em 0; margin-bottom: 0; }
.inner_head { font-size: 7em; color: #3E4939; padding-bottom: 10px; margin-bottom: -.75em; text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25); justify-content: center; display: flex; position: inherit; z-index: 1; background-color: #ffffffa3; }
.hero-container16 { background: url("/images/background_bhagwat_geeta.jpg") center center /cover; height: 25em; position: relative; margin-bottom: 0; z-index: 99999; }
.book_img { width: 18%; position: absolute; top: 87%; left: 50%; transform: translate(-50%, -50%); z-index: 999999; pointer-events: none; }
.book_img img { width: 100%; }

/* Chapter Grid */
.chapter_main { 
    width: 100%; 
    float: left; 
    padding-top: 2em; 
    padding-bottom: 4em; 
    position: relative; 
    z-index: 1; 
}
.chapter_head p { text-align: center; padding: 1em 0em; font-size: 24px; color: #bd003c; letter-spacing: 1px; position: relative; font-weight: bold; text-decoration: underline;}
.chapter_container { 
    padding: 0em 6em;
    display: grid;
    grid-template-columns: repeat(5, 147px);
    grid-gap: 125px 190px;
    justify-content: center;
}

/* The Diamond Shape Logic */
.chapter {
    width: 180px;
    height: 180px;
    overflow: hidden;
    border: 1px solid #928c8c;
    position: relative;
    transform: rotate(45deg); /* Diamond shape */
    border-radius: 15px;
    margin: 0;
    cursor: pointer;
    background: #fff;
}
.chapter:hover { transform: rotate(45deg); }

.chapter_img {
    width: 362px;
    height: 336px;
    transform: rotate(-45deg); /* Counter rotate image */
    position: absolute;
    top: -60px;
    left: -38px;
}
.chapter_img img { width: 100%; }

.chapter_num {
    position: absolute;
    background-color: #352c2cad;
    width: 258px;
    height: 40px;
    transform: rotate(-46deg); /* Counter rotate text strip */
    top: 36%;
    left: -41%;
    display: flex;
    justify-content: center;
    align-items: center;
}
.chapter_num p { 
    color: #fff; 
    text-align: center;
    font-size: 24px; 
    line-height: 18px;
    padding-top: 11px;
    padding-left: 2em;
    padding-right: 2em;
    margin: 0; 
}

/* Verse List / Shlokas */
.shlok_inner { padding: 0; min-height: 100vh; background: #f5f4f0; }
.shlok { width: 100%; padding-top: 2em; padding-bottom: 4em; animation: fadeIn 0.5s; }
.shlok_main { max-width: 1100px; margin: 0 auto; padding: 2rem; text-align: center; }
.breadcrumb { text-align: left; margin-bottom: 1rem; }
.back_chapter { 
    background: none;
    color: #bd003c;
    font-weight: bold;
    font-size: 0.9rem;
    text-decoration: underline;
    border: none;
    cursor: pointer;
    padding: 0;
    margin: 0;
}
.back_chapter:hover {
    color: #8a002a;
}
.shlok_head p { 
    color: #bd003c;
    font-size: 1.8rem;
    border-bottom: 2px solid #bd003c;
    display: inline-block;
    padding-bottom: 5px;
    margin-bottom: 1.5rem;
    text-align: center;
    text-transform: uppercase;
    font-weight: bold;
}
.shlok_head { text-align: center; margin-bottom: 20px;}

.shlok_sort { 
    border-top: 1px solid #bd003c;
    border-bottom: 1px solid #bd003c;
    padding: 0.5rem 2rem;
    text-align: left;
    margin-bottom: 2rem;
    background: rgba(189, 0, 60, 0.05);
}
.shlok_h p { 
    margin: 0;
    color: #bd003c;
    font-weight: bold;
    font-size: 15px;
}

.shlok_container { display: flex; justify-content: center; width: 100%; }
.shlok_area { 
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 2rem 1rem;
    justify-items: center;
    width: 100%;
}

/* Scroll Items */
.shlok_img {
    background-image: url('/images/gita_book.jpg');
    background-size: 100% 100%;
    background-repeat: no-repeat;
    width: 130px;
    height: 180px;
    position: relative;
    cursor: pointer;
    transition: transform 0.2s;
    filter: drop-shadow(0 5px 5px rgba(0,0,0,0.2));
    display: flex;
    align-items: center;
    justify-content: center;
}
.shlok_img:hover { transform: translateY(-5px); }
.shlok_img > img { 
    display: none;
}

.shlok_num {
    position: absolute;
    top: 35%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100%;
    text-align: center;
}
.shlok_num p { 
    color: #4a3b2a;
    font-size: 1.5rem;
    font-weight: bold;
    line-height: 1.1;
    margin: 0;
    font-family: serif;
}

.shlok_play {
    position: absolute;
    bottom: 30%;
    left: 50%;
    transform: translateX(-50%);
}
.shlok_play i { 
    font-size: 35px;
    color: #8b4513;
    filter: drop-shadow(0 2px 2px rgba(0,0,0,0.3));
}

@keyframes fadeIn { from { opacity:0; } to { opacity:1; } }
</style>