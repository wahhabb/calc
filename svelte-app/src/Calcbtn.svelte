<script context="module">
	 let lastBtn = ""
	 let lastOper = ""
	 let operand = ""
	 let inDecimal = 0;
</script>
<script>
	export let width = "";
	export let use = "number";
	import { display } from './stores.js';
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	
	let calcClick = (a) => {
		const btn = a.target.innerHTML;
		if ("0" <= btn && btn <= "9") {
			dispatch('ac', {
				symbol: btn,
			});
			if (lastBtn != "number" ) {
				display.set(0);
			}
			if (inDecimal == 1) {
				display.set(Number(String($display) + "." + btn))
				++inDecimal
			} else {
			if (inDecimal) {
				display.set(Number(String($display) + btn))
				++inDecimal		
			} else {
				display.set($display * 10 + Number(btn))
			}
	}
			lastBtn = "number"
			
		} else if (btn == "<sup>+</sup>/<sub></sub>") {
				display.set(-$display)
		} else {
			switch (btn) {
			case ".":		
				if (inDecimal == 0) {
					inDecimal = 1;
					if (lastBtn === "operator") {
						lastBtn = "number"
						display.set(0)						
					}
				}
				break
			case "AC":
				lastOper = "" // fall through!	
			case "C":
				display.set(0)
				lastBtn = "number"
				a.target.innerHTML = "AC"
				inDecimal = 0
				break
			case "%":
				display.set($display / 100)
				break
		case "+":
		case "":
		case "×":
		case "÷":
		case "=":
		dispatch('func', {
			symbol: btn,
		});
				switch (lastOper) {
					case "":
						operand = $display
						break;
					case "+":
						operand += $display
						break;
					case "":
						operand -= $display
						break;
					case "×":
						operand *= $display
						break;
					case "÷":
						operand /= $display
						break;
				}
				display.set(operand)
				lastBtn = "operator"
				lastOper = btn;
				inDecimal = 0
				if (btn === "=") {
					lastOper = "";
					operand = 0;
				}
				break;			
		}
	}
	}
</script> 
	
<button class="{width} {use}" on:click={(a) => calcClick(a)}>
	<slot></slot>
</button>
<style>
	button {
		background: #777;
		height: 100%;
		color: white;
		font-size: 140%;
		font-weight: 200;
		border: none;
	}
	button:active {
		background:#aaa;
	}
	.twowide {
		grid-column-end: span 2;
		text-align: left;
		padding-left: 1.3em;
	}
	.oper {
		background: #f94;
		font-size: 180%;
		padding-top: .31em;
	}
	.fn, .plusminus {
		background: #555;
	}
	button.oper:active {
		background: #c72;
	}
	button.fn:active, button.plusminus:active {
		background: #777;
	}
</style>