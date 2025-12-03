<script>
  import { createEventDispatcher } from 'svelte';
  export let show = false;
  export let lyrics = "";
  export let songUrl = "";
  export let title = "";

  const dispatch = createEventDispatcher();

  let audioRef;
  let fontSize = 17; // Default from your JS
  let isProjectorMode = false;

  function closePopup() {
    if(audioRef) audioRef.pause();
    dispatch('close');
    isProjectorMode = false;
    fontSize = 17;
  }

  function toggleProjector() {
    isProjectorMode = true;
    fontSize = 40; // From your JS
  }

  function closeProjector() {
    isProjectorMode = false;
    fontSize = 17; // Reset
  }
</script>

{#if show}
<div class="song_popup" style="display: block;">
  <div class="deliveryOverlay" on:click={closePopup}></div>
  
  {#if !isProjectorMode}
    <div class="song_pop_close" on:click={closePopup}>x</div>
  {/if}

  <div class="inner_background_pop">
    <center>
      <div class="{isProjectorMode ? 'col-md-12' : 'col-md-8'} music_popup">
        <div class="music-bg">
          
          <div class="music_box_contral">
            <div class="music_pro">
              <div class="font_control">
                {#if isProjectorMode}
                  <div class="sild_controler" style="display: block;">
                    <div class="slid_cont_head"><b>Font Size:</b></div>
                    <div class="slid_cont_contaler">
                      <p style="font-size:18px; margin-top: 6px;">12px</p>
                      <input type="range" min="12" max="65" bind:value={fontSize} id="font_control" />
                      <p style="font-size:18px; margin-top: 6px;">65px</p>
                    </div>
                  </div>
                  <div class="projector_close" style="display: block;" on:click={closeProjector}>X</div>
                {:else}
                  <img class="projector_mode" src="/images/projector_black.png" alt="Projector Mode" on:click={toggleProjector}/>
                {/if}
              </div>
            </div>
          </div>

          <div class="lyrics">
            <div class="music-single {isProjectorMode ? 'music_pad' : ''}" 
                 style="font-size: {fontSize}px; max-height: {isProjectorMode ? '65vh' : '70vh'};">
              {@html lyrics} 
            </div>
            
            <audio bind:this={audioRef} class="audio" id="audio" controls autoplay src={songUrl}>
              Your browser does not support the audio element.
            </audio>
          </div>

        </div>
      </div>
    </center>
  </div>
</div>
{/if}

<style>
/* CSS from sanskrit.css for popup */
.song_popup { position: fixed; top: 0; bottom: 0; right: 0; left: 0; z-index: 9999; }
.deliveryOverlay { position: absolute; width: 100%; height: 100%; background-color: rgba(0, 0, 0, 0.7); }
.music_popup { position: absolute; z-index: 999; top: 50%; left: 50%; transform: translate(-50%, -50%); }
.music-bg { width: 100%; background-color: #fad4b3; border-radius: 20px; float: left; }
.song_pop_close { position: absolute; font-size: 35px; right: 30px; top:10px; cursor: pointer; color: #fff; z-index: 10000; }
.lyrics { background-color: #fad4b3ed; border-radius: 20px; width: 100%; float:left;}
.music-single { padding: 1em 7em; overflow: auto; text-align: center; color: #3E4939; font-family: 'Noto Sans Devanagari'; white-space: pre-line; }
.music_pad { padding: 1em 4em; }
.audio { width: 100%; outline: none; padding: 10px; border-radius: 30px; margin-top: 10px; }
.projector_mode { float: right; width: 30px; margin: 10px 20px 0 0; cursor: pointer; }
.projector_close { float: right; font-size: 24px; cursor: pointer; margin-right: 20px; font-weight: bold;}
.sild_controler { width: 90%; float: left; padding: 0 5%; }
.slid_cont_head { float: left; font-size: 16px; font-weight: bold; margin-right: 10px;}
.slid_cont_contaler { display: flex; align-items: center; justify-content: center; }
input[type=range] { width: 60%; margin: 0 10px; }
</style>