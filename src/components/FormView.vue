<template>
	<div
		class="w-full p-4 bg-[#394264] rounded-lg shadow sm:p-6 md:p-8 text-white overflow-hidden text-ellipsis"
	>
		<div>
			<form class="mx-auto" @submit.prevent="onSubmit">
				<div class="flex lg:flex-1 text-2xl text-white mb-5">
					Add New Expense
				</div>

				<div class="mb-5">
					<label class="block mb-2 text-sm font-medium text-white">Title</label>
					<input
						class="border text-sm rounded-lg block w-full p-2.5 bg-[#1f253d] border-gray-600 placeholder-gray-400 text-white focus:ring-blue-500 focus:border-blue-500"
						placeholder="Food Expense"
						v-model="title"
					/>
				</div>

				<div class="mb-5">
					<label class="block mb-2 text-sm font-medium text-white">Type</label>
					<select
						id="countries"
						v-model="type"
						class="border text-sm rounded-lg block w-full p-2.5 bg-[#1f253d] border-gray-600 placeholder-gray-400 text-white focus:ring-blue-500 focus:border-blue-500"
					>
						<option>Income</option>
						<option>Expense</option>
					</select>
				</div>

				<div class="mb-5">
					<label class="block mb-2 text-sm font-medium text-white"
						>Description</label
					>
					<textarea
						rows="4"
						v-model="description"
						class="border text-sm rounded-lg block w-full p-2.5 bg-[#1f253d] border-gray-600 placeholder-gray-400 text-white focus:ring-blue-500 focus:border-blue-500"
						placeholder="Expense on lunch with friends"
					></textarea>
				</div>

				<div class="mb-5">
					<label class="block mb-2 text-sm font-medium text-white"
						>Amount</label
					>
					<input
						class="border text-sm rounded-lg block w-full p-2.5 bg-[#1f253d] border-gray-600 placeholder-gray-400 text-white focus:ring-blue-500 focus:border-blue-500"
						placeholder="100"
						type="number"
						v-model="amount"
					/>
				</div>

				<button
					type="submit"
					class="text-white focus:ring-4 focus:outline-none font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center bg-[#4fc4f6] hover:bg-[#35aadc] focus:ring-blue-800"
				>
					Add New Item
				</button>
			</form>
		</div>
	</div>
</template>

<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const toast = useToast();
const emit = defineEmits(['transactionAdded']);

let title = ref("");
let type = ref("");
let description = ref("");
let amount = ref("");



const onSubmit = ()=> {
	if (!title.value || !type.value || !description.value || !amount.value) {
		toast.error("All fields must be filled!");
		return
	}

	const transaction = {
		name: Date.now(),
		title: title.value,
		type: type.value,
		description: description.value,
		amount: parseFloat(amount.value)
	}

	emit('transactionAdded', transaction)

	title = ''
	type = ''
	description = ''
	amount = ''

}
</script>
<style scoped></style>
