<script>
const plans = {
  5: [
    {gk: 0, f1: 1, f2: 2, d1: 3, d2: 4}, 
    {gk: 0, f1: 1, f2: 2, d1: 3, d2: 4},
    {gk: 2, f1: 3, f2: 4, d1: 0, d2: 1}, 
    {gk: 2, f1: 3, f2: 4, d1: 0, d2: 1}, 
    {gk: 4, f1: 0, f2: 1, d1: 2, d2: 3}, 
    {gk: 4, f1: 0, f2: 1, d1: 2, d2: 3}, 
    {gk: 1, f1: 2, f2: 3, d1: 0, d2: 4}, 
    {gk: 1, f1: 2, f2: 3, d1: 0, d2: 4}
  ], 
  6:[
    {gk: 0, f1: 1, f2: 2, d1: 3, d2: 4, s1: 5},
    {gk: 0, f1: 3, f2: 4, d1: 1, d2: 5, s1: 2},
    {gk: 2, f1: 1, f2: 5, d1: 4, d2: 0, s1: 3},
    {gk: 2, f1: 4, f2: 0, d1: 5, d2: 3, s1: 1},
    {gk: 1, f1: 5, f2: 3, d1: 4, d2: 2, s1: 0},
    {gk: 1, f1: 2, f2: 3, d1: 5, d2: 0, s1: 4},
    {gk: 4, f1: 0, f2: 5, d1: 2, d2: 1, s1: 3},
    {gk: 4, f1: 1, f2: 2, d1: 0, d2: 3, s1: 5},
  ],
  7:[
    {gk:0, f1:1, f2:2, d1:3, d2:4, s1:5, s2:6},
    {gk:0, f1:3, f2:4, d1:5, d2:6, s1:1, s2:2},
    {gk:1, f1:5, f2:6, d1:2, d2:4, s1:0, s2:3},
    {gk:1, f1:2, f2:4, d1:0, d2:3, s1:5, s2:6},
    {gk:5, f1:3, f2:0, d1:2, d2:6, s1:1, s2:4},
    {gk:5, f1:2, f2:6, d1:1, d2:4, s1:0, s2:3},
    {gk:3, f1:1, f2:4, d1:0, d2:6, s1:5, s2:2},
    {gk:3, f1:0, f2:6, d1:5, d2:2, s1:1, s2:4},
  ],
  8:[
    {gk:0, f1:1, f2:2, d1:3, d2:4, s1:5, s2:6, s3:7},
    {gk:0, f1:3, f2:4, d1:5, d2:6, s1:1, s2:2, s3:7},
    {gk:1, f1:5, f2:6, d1:7, d2:2, s1:3, s2:4, s3:0},
    {gk:1, f1:7, f2:2, d1:0, d2:3, s1:5, s2:6, s3:4},
    {gk:4, f1:0, f2:3, d1:5, d2:6, s1:1, s2:2, s3:7},
    {gk:4, f1:5, f2:6, d1:1, d2:7, s1:0, s2:2, s3:3},
    {gk:3, f1:1, f2:7, d1:0, d2:2, s1:5, s2:6, s3:4},
    {gk:3, f1:0, f2:2, d1:5, d2:4, s1:1, s2:7, s3:6},
  ],
  9:[
    {gk:0, f1:1, f2:2, d1:3, d2:4, s1:5, s2:6, s3:7, s4:8},
    {gk:0, f1:5, f2:6, d1:7, d2:8, s1:1, s2:2, s3:3, s4:4},
    {gk:1, f1:2, f2:3, d1:4, d2:5, s1:6, s2:7, s3:8, s4:0},
    {gk:1, f1:6, f2:7, d1:8, d2:0, s1:2, s2:3, s3:4, s4:5},
    {gk:2, f1:3, f2:4, d1:5, d2:6, s1:7, s2:8, s3:0, s4:1},
    {gk:2, f1:7, f2:8, d1:0, d2:1, s1:3, s2:4, s3:5, s4:6},
    {gk:3, f1:4, f2:5, d1:6, d2:7, s1:8, s2:0, s3:1, s4:2},
    {gk:3, f1:8, f2:0, d1:1, d2:2, s1:4, s2:5, s3:6, s4:7},
  ]
}


let numPlayers = 9;
const players = new Array(9).fill('').map((_, i) => 'Player ' + (i + 1));
let stats = {f: {}, d: {}, g: {}, s: {}};
$: {
  if (numPlayers && players) stats = {f: {}, d: {}, g: {}, s: {}};
}

$: sessions = new Array(8).fill(null).map((_, i) => {
  const positions = ({
    time: (i % 4) * 5,
    gk: players[plans[numPlayers][i].gk],
    f1: players[plans[numPlayers][i].f1],
    f2: players[plans[numPlayers][i].f2],
    d1: players[plans[numPlayers][i].d1],
    d2: players[plans[numPlayers][i].d2],
    s1: players[plans[numPlayers][i].s1] ?? '-',
    s2: players[plans[numPlayers][i].s2] ?? '-',
    s3: players[plans[numPlayers][i].s3] ?? "-",
    s4: players[plans[numPlayers][i].s4] ?? '-'
  });

  stats.g[plans[numPlayers][i].gk] = (stats.g[plans[numPlayers][i].gk] || 0) + 1;
  stats.f[plans[numPlayers][i].f1] = (stats.f[plans[numPlayers][i].f1] || 0) + 1;
  stats.f[plans[numPlayers][i].f2] = (stats.f[plans[numPlayers][i].f2] || 0) + 1;
  stats.d[plans[numPlayers][i].d1] = (stats.d[plans[numPlayers][i].d1] || 0) + 1;
  stats.d[plans[numPlayers][i].d2] = (stats.d[plans[numPlayers][i].d2] || 0) + 1;
  stats.s[plans[numPlayers][i].s1] = (stats.s[plans[numPlayers][i].s1] || 0) + 1;
  stats.s[plans[numPlayers][i].s2] = (stats.s[plans[numPlayers][i].s2] || 0) + 1;
  stats.s[plans[numPlayers][i].s3] = (stats.s[plans[numPlayers][i].s3] || 0) + 1;
  stats.s[plans[numPlayers][i].s4] = (stats.s[plans[numPlayers][i].s4] || 0) + 1;

  return positions;
});

</script>

<main>
  <h2 class='team-header'>Team</h2>
  <div class="team">
    <div class="numplayers"><label>Num Players:</label>
      <div class="buttons">
        <button on:click={() => {numPlayers = Math.max(5, numPlayers - 1)}}>⊖</button>
        <strong>{numPlayers}</strong>
        <button on:click={() => {numPlayers = Math.min(9, numPlayers + 1)}}>⊕</button>
      </div>
    </div>

    {#each players as player, i}
      <div>
        <label class="player">Player {i + 1}
          <input type="text" class="player" bind:value={player} disabled={i >= numPlayers && i >= 5} />
        </label>
        <div class="stats">
        {#if i < numPlayers}
          <span>F: {stats.f[i] ?? 0}</span>
          <span>D: {stats.d[i] ?? 0}</span>
          <span>G: {stats.g[i] ?? 0}</span>
          <span>S: {stats.s[i] ?? 0}</span>
          <strong>T: {(stats.f[i] ?? 0) + (stats.d[i] ?? 0) + (stats.g[i] ?? 0) + (stats.s[i] ?? 0)}</strong>
        {:else }&nbsp;
        {/if}
        </div>
      </div>
    {/each}
  </div>

  <h2>Schedule</h2>
  <div class="schedule">
    {#each sessions as session}
      {#if session.time === 0}
        <div class="session header">
          <div class="time">&nbsp;</div>
          <strong class="f">AT</strong>
          <strong class="f">AT</strong>
          <strong class="d">DF</strong>
          <strong class="d">DF</strong>
          <strong class="gk">GK</strong>
          <strong class="sub">SB</strong>
          <strong class="sub">SB</strong>
          <strong class="sub">SB</strong>
          <strong class="sub">SB</strong>
        </div>
      {/if}

      <div class="session players">
        <strong class="time">{session.time}-{session.time + 5}</strong>
        <div class="f">{session.f1}</div>
        <div class="f">{session.f2}</div>
        <div class="d">{session.d1}</div>
        <div class="d">{session.d2}</div>
        <div class="gk">{session.gk}</div>
        <div class="sub">{session.s1}</div>
        <div class="sub">{session.s2}</div>
        <div class="sub">{session.s3}</div>
        <div class="sub">{session.s4}</div>
      </div>
    {/each}
  </div>
</main>

<style>
  main {
    display: flex;
    gap: 20px;
    flex-direction: column;
  }

  label {
    font-size: 12px;
    font-weight: 600;
  }

  .team {
    display: grid;
    grid-template-columns: repeat(2, 50%);
    gap: 10px;
  }

  .numplayers {
    width: 100%;
    grid-column: 1 / -1;
    display: flex;
    gap: 10px;
    justify-content: center;
    flex-direction:column;
  }

  .buttons {
    display: flex;
    gap: 20px;
    justify-content: center;
  }

  .player {
    width: 100%;
  }

  .stats {
    display: flex;
    justify-content: space-evenly;
  }

  .schedule {
    display: grid;
    width: 100%;
    grid-template-columns: repeat(5, 1fr);
    grid-template-rows: repeat(2, 1fr);
    gap: 10px;
  }

  .session {

  }

  .session * {
    display: block;
  }

  .time {
    margin-bottom: 10px;
  }

  .players .time {
    border-bottom: 1px solid #ccc;
  }

  .gk {
    margin: 10px 0
  }

  @media print {
    .team-header {
      display: none;
    }

    .team {
      display: none;
    }
  }
</style>
