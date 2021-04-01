<script>
import { blur, fly } from 'svelte/transition';

let ammonia = true;
let nitrite = false;
let nitrate = false;

let results = [];
let waterCondition;

let ammoniaRes;
let nitriteRes;
let nitrateRes;

let chemical = "ammonia";
let action;
let nitrateMessage;
let flag;

let condition;

function calculateAction(ammoniaRes, nitriteRes, nitrateRes) {
  if (nitrateRes >= 40) {
    nitrateMessage =
      "Consider a 25-30% water change twice a week as nitrates are on the high side";
  } else if (nitrateRes > 0) {
    nitrateMessage = "Nitrates are good, continue weekly 25-30% water change";
  } else {
    nitrateMessage = "With nitrate that low your tank could be uncycled";
  }

  if (ammoniaRes === 4 || nitriteRes === 4) {
    flag = greaterRisk(ammoniaRes, nitriteRes);
    waterCondition = "High risk";
    action = `30% water change, treat water with triple dose of Seachem Prime daily for at least 3 days to protect your frogs from the ${flag}, test again TOMORROW, then input your updated water values and follow the lastest recommendation`;
  } else if (ammoniaRes === 2 || nitriteRes === 2) {
    flag = greaterRisk(ammoniaRes, nitriteRes);
    waterCondition = "Intermediate risk";
    action = `${nitrateMessage}, treat water with double dose of Seachem Prime daily for at least 3 days to protect your frogs from the ${flag}, test again in 1-2 days, then input your updated water values and follow the lastest recommendation`;
  } else if (ammoniaRes > 0 || nitriteRes > 0) {
    flag = greaterRisk(ammoniaRes, nitriteRes);
    waterCondition = "Almost safe";
    action = `${nitrateMessage}, treat water with single dose of Seachem Prime daily for at least 3 days to protect your frogs from the ${flag}, test again this week, then input your updated water values and follow the lastest recommendation`;
  } else if (ammoniaRes === 0 && nitriteRes === 0) {
    if (nitrateRes !== 0) {
      waterCondition = "Safe";
      action = `${nitrateMessage}, ammonia and nitrite are perfect, no need to add Seachem Prime.`;
    } else {
      waterCondition = "Safe";
      action = `${nitrateMessage}, ammonia and nitrite are perfect, no need to add Seachem Prime.`;
    }
  }
}

function greaterRisk(am, ni) {
  if (am > ni) {
    return "Ammonia";
  }
  if (am === ni) {
    return "Ammonia and Nitrite";
  } else {
    return "Nitrite";
  }
}

function scrollToTop() {
  if (window.innerWidth < 500) {
    document.documentElement.scrollTo({
      top: 0,
      behavior: "smooth",
    });
  }
}

function addToResult(newObj) {
  if (newObj["Ammonia"] !== undefined && newObj["Ammonia"] !== null) {
    results = [...results, newObj];
    ammonia = false;
    chemical = "nitrite";
    nitrite = true;
  } else if (newObj["Nitrite"] !== undefined && newObj["Nitrite"] !== null) {
    results = [...results, newObj];
    nitrite = false;
    chemical = "nitrate";
    nitrate = true;
  } else if (newObj["Nitrate"] !== undefined && newObj["Nitrate"] !== null) {
    results = [...results, newObj];
    nitrite = false;
    nitrate = false;

    ammoniaRes = results[0]["Ammonia"];
    nitriteRes = results[1]["Nitrite"];
    nitrateRes = results[2]["Nitrate"];
    calculateAction(ammoniaRes, nitriteRes, nitrateRes);

    if (waterCondition === "Safe") {
      condition = "safeStyle";
    } else if (waterCondition === "Almost safe") {
      condition = "lowStyle";
    } else if (waterCondition === "Intermediate risk") {
      condition = "intermediateStyle";
    } else if (waterCondition === "High risk") {
      condition = "highStyle";
    }

    let finished = document.querySelector(".finished");
    finished.play();
  }

  scrollToTop();
}


    

</script>
<style>
    header {display: flex; justify-content: center;}

    .chemical {color: blue;}

    .card {box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26); padding: 1rem;
      border-radius: 5px;}

    .safeStyle{ background-color: rgba(220, 247, 178, 0.781);}

    .lowStyle{ background-color: rgba(108, 179, 201, 0.863);}

    .intermediateStyle{ background-color: rgb(247, 229, 205);}

    .highStyle{ background-color: rgba(223, 69, 8, 0.507);}

    @media screen and (min-width: 900px){
    .grid-container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 10px 10px;
    margin-left: 5%;
    margin-right: 5%;
    }

    h2 {padding-left: 1rem;}

    img{
        width: 80%;
        padding-left: 10%;
        padding-right: 10%;

    }
    
    img:hover{
        background-color: rgba(27, 221, 255, 0.103);
    }

    .results-grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr;
    gap: 10px 10px;
    margin-left: 5%;
    margin-right: 5%;

    }
    
    }

    @media screen and (min-width: 501px) and (max-width: 899px){
    .grid-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    gap: 10px 10px;
    margin-left: 5%;
    margin-right: 5%;
    }

    h2 {padding-left: 1rem;}

    img{
        width: 80%;
        padding-left: 10%;
        padding-right: 10%;

    }

    img:hover{
        background-color: rgba(27, 221, 255, 0.103);
    }
    
    .results-grid {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    gap: 10px 10px;
    margin-left: 5%;
    margin-right: 5%;


    }}

    @media screen and (max-width: 500px){
    .grid-container {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr 1fr 1fr 1fr 1fr;
    gap: 10px 10px;
    margin-left: 5%;
    margin-right: 5%;
    }

    img{
        width: 80%;
        padding-left: 10%;
        padding-right: 10%;}

    .results-grid {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    gap: 10px 10px;
    margin-left: 5%;
    margin-right: 5%;


    }}


</style>
{#if ammonia}
<h2 in:fly out:fly>This tool is intended as a guide for African Dwarf Frogs and the API freshwater master kit.</h2>
{/if}
{#if ammonia || nitrite || nitrate}
<h2 in:fly out:fly>Select <span class="chemical">{chemical}</span> colour that most closely matches your result: </h2>
{:else}
<h2 in:fly out:fly>Results:</h2>
{/if}
<div in:fly out:fly class="grid-container">
    {#if ammonia}
    <figure out:blur>
        <header>Ammonia 0ppm</header>
        <img on:click={()=>{addToResult({"Ammonia": 0})}}  src="./images/ammonia-0ppm.png" alt="ammonia">
    </figure>

    <figure out:blur>
        <header>Ammonia 0.25ppm</header>
        <img on:click={()=>{addToResult({"Ammonia": 0.25})}} src="./images/ammonia-0.25ppm.png" alt="ammonia">
    </figure>

    <figure out:blur>
        <header>Ammonia 0.5ppm</header>
        <img on:click={()=>{addToResult({"Ammonia": 0.5})}} src="./images/ammonia-0.5ppm.png" alt="ammonia">
    </figure>

    <figure out:blur>
        <header>Ammonia 1ppm</header>
        <img on:click={()=>{addToResult({"Ammonia": 1})}} src="./images/ammonia-1ppm.png" alt="ammonia">
    </figure>

    <figure out:blur>
        <header>Ammonia 2ppm</header>
        <img on:click={()=>{addToResult({"Ammonia": 2})}} src="./images/ammonia-2ppm.png" alt="ammonia">
    </figure>
    <figure out:blur>
        <header>Ammonia 4ppm+ </header>
        <img on:click={()=>{addToResult({"Ammonia": 4})}} src="./images/ammonia-4ppm.png" alt="ammonia">
    </figure>

    {/if}

    {#if nitrite}
    
    <figure out:blur>
        <header>Nitrite 0ppm</header>
        <img on:click={()=>{addToResult({"Nitrite": 0})}} src="./images/nitrite-0ppm.png" alt="nitrite">
    </figure>

  
    <figure out:blur>
        <header>Nitrite 0.25ppm</header>
        <img on:click={()=>{addToResult({"Nitrite": 0.25})}} src="./images/nitrite-0.25ppm.png" alt="nitrite">
    </figure>

    <figure out:blur>
        <header>Nitrite 0.5ppm</header>
        <img on:click={()=>{addToResult({"Nitrite": 0.5})}} src="./images/nitrite-0.5ppm.png" alt="nitrite">
     </figure>

    <figure out:blur>
        <header>Nitrite 1ppm</header>
        <img on:click={()=>{addToResult({"Nitrite": 1})}} src="./images/nitrite-1ppm.png" alt="nitrite">
    </figure>
    
    <figure out:blur>
        <header>Nitrite 2ppm</header>
        <img on:click={()=>{addToResult({"Nitrite": 2})}} src="./images/nitrite-2ppm.png" alt="nitrite">
    </figure>

    <figure out:blur>
        <header>Nitrite 4ppm+</header>
        <img on:click={()=>{addToResult({"Nitrite": 4})}} src="./images/nitrite-4ppm.png" alt="nitrite">
    </figure>
    

    {/if}

    {#if nitrate}
    
    <figure out:blur>
        <header>Nitrate 0ppm</header>
        <img on:click={()=>{addToResult({"Nitrate": 0})}} src="./images/nitrate-0ppm.png" alt="nitrate">
    </figure>

    <figure out:blur>
        <header>Nitrate 5ppm</header>
        <img on:click={()=>{addToResult({"Nitrate": 5})}} src="./images/nitrate-5ppm.png" alt="nitrate">
    </figure>

    <figure out:blur>
        <header>Nitrate 10ppm</header>
        <img on:click={()=>{addToResult({"Nitrate": 10})}} src="./images/nitrate-10ppm.png" alt="nitrate">
    </figure>

    <figure out:blur>
        <header>Nitrate 20ppm</header>
        <img on:click={()=>{addToResult({"Nitrate": 20})}} src="./images/nitrate-20ppm.png" alt="nitrate">
    </figure>

    <figure out:blur>
        <header>Nitrate 40ppm</header>
        <img on:click={()=>{addToResult({"Nitrate": 40})}} src="./images/nitrate-40ppm.png" alt="nitrate">
    </figure>

    <figure out:blur>
        <header>Nitrate 80ppm+</header>
        <img on:click={()=>{addToResult({"Nitrate": 80})}} src="./images/nitrate-80ppm.png" alt="nitrate">
    </figure>
    
    {/if}
    
</div>

{#if !ammonia && !nitrite && !nitrate}
<div class="results-grid">
    <div class="card {condition}">
    <h3><i class="fas fa-tint"></i> Water condition: <br><br>{waterCondition}</h3>
    </div>

    <div class="card">
    <h3><i class="fas fa-biohazard"></i> Parameters:<br><br> Ammonia: {ammoniaRes}ppm <br> Nitrite: {nitriteRes}ppm <br> Nitrate: {nitrateRes}ppm <br>{#if flag} Keep an eye on: <span class="chemical">{flag}</span> {/if}</h3>
    </div> 
    
    <div class="card">
    <h3><i class="fas fa-comment-medical"></i> Recommended action: <br><br>{action} </h3>
    </div>
</div>
{/if}

<!-- svelte-ignore a11y-media-has-caption -->
<audio class="finished" src="./audio/finished.mp3"></audio>