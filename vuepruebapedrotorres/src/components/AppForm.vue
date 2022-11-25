<script setup lang="ts">
    import { cultural_rights, expertises, nacs } from '@/helpers'
    import formT from '@/types/formModel'

    const formModel = reactive<formT>({
        nac: "",
        final_hour: "",
        start_time: "",
        activity_name: "",
        expertise_id: "",
        activity_date: new Date(),
        cultural_right_id: "",
    })
</script>

<template>
    <section class="flex flex-col gap-4">
		<header>
			<div class="grid grid-cols-2">
				<div>
					<h2 class="text-4xl">
						Formulario
					</h2>
				</div>
				<div class="flex justify-end">
					<p class="text-2xl">
						Consecutivo
					</p>
				</div>
			</div>
		</header>
		<form>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-x-12 gap-y-4">
				<div class="flex flex-col">
					<label for="nombre_act" class="text-lg font-semibold">
						NOMBRE ACTIVIDAD *
					</label>
					<input v-model="formModel.activity_name" id="nombre_act" type="text" placeholder="Hora de Inicio" class="app-input">
				</div>
				<div class="flex flex-col">
					<label for="fecha" class="text-lg font-semibold">
						FECHA *
					</label>
					<input v-model="formModel.activity_date" id="fecha" type="date" placeholder="Fecha del dia" class="app-input">
				</div>
				<div class="flex flex-col">
					<label for="hora_inicio" class="text-lg font-semibold">
						HORA INICIO *
					</label>
					<input v-model="formModel.start_time" id="hora_inicio" type="time" placeholder="Hora de Inicio" class="app-input">
				</div>
				<div class="flex flex-col">
					<label for="hora_final" class="text-lg font-semibold">
						HORA FINAL *
					</label>
					<input v-model="formModel.final_hour" :min="formModel.start_time" id="hora_final" type="time" placeholder="Hora Final" class="app-input">
				</div>
				<div class="flex flex-col">
					<label for="derechos_culturales" class="text-lg font-semibold">
						Derechos culturales *
					</label>
					<select v-model="formModel.cultural_right_id" id="derechos_culturales" type="text" placeholder="Seleccione" class="app-input">
						<option value="" disabled>
							Seleccione
						</option>
						<option :value="cultural_right" v-for="cultural_right in cultural_rights">
							{{ cultural_right }}
						</option>
					</select>
				</div>
				<div class="flex flex-col">
					<label for="nac" class="text-lg font-semibold">
						NAC
					</label>
					<select v-model="formModel.nac" id="nac" type="text" class="app-input">
						<option value="" disabled>
							Seleccione
						</option>
						<option :value="nac" v-for="nac in nacs">
							{{ nac }}
						</option>
					</select>
				</div>
				<div class="flex flex-col">
					<label for="experticia" class="text-lg font-semibold">
						EXPERTICIA *
					</label>
					<select v-model="formModel.expertise_id"  id="experticia" type="text" class="app-input">
						<option value="" disabled>
							Seleccione
						</option>
						<option :value="expertise" v-for="expertise in expertises">
							{{ expertise }}
						</option>
					</select>
				</div>
				<div class="flex justify-end items-end">
					<button class="bg-blue-400 text-white font-semibold text-2xl px-4 py-1 rounded">
						Guardar
					</button>
				</div>
			</div>
		</form>
	</section>
</template>