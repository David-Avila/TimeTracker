<script>
  import Timer from './lib/Timer.svelte'
  let timers = [];
  let cont; 

  loadTimers();

  function addTimer(){
    if (cont === "" || cont === undefined){
      return
    }
    timers.push({
      title: cont,
      milisecs: 0,
      seconds: 0,
      minutes: 0,
      hours: 0,
      id: Math.random() * 1000000000,
    })

    saveTimers();
    timers = timers;
    cont = "";
  }

  function loadTimers() {
    const t = localStorage.getItem('timers');
    if (t != null){
      timers = JSON.parse(t);
    }
  }

  function saveTimers() {
    console.log("Saving");
    localStorage.setItem('timers', JSON.stringify(timers));
  }

  function deleteTimer(id){
    timers = timers.filter(t => t.id != id);
    saveTimers();
  }

</script>

<svelte:head>
  <title>Time Tracker</title>
</svelte:head>


<main class="app">
  <div class="frame">

    <style>
    :root{
      --fontClr: #1c2227;
      --otherClr: #7b7d67;
      --accentColor: #495159;
      --mainColor: #ff8552;
      --middleClr: #f1ffc4;
    }

    body{
      margin: 0;
      padding: 0;
    }
    </style>

    <div class="header">
      <h1 >Time Tracker</h1>
      <div class="ss">
        <input type="text" maxlength="38" bind:value={cont}>
        <button on:click={addTimer}>Add Tracker</button> 
      </div>
    </div>
    <div class="container">
      {#each timers as t}
        <Timer data={t} call={saveTimers} remove={deleteTimer}/>
      {/each}

    </div>
  </div>
</main>

<style>
.app{
  width: 100vw;
  height: 100vh;

  display: flex;
  align-items: center;
  justify-content: center;

  background-color: var(--middleClr);
}

.frame{
  width: 95%;
  height: 95%;

  display: flex;
  align-items: center;
  align-content: start;
  flex-flow: column nowrap;
  text-align: center;

  border-radius: 20px;
  border:4px solid var(--accentColor);
  background-color: var(--middleClr);
  filter: drop-shadow(0 0 32px var(--accentColor));
}

button,
input{
  border-radius: 10px;
  padding: 5px 10px;
  font-weight: 700;
  width: fit-content;
  border: 2px solid var(--fontClr);
  background-color: var(--accentColor);
  transition: all 0.2s ease-in-out;
  box-shadow: 0px 0px var(--accentColor);
}

button:hover {
  transform: translateY(-3px);
  box-shadow: 0px 3px var(--accentColor);
}

input{
  width: 150px;

}

.header{
  height: fit-content;
  width: 100%;
  text-align: center;
  border-radius: 15px 15px 0 0;
  padding-bottom: 20px;
  border:none;
  border-bottom: 4px solid var(--accentColor);

  background-color: var(--mainColor);
  color: var(--fontClr);
}

.container{
  width: 100%;
  height: fit-content;
  top: 20%;
  overflow: hidden;
  overflow-y: scroll;

  display: flex;
  align-items: center;
  justify-content: center;
  flex-flow: row wrap;

  gap: 20px;
  padding: 20px;
}

</style>
















