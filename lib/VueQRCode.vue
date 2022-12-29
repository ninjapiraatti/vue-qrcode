<script setup lang="ts">

const props = defineProps({
		input: { type: String }
	}
)

</script>

<template>
	<h1>{{ props.input }}</h1>
</template>

<style scoped>
h1 {
	color: #7e22ce;
}
</style>