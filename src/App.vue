<script setup>
import Header from "@/components/Header.vue";
import ExpenseList from "./components/ExpenseList.vue";
import FormView from "./components/FormView.vue";
import { useToast } from "vue-toastification";

import { ref, computed, onMounted } from "vue";

const toast = useToast();
let expenseList = ref([]);

onMounted(()=>{
	const savedExpenses = JSON.parse(localStorage.getItem('expenses'));

	if (savedExpenses) {
		expenseList.value = savedExpenses;
	}
})

const addExpense = (transaction) => {
	expenseList.value.unshift(transaction);
	saveExpensesToLocalStorage()
	toast.success("New Expense Added")
};

const removeExpense = (name) => {
	expenseList.value =expenseList.value.filter((transaction) => transaction.name != name)
	saveExpensesToLocalStorage()
	toast.success("Expense Deleted")
};

const saveExpensesToLocalStorage = () => {
	localStorage.setItem('expenses', JSON.stringify(expenseList.value));
};

const income = computed(()=>{
	let incomeAmount = 0.0
	expenseList.value.forEach(element => {
		if (element.type == "Income") {
			incomeAmount += element.amount
		}
	});
	return incomeAmount
})

const expense = computed(()=>{
	let expenseAmount = 0.0
	expenseList.value.forEach(element => {
		if (element.type == "Expense") {
			expenseAmount += element.amount
		}
	});
	return expenseAmount
})
</script>

<template>
	<main class="main-container">
		<Header :income="income" :expense="expense"></Header>
		<section class="h-full w-full">
			<div class="grid grid-cols-2 gap-4">
				<div class="">
					<ExpenseList :expenseList="expenseList" @transactionDeleted="removeExpense"></ExpenseList>
				</div>
				<div class="">
					<FormView @transactionAdded="addExpense"></FormView>
				</div>
			</div>
		</section>
	</main>
</template>

<style>
body {
	background-color: #1f253d;
}

.main-container {
	width: 1600px;
	height: 800px;
	margin: 2em auto;
}
</style>
