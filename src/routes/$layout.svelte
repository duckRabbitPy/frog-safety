<script>
	// import global css from src
	import "/src/global.css";
	import Footer from "/src/lib/Footer.svelte";

	let main = true;

	function mainActive(){
		main = true
	}

	function tipsActive(){
		main = false
	}

</script>

<style>

nav {
	color: black;
	font-size: x-large;
	display: flex;
	justify-content: flex-end;
	padding-right: 5%;

	}

a {
	text-decoration: none;
	color: black;
}

button {
	font-size: x-large;
	margin: 0.5rem;
}

.active{
	background-color: rgb(195, 255, 195);
}

.inactive {
	background-color: lightgrey;
}


img {
	height: 200px;
	margin-left: 20px;
}

@media screen and (max-width: 500px){
	button {
	font-size: medium;
	margin: 0.5rem;}

	img {height: 150px}

}

</style>


<nav>
    <ul>
    <button class={main ? "active" : "inactive"} on:click={mainActive}><a href=".">Water parameter tool</a></button>
	<button class={main ? "inactive" : "active"} on:click={tipsActive}><a href="tips">Aquarium Tips</a></button>
    </ul>
	<img src="/images/froglogo.png" alt="frog logo">
</nav>

<slot></slot>

<Footer/>