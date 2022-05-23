<script>

let dificultyVar;
let multi_booleanVar;
let question_amount;
let requestvar = [];
let databaserequester = "";
let data = getData();
// let databaserequester = "https://opendb.com/api.php?amount=";

const handleSubmit = () => {
	requestvar.push(question_amount, dificultyVar, multi_booleanVar,)
	databaserequester = `https://opentdb.com/api.php?amount=`+`${question_amount}`+`&difficulty=`+`${dificultyVar}`+`&type=`+`${multi_booleanVar}`;
	console.log(databaserequester)
	getData()
}

async function getData(){
	const url = databaserequester;
	let resp = await fetch(url);
	let data = await resp.json();
	
	return
}


</script>

<main>
	<header>
		<h1>
			Wellcome to the api-generator quiz!
		</h1>
	</header>
	<section>

		<form on:submit|preventDefault={handleSubmit}>
			<label for="dificulty">Choose dificulty:</label>
  			<select id="dificulty_id" bind:value={dificultyVar}>
    			<option value="easy">easy</option>
    			<option value="medium">meduim</option>
    			<option value="hard">hard</option>
    			</select>	
			
				<label for="multi_boolean">Choose question type:</label>
				<select id="multi_boolean" bind:value={multi_booleanVar}>
				  <option value="multiple">multiple</option>
				  <option value="boolean">true or false</option>
				  </select>	
				<label for="number_of_questions">Select amount of questions:</label>
				<input type="number" min="1" max="50" bind:value={question_amount}>


				<input type="submit" value="Submit" >submit
		</form>

	</section>

	{#await getData()}
	<p>loading</p>
	{:then items}
		{#each items as item}
		<li>{item.results}</li>
	{/each}
	{:catch error}
	<p>{error.message}</p>
	{/await}
</main>

<style>
	
</style>