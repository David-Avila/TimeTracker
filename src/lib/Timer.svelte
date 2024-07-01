<script>
  export let data;
  export let call;
  export let remove;
  let running = false;
  let timer = null;


  const start = () => {
    running = true;
    timer = setInterval(() => {
      data.milisecs++;
      if (data.milisecs >= 100){
        data.milisecs = 0;
        data.seconds++;
        if (data.seconds >= 60){
          data.seconds = 0;
          data.minutes++;
          if (data.minutes >= 60){
            data.minutes = 0;
            data.hours++;
          }
        }
      }

    }, 10);
  }

  const stop = () => {
    running = false;
    call();
    clearInterval(timer);
  }

  const btnClicked = () => {
    if (running){
      stop();
    } else {
      start();
    }
  }
</script>

<main class="timer">
  <div class="div1">
    <h3>{data.title}</h3>
    <h3 class="time">{data.hours + ":" + data.minutes + ":" + 
      data.seconds + (data.milisecs < 10 ? ":0" : ":") + data.milisecs}</h3>
  </div>
  <div class="btns">
  <button on:click={btnClicked}>{running ? "Pause" : "Start"}</button>
    <button class="danger"
      on:click={() => {
        stop();
        remove(data.id);
      }}
    >Delete</button>
  </div>
</main>

<style>
.timer{
  width: min(95%, 360px);
  height: 120px;
  color: black;
  border: 2px solid var(--accentColor);
  border-radius: 25px;

  display: flex;
  align-items: center;
  justify-content: space-evenly;
  flex-flow: row wrap;

  color: var(--fontClr);
  background-color: (--otherClr);
}

.div1{
  display: flex;
  align-items: center;
  justify-content: center;
  width: 70%;
  height: 100%;
  flex-flow: column nowrap;
}

.div1 > *{
  margin: 0;
  text-align: left;
  width: max-content;
  word-wrap: break-word;
}

.btns{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-flow: column nowrap;
}

h3{
  max-width: 250px;
  overflow: hidden;
  overflow-x: scroll;
}

button{
  border-radius: 10px;
  padding: 5px 10px;
  margin: 5px;
  width: 84px;
  font-weight: 700;
  border: 2px solid var(--fontClr);
  background-color: var(--accentColor);
  transition: all 0.2s ease-in-out;
  box-shadow: 0px 0px var(--accentColor);
}

button:hover {
  transform: translateY(-3px);
  box-shadow: 0px 3px var(--accentColor);
}

.danger{
  background-color: var(--mainColor);
}

</style>





