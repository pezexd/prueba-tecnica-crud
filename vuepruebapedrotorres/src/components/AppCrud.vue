<script setup lang="ts">
    import { TabulatorFull as Tabulator } from 'tabulator-tables'
    import dataT from '@/types/dataModel'
    import { cultural_rights, expertises, nacs } from '@/helpers'

    const exampleTable = ref<HTMLElement | string>("")
    const tabulator = ref()

	const dateFormat = (date: string): Date => {
		const dateTransform = new Date(date)

		return dateTransform.toLocaleString("es-ES") as unknown as Date
	}

    const tabledata: dataT[] = [
        {
            id: 1,
            consecutive: "FP2",
            "monitor_id": "KAREM LOPEZ",
            "cultural_right_id": "Acceso y participación en la vida cultural",
            "nac_id": "Restrepo",
            "activity_date": dateFormat("2022-09-05"),
            "start_time": "10:00",
            "final_hour": "11:00",
            "expertise_id": "Danza",
            "fecha_db": dateFormat("2022-09-05"),
            "state": "Aprobado"
        },
        {
            id: 2,
            consecutive: "FP2",
            "monitor_id": "KAREM LOPEZ",
            "cultural_right_id": "Acceso y participación en la vida cultural",
            "nac_id": "Restrepo",
            "activity_date": dateFormat("2022-09-05"),
            "start_time": "10:00",
            "final_hour": "11:00",
            "expertise_id": "Danza",
            "fecha_db": dateFormat("2022-09-05"),
            "state": "Aprobado"
        },
        {
            id: 3,
            consecutive: "FP2",
            "monitor_id": "KAREM LOPEZ",
            "cultural_right_id": "Acceso y participación en la vida cultural",
            "nac_id": "Restrepo",
            "activity_date": dateFormat("2022-09-05"),
            "start_time": "10:00",
            "final_hour": "11:00",
            "expertise_id": "Danza",
            "fecha_db": dateFormat("2022-09-05"),
            "state": "Aprobado"
        },
        {
            id: 4,
            consecutive: "FP2",
            "monitor_id": "KAREM LOPEZ",
            "cultural_right_id": "Acceso y participación en la vida cultural",
            "nac_id": "Restrepo",
            "activity_date": dateFormat("2022-09-05"),
            "start_time": "10:00",
            "final_hour": "11:00",
            "expertise_id": "Danza",
            "fecha_db": dateFormat("2022-09-05"),
            "state": "Aprobado"
        },
    ];

    onMounted(() => {
        tabulator.value = new Tabulator(exampleTable.value, {
            data: tabledata,
            reactiveData: true,
            columns:[
                {title:"#", field:"id", width:50},
                {title:"CONSECUTIVO", field:"consecutive", editor:"input"},
                {title:"NOMBRE", field:"monitor_id", editor:"input"},
                {title:"DERECHO CULTURAL", field:"cultural_right_id", editor:"input"},
                {title:"NAC", field:"nac_id", editor:"input"},
                {title:"FECHA", field:"activity_date", editor:"input"},
                {title:"HORA INICIO", field:"start_time", editor:"input"},
                {title:"HORA FINAL", field:"final_hour", editor:"input"},
                {title:"EXPERTICIA", field:"expertise_id", editor:"input"},
                {title:"FECHA CARGA", field:"fecha_db", editor:"input"},
                {title:"ESTADO", field:"state", editor:"input"},
            ],
            layout:"fitData",
        })
    })

	const filters = reactive({
		search: "",
		cultural_filter: "",
		nacs_filter: "",
		expertises_filter: "",
		date_range: "",
		date_range2: "",
		state: "",
		entrys: ""
	})
</script>

<template>
	<section class="mt-16 border-t-2 border-dashed border-black">
		<header class="p-4">
			<h2 class="text-lg">
				Vista de Lista
			</h2>
		</header>
		<div class="grid grid-rows-[auto_1fr_auto] md:grid-rows-1 md:grid-cols-[auto_1fr_auto] gap-4 border-y-2 border-black py-2 px-8">
			<div class="flex md:h-28 md:w-8 pointer-events-none">
				<h3 class="inline-block text-4xl md:transform md:-rotate-90 pointer-events-none">
					Filtros
				</h3>
			</div>
			<div class="flex flex-col items-center gap-y-4">
				<div class="flex flex-col gap-8 md:flex-row md:items-start">
					<div class="flex gap-4">
						<button class="flex justify-center min-w-max border-2 border-black px-2 py-1 rounded text-sm font-semibold">
							Crear registro
						</button>
						<div class="flex items-center gap-2 max-w-xs">
							<label for="search" class="text-sm font-semibold">Buscar:</label>
							<div class="relative block">
								<span class="absolute inset-y-0 right-0 flex items-center pr-2">
									<icon:carbon:search class="w-5 h-5" />
								</span>
								<input v-model="filters.search" id="search" type="text" class="py-1 px-2 md:max-w-[107px] text-sm border-2 border-black outline-none rounded w-auto">
							</div>
						</div>
					</div>
					<div class="flex flex-col gap-2 md:grid md:grid-cols-[auto_auto_auto]">
						<div class="relative block">
							<span class="absolute inset-y-0 right-0 flex items-center px-0.5 border-2 border-black bg-stone-300 pointer-events-none">
								<icon:carbon:caret-down />
							</span>
							<select v-model="filters.cultural_filter" id="cultural_filter" class="w-full pr-2 text-sm border-2 border-black outline-none">
								<option value="" disabled>
									Derecho cultural
								</option>
								<option :value="cultural_right" v-for="cultural_right in cultural_rights">
									{{ cultural_right }}
								</option>
							</select>
						</div>
						<div class="relative block">
							<span class="absolute inset-y-0 right-0 flex items-center px-0.5 border-2 border-black bg-stone-300 pointer-events-none">
								<icon:carbon:caret-down />
							</span>
							<select v-model="filters.nacs_filter" id="nacs_filter" class="w-full pr-2 text-sm border-2 border-black outline-none">
								<option value="" disabled>
									Nac
								</option>
								<option :value="nac" v-for="nac in nacs">
									{{ nac }}
								</option>
							</select>
						</div>
						<div class="relative block">
							<span class="absolute inset-y-0 right-0 flex items-center px-0.5 border-2 border-black bg-stone-300 pointer-events-none">
								<icon:carbon:caret-down />
							</span>
							<select v-model="filters.expertises_filter" id="expertises_filter" class="w-full pr-2 text-sm border-2 border-black outline-none">
								<option value="" disabled>
									Experticia
								</option>
								<option :value="expertise" v-for="expertise in expertises">
									{{ expertise }}
								</option>
							</select>
						</div>
					</div>
				</div>
				<div class="flex flex-col items-start md:flex-row md:items-center gap-2">
					<label for="date_range" class="font-medium">
						Fecha rango:
					</label>
					<div class="relative block">
						<span class="absolute inset-y-0 right-0 flex items-center px-1 rounded-r bg-white border-2 border-black pointer-events-none">
							<icon:carbon:calendar />
						</span>
						<input v-model="filters.date_range" id="date_range" type="date" class="py-1 px-2 text-sm border-2 border-black outline-none rounded w-auto">
					</div>
					<div class="relative block">
						<span class="absolute inset-y-0 right-0 flex items-center px-1 rounded-r bg-white border-2 border-black pointer-events-none">
							<icon:carbon:calendar />
						</span>
						<input v-model="filters.date_range2" id="date_range2" type="date" class="py-1 px-2 text-sm border-2 border-black outline-none rounded w-auto">
					</div>
				</div>
			</div>
			<div class="flex flex-col justify-between gap-2">
				<div class="flex justify-between gap-2">
					<div class="flex">
						<div class="relative block">
							<span class="absolute inset-y-0 right-0 flex items-center px-0.5 border-2 border-black bg-stone-300 pointer-events-none">
								<icon:carbon:caret-down />
							</span>
							<select v-model="filters.state" id="state" class="pr-2 max-w-[107px] text-sm border-2 border-black outline-none w-auto">
								<option value="" disabled>
									Estado
								</option>
								<option value="approved">
									Aprobado
								</option>
								<option value="rechazed">
									Rechazado
								</option>
								<option value="revision">
									En revision
								</option>
							</select>
						</div>
					</div>
					<div class="flex items-center gap-1 relative">
						<label for="entrys" class="text-sm font-semibold">
							Mostrar
						</label>
						<div class="relative block">
							<span class="absolute inset-y-0 right-0 flex items-center px-0.5 border-2 border-black bg-stone-300 pointer-events-none">
								<icon:carbon:caret-down />
							</span>
							<select v-model="filters.entrys" id="entrys" class="pr-2 max-w-[107px] text-sm border-2 border-black outline-none w-auto">
								<option value="10">
									10
								</option>
								<option value="20">
									20
								</option>
							</select>
						</div>
						<span class="text-sm font-semibold">
							Entradas
						</span>
					</div>
				</div>
				<div class="grid grid-cols-2 gap-4 md:gap-1">
					<button class="flex gap-1 justify-between items-center px-2 py-1 outline-none border-2 border-black rounded text-sm font-semibold bg-emerald-400">
						<span>
							Exportar PDF
						</span>
						<icon:carbon:generate-pdf />
					</button>
					<button class="flex gap-1 justify-between items-center px-2 py-1 outline-none border-2 border-black rounded text-sm font-semibold bg-emerald-400">
						Exportar XLS
						<icon:carbon:download />
					</button>
				</div>
			</div>
		</div>
	</section>
	<section class="mt-16">
		<div ref="exampleTable"></div>
	</section>
</template>

<style>
    @import  "tabulator-tables";
</style>