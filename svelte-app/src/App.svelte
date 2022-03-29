<script>
	import Calcbtn from './Calcbtn.svelte'
	import Display from './Display.svelte'
	const setOperColor = (event) => {
		let selected = event.detail.symbol;
		if (selected === "=")
			selected = "";
		let opers = document.getElementsByClassName("oper");
		for(var i = 0, length = opers.length; i < length; i++) {
			opers[i].style.backgroundColor = "#F94";
			if (opers[i].innerHTML === selected) {
				opers[i].style.backgroundColor = "#c72";
			}
		}
	}
	const setClear = (event) => {
		let selected = event.detail.symbol;
		let opers = document.getElementsByClassName("fn");
		opers[0].innerHTML ="C";
	}
</script>

<h1>Calculator</h1>
<div class="calc">
<Display />
	<Calcbtn use="fn" on:func = {setOperColor} >AC</Calcbtn>
	<Calcbtn use="plusminus"><sup>&plus;</sup>/<sub>&minus;</sub></Calcbtn>
	<Calcbtn use="fn">%</Calcbtn>
	<Calcbtn use="oper" on:func = {setOperColor}>&div</Calcbtn>
	<Calcbtn on:ac = {setClear}>7</Calcbtn>
	<Calcbtn on:ac = {setClear}>8</Calcbtn>
	<Calcbtn on:ac = {setClear}>9</Calcbtn>
	<Calcbtn use="oper" on:func = {setOperColor}>&times;</Calcbtn>
	<Calcbtn on:ac = {setClear}>4</Calcbtn>
	<Calcbtn on:ac = {setClear}>5</Calcbtn>
	<Calcbtn on:ac = {setClear}>6</Calcbtn>
	<Calcbtn use="oper" on:func = {setOperColor}>&minus;</Calcbtn>
	<Calcbtn on:ac = {setClear}>1</Calcbtn>
	<Calcbtn on:ac = {setClear}>2</Calcbtn>
	<Calcbtn on:ac = {setClear}>3</Calcbtn>
	<Calcbtn use="oper" on:func = {setOperColor}>&plus;</Calcbtn>
	<Calcbtn width="twowide">0</Calcbtn>
	<Calcbtn on:ac = {setClear}>.</Calcbtn>
	<Calcbtn use="oper" on:func = {setOperColor}>=</Calcbtn>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Work+Sans:wght@200&display=swap');
	.calc {
		display: inline-grid;
		justify-content: center;
		grid-template-columns: 62px 62px 62px 65px;
		grid-template-rows: 78px repeat(5, 50px);
		margin: 0 auto;
		gap: 1px;
		background: #444;
		font-family: 'Work Sans', sans-serif;
	}
</style>