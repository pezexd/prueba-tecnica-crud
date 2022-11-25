<script setup lang="ts">
	import { useStore } from '@/store'

	useHead({
		title: 'PRUEBA TECNICA',
	})
</script>

<template>
	<app-form />
	<app-crud />
</template>

<route lang="yaml">
name: home
</route>
