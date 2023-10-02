<script setup>
import { ref } from 'vue';
const Layout = [['C', 'CE', '', '/'],
['7', '8', '9', '*'],
['4', '5', '6', '+'],
['1', '2', '3', '-'],
['0', '.', '='],
];
const numbers = Array.from({ length: 10 }, (value, index) => String(index))
const operators = ["/", "*", "+", "-"];
let buffer = 0;
let operator = ref("")
let result = ref("0");
function calculate(operation) {
	if (operation == "=") {
		const number = result.value.includes('.') ? parseFloat(result.value) : parseInt(result.value)
		switch (operator.value) {
			case "+":
				buffer += number
				break;
			case "-":
				buffer -= number
				break;
			case "*":
				buffer *= number
				break;
			case "/":
				buffer /= number
				break;
		}
		console.log(result.value, result.value.includes('.') ? parseFloat(result.value) : parseInt(result.value), buffer, buffer + number)
		result.value = String(buffer)
		// buffer = 0
	}
	if (operators.includes(operation)) {
		operator.value = operation
		buffer = result.value.includes('.') ? parseFloat(result.value) : parseInt(result.value);
		result.value = "0"
	}
	else if (numbers.includes(operation)) {
		if ((operation == '0' && result.value.includes('.')) == false) {
			result.value += operation;
		}
	}
	else {
		switch (operation) {
			case 'C':
				result.value = "0";
				break;
			case '.':
				if (result.value.includes('.') == false) {
					result.value += "."
				}
				break;
			default:
				break;
		}
	}
}
</script>

<template>
	<section class="calculator">
		<section class="panel">
			<div style="overflow-x: scroll;">
				<samp>{{ result.includes('.') ? parseFloat(result) : parseInt(result) }}</samp>
			</div>
			<span class="operator">{{ operator }}</span>
		</section>
		<table>
			<tr v-for="array in Layout">
				<td v-for="val in array" :colspan="val == '0' ? 2 : 1">
					<button @click="calculate(val)" v-if="val != ''">{{ val }}</button>
				</td>
			</tr>
		</table>
	</section>
</template>

<style lang="scss" scoped >
section.calculator {
	$cell-size: 50px;

	section.panel {
		position: relative;
		border: 0.5rem var(--second-background) groove;
		padding: 0.25rem;
		height: 2rem;
		width: $cell-size*4;

		samp {
			font-size: 2rem;
			max-width: 100%;
		}

		.operator {
			position: absolute;
			right: -3rem;
			top: -2rem;
			font-size: 3rem;
			padding: 0.2rem;
			font-weight: bolder;
			border-radius: 0.1rem;
		}
	}

	table {
		border-collapse: collapse;
		border-spacing: 0;
		user-select: none;

		td {

			width: $cell-size;
			height: $cell-size;
			border: 3px solid;
			text-align: center;

			button {
				font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
				font-weight: bolder;
				font-size: 2rem;
				border: none;
				background: none;
				color: var(--text);
				width: 100%;
				height: 100%;

				&:hover {
					background-color: var(--selection);
				}
			}

		}
	}
}
</style>