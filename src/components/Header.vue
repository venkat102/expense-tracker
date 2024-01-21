<template>
	<header class="bg-[#394264] mb-5 rounded-lg">
		<nav
			class="mx-auto flex max-w-7xl items-center justify-between p-6 lg:px-8"
			aria-label="Global"
		>
			<div class="flex lg:flex-1 text-2xl text-white">Expense Tracker</div>

			<div class="hidden lg:flex lg:flex-1 lg:justify-end">
				<span class="text-lg font-semibold leading-6 text-[#11a8ab] p-5">{{ props.income }}</span>
				<div class="w-full h-4 mt-6 bg-[#e64c65] rounded-full">
					<div
						class="h-4 bg-[#11a8ab] rounded-full"
						id="progress-bar"
					></div>
				</div>
				<span class="text-lg font-semibold leading-6 text-[#e64c65] p-5">{{ props.expense }}</span>
			</div>

		</nav>
	</header>
</template>

<script setup>
import { computed, defineProps} from 'vue'

const props = defineProps(['income', 'expense'])

const progressPercent = computed(()=>{
	const total_amount = props.income + props.expense
	return `${props.income / total_amount * 100}%`
})

</script>

<style scoped>
#progress-bar{
	width: v-bind(progressPercent);
}
</style>
