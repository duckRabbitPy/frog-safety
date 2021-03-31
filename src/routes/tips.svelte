<script>
    import { fade } from 'svelte/transition';
</script>
<style>

.card {box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26); padding: 1rem;
      border-radius: 5px;}

.card:hover {
    background-color:  rgba(27, 221, 255, 0.103);
}

@media screen and (min-width: 900px){
    .results-grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr;
    gap: 10px 10px;
    margin-top: 5%;
    margin-left: 5%;
    margin-right: 5%;

    }}

    @media screen and (min-width: 501px) and (max-width: 899px){

    .results-grid {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    margin-top: 5%;
    gap: 10px 10px;
    margin-left: 5%;
    margin-right: 5%;


    }}

    @media screen and (max-width: 500px){
  
    .results-grid {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    margin-top: 5%;
    gap: 10px 10px;
    margin-left: 5%;
    margin-right: 5%;


    }}

</style>




<div in:fade class="results-grid">
    <div class="card info">
        <h2><i class="fas fa-arrows-alt"></i> Shake your tests well </h2>
        <p>Carefully read the instructions on the bottles and shake vigorously for accurate results, this is especially the case for nitrate bottle two.</p>
    </div>

    <div class="card info">
    <h2><i class="fas fa-utensils"></i> Clean up left over food</h2>
    <p>Make sure you are not over-feeding your frogs, remove uneaten food straight away so it doesn't have time to collect under ornaments.</p>
    </div> 


    <div class="card info">
        <h2><i class="fas fa-vial"></i> Ensure that your pH is stable</h2>
        <p>African dwarf frogs can adapt to a fairly wide range of pH levels, what is most important is that the pH levels remain stable, it is the swings and crashes that are most dangerous.</p>
    </div>

    <div class="card info">
        <h2><i class="fas fa-microscope"></i> Use bacteria starter when cycling</h2>
        <p>Use Seachem Stability, Tetra SafeStart or equivalent when attempting to cycle your tank, many people find it speeds up the process.</p>
    </div>

    <div class="card info">
        <h2><i class="fas fa-recycle"></i> Keep your tank cycled</h2>
        <p>Make sure that you have a filter that can adequately handle the bioload of your frogs. Avoid massive water changes over 50%, this can crash your cycle. Don't over-clean/rinse your filter, this can also crash your cycle.</p>
    </div>
    
    <div class="card info">
        <h2><i class="fas fa-headset"></i> Ask for help</h2>
        <p>The African Dwarf Frog community has a wealth of experience and can advise on things such as PH swings, cycling, water hardness, infections and tank setup! Check out the facebook group <a href="https://www.facebook.com/groups/159215380775">HERE</a></p>
    </div>

</div>