<script>
  let clicks = 100;
  let multiplier = 1;
  let workers = [];
  let worker_multiplier = 1;

  let upgrades = [
    { cost: 15, name: "Doubler", multiplier: 2, worker: 0 },
    { cost: 5, name: "Workers", multiplier: 2, worker: 1 },
  ];

  function increment() {
    clicks = clicks + worker_multiplier;
    console.log("click" + clicks);
  }

  let bettergame = false;
</script>

<article>
  {#if bettergame}
    <div>BETTER GAME</div>
    <iframe src="https://gurka.se/" frameborder="0"></iframe>
    <button on:click={()=>{bettergame = !bettergame}}> Klicka här för att gå tillbaka </button>

  {:else}
    <header>
      <div class="grid">
        {#each upgrades as upgrade}
          <button
            class="upgrade"
            on:click={() => {
              if (clicks >= upgrade.cost * worker_multiplier) {
                clicks -= upgrade.cost * worker_multiplier;

                if (upgrade.multiplier) {
                  worker_multiplier = worker_multiplier * upgrade.multiplier;
                }

                if (upgrade.worker && clicks) {
                  workers = [upgrade.name, ...workers];
                  /* start "clicking" every 1000 ms */
                  setInterval(increment, 1000);
                }
              } else {
                alert("sluta spela detta spel");
              }
            }}
          >
            <span>{upgrade.name}</span>
            <span>{upgrade.cost * worker_multiplier}</span>
          </button>
        {/each}
      </div>
    </header>
    <div class="game">
      <button on:click={increment} class="clicker">
        <span class="clicks">{clicks}</span>
        <span class="pointtext">PPC: {worker_multiplier}</span>
      </button>
    </div>

      <button on:click={()=>{bettergame = !bettergame}}> Klicka här för att spela ett bättre spel </button>

    <footer>
      <div class="panelright">
        <div>
          <span>Workers</span>
          <hr />
          <div class="shop">
            {#each workers as worker}
              <div class="worker">{worker}</div>
            {/each}
          </div>
        </div>
        <hr />
      </div>
    </footer>
  {/if}
</article>

<style>

  iframe{
    width: 100%;
    height: 60vh;
  }

  .shop {
    display: grid;
    grid-auto-flow: row; /* default */
    gap: 8px;
    grid-template-rows: repeat(3, 1fr);
    grid-template-columns: repeat(3, 1fr);
  }

  .upgrade {
    width: 100%;
    height: 100%;
    border: 4px solid rgb(0, 0, 0);
    background-color: rgb(59, 183, 28);
    background-image: url("https://swall.teahub.io/photos/small/2-21651_nebula-space-wallpaper-orange-and-blue-space.jpg");
    place-items: center;
    place-content: center;
    display: flex;
    flex-direction: column;
    background-size: 100%;
    background-position: 0px -29px;
  }

  .worker {
    width: 100%;
    height: 100%;
    border: 1px solid black;
    background-color: rgb(128, 141, 27);
    place-items: center;
    place-content: center;
    display: flex;
  }

  .game {
    height: 50vh;
    display: flex;
    flex-direction: column;
    place-items: center;
    place-content: center;
  }
  .clicker {
    clip-path: circle();
    display: flex;
    height: 100%;
    width: 100%;
    flex-direction: column;
    place-items: center;
    place-content: center;
    background-image: url("https://e0.pxfuel.com/wallpapers/757/616/desktop-wallpaper-applejack-my-little-pony-friendship-is-magic.jpg");
    background-size: 60%;
    background-position: 230px -5px;
  }

  .panelright {
    height: 100%;
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .clicks {
    font-size: 100px;
    color: rgb(0, 0, 0);
  }

  .pointtext {
    color: rgb(0, 0, 0);
    font-size: 25px;
    font-weight: bold;
  }

  article {
    background-image: url("https://swall.teahub.io/photos/small/2-21651_nebula-space-wallpaper-orange-and-blue-space.jpg");
    background-size: 100%;
    background-position: 0px -500px;
  }

  header {
    background-image: url("https://img.archiexpo.com/images_ae/photo-mg/3852-17555356.jpg");
    background-size: 100%;
    background-position: -1px -50px;
  }

  footer {
    background-image: url("https://img.archiexpo.com/images_ae/photo-mg/3852-17555356.jpg");
    background-size: 100%;
    background-position: -1px -1px;
  }

  div {
    background-image: url("https://swall.teahub.io/photos/small/2-21651_nebula-space-wallpaper-orange-and-blue-space.jpg");
    background-size: 100%;
    background-position: -1px -1px;
  }
</style>
