<template>
	<div
		class="w-full p-4 bg-[#394264] rounded-lg shadow sm:p-6 md:p-8 text-white"
	>
		<ul class="flex flex-col divide-y w-full">
			<transition-group name="fade">
				<li
					class="flex flex-row w-inherit"
					v-for="expense in props.expenseList"
					:key="expense.name"


				>
					<div
						class="cursor-pointer hover:bg-[#1f253d] flex flex-1 justify-between items-center group border-4 border-[#394264]"
						:class="
							expense.type === 'Expense'
								? 'border-l-rose-500'
								: 'border-l-green-500'
						"
					>
						<div class="pl-1 mr-16 ml-5 w-3/4 overflow-hidden text-ellipsis">
							<div class="font-medium text-white">{{ expense.title }}</div>
							<div class="text-gray-200 text-sm ">
								{{ expense.description }}
							</div>
						</div>
						<div class="text-gray-200 text-lg m-5">{{ expense.amount }}</div>
						<div
							id="trash"
							class="text-white text-lg bg-[#cc324b] h-full p-3 content-center transition-all hidden group-hover:block"
							@click="deleteTransaction(expense.name)"
						>
							<svg
								xmlns="http://www.w3.org/2000/svg"
								width="18"
								height="18"
								fill="currentColor"
								class="bi bi-trash mt-3"
								viewBox="0 0 16 16"
							>
								<path
									d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5m2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5m3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0z"
								/>
								<path
									d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4zM2.5 3h11V2h-11z"
								/>
							</svg>
						</div>
					</div>
				</li>
			</transition-group>
		</ul>
	</div>
</template>

<script setup>
import { defineProps } from "vue";

const emit = defineEmits(['transactionDeleted'])

const props = defineProps(["expenseList"]);


const deleteTransaction = (name)=>{
	emit('transactionDeleted', name)
}
</script>

<style scoped>
.animate__fadeOut{
	position: absolute;
}

.fade-enter-from{
	opacity: 0;
}

.fade-enter-active{
	transition: all 1s linear;
}

.fade-leave-to{
	transition: all 1s linear;
	opacity: 0;
}

</style>
