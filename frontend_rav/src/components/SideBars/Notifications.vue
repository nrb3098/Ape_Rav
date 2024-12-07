<template>
	<div class=" bg-azulBarraApe w-64 md:w-[260px] xl:w-72 rounded-[35px] mr-2 mt-2 h-screen ">
		<!-- Sidebar Derecho -->
		<div>
			<div class="flex flex-col bg-white items-center ">
				<!-- Sección de Actividad -->
				<div
					class="bg-azulBarraApe md:w-full  flex justify-between px-4 items-center shadow-custom lg:shadow-none rounded-tr-[35px] rounded-tl-[35px]">
					<h2
						class="text-lg md:text-xl lg:text-2xl lg:text-center font-bold text-amarillo py-2 ">
						Actividad
					</h2>
					<div class="md:w-10">
						<router-link to="/IndicadoresActividad">
						<span>
						<svg
							width="38"
							height="37"
							viewBox="0 0 41 40"
							fill="none"
							xmlns="http://www.w3.org/2000/svg">
							<rect
								x="0.5"
								y="-0.000244141"
								width="40.0001"
								height="40.0003"
								rx="20"
								fill="#7A1F7E" />
							<path	
								d="M23.95 11.7801C23.91 12.0301 23.89 12.2801 23.89 12.5301C23.89 14.7801 25.71 16.5991 27.95 16.5991C28.2 16.5991 28.44 16.5701 28.69 16.5301V24.5991C28.69 27.9901 26.69 30.0001 23.29 30.0001H15.901C12.5 30.0001 10.5 27.9901 10.5 24.5991V17.2001C10.5 13.8001 12.5 11.7801 15.901 11.7801H23.95ZM24.151 17.8601C23.88 17.8301 23.611 17.9501 23.45 18.1701L21.031 21.3001L18.26 19.1201C18.09 18.9901 17.89 18.9391 17.69 18.9601C17.491 18.9901 17.311 19.0991 17.19 19.2591L14.231 23.1101L14.17 23.2001C14 23.5191 14.08 23.9291 14.38 24.1501C14.52 24.2401 14.67 24.3001 14.84 24.3001C15.071 24.3101 15.29 24.1891 15.43 24.0001L17.94 20.7691L20.79 22.9101L20.88 22.9691C21.2 23.1391 21.6 23.0601 21.83 22.7591L24.72 19.0301L24.68 19.0501C24.84 18.8301 24.87 18.5501 24.76 18.3001C24.651 18.0501 24.41 17.8801 24.151 17.8601ZM28.0901 9.99976C29.4201 9.99976 30.5001 11.0798 30.5001 12.4098C30.5001 13.7398 29.4201 14.8198 28.0901 14.8198C26.7601 14.8198 25.6801 13.7398 25.6801 12.4098C25.6801 11.0798 26.7601 9.99976 28.0901 9.99976Z"
								fill="#FDC300" />
						</svg>
						</span>
						</router-link>
					</div>
				</div>
				<!--linea divisora text actividad-->
				<div class="bg-white w-[260px] h-0.5 -mt-5 mb-5"></div>
				<div class="grid grid-cols-1 bg-azulBarraApe items-center gap-5 p-3"> 
					<!-- Agrega un gap para separación -->
				<div v-for="(goal, index) in goals" :key="index" class="indicator-wrapper flex items-center gap-10 rounded-lg overflow-hidden" 
					:style="getGradientStyle(index)">
					<!-- Indicador Circular -->
					<div class="relative w-32 h-20 md:w-32 md:h-52">
					<svg class="w-full h-full" viewBox="0 0 100 100">
						<circle
						cx="50"
						cy="50"
						r="30"
						stroke="lightgray"
						stroke-width="6"
						fill="none" />
						<circle
						cx="50"
						cy="50"
						r="30"
						stroke="currentColor"
						:stroke-dasharray="circumference"
						:stroke-dashoffset="circumference - (circumference * goal.value) / 100"
						stroke-width="5"
						fill="none"
						class="text-customPurple transition-all duration-1000 ease-out" />
					</svg>
					<span class="absolute inset-0 flex items-center justify-center text-lg font-bold w-full h-full text-center ">
						{{ goal.value }}%
					</span>
					</div>

					<!-- Texto a la derecha del indicador -->
					<div class="grid grid-cols-1 justify-center items-start">
					<div :class="index === 2 ? 'text-white' : 'text-black'" class="text-sm font-semibold ">
						{{ goal.label }}
					</div>
					<div :class="index === 2 ? 'text-white text-2xl font-bold' : 'text-black text-xl font-bold'">
						{{ goal.meta || 0 }}
					</div>
					<div :class="index === 2 ? 'text-white' : 'text-black'" class="mt-1 text-sm font-semibold">
						Estado Actual
					</div>
					<div :class="index === 2 ? 'text-white text-2xl font-bold' : 'text-black text-xl font-bold'">
						{{ goal.current || 0 }}
					</div>
					</div>
				</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
// Estado de las metas (si es necesario para otras funcionalidades)180deg, #5E91E1 0%, #315CA0 100%

const getGradientStyle = () => {
  return {
    background: 'linear-gradient(180deg, #E3F2FD 0%, #1565C0 100%)',
    backgroundBlendMode: 'multiply',
  };
};

const goals = ref([
  { label: "Meta Anual", value: 0, meta: 1000000, current: 1200 },
  { label: "Meta Trimestral", value: 0, meta: 3000000, current: 50 },
  { label: "Meta Diaria", value: 0, meta: 30000, current: 600 }     
]);


const circumference = 2 * Math.PI * 40;
// Simular valores de las metas (puedes eliminar esta parte si no es necesario)
onMounted(() => {
	setTimeout(() => {
	    goals.value[0].value = 80; 
		goals.value[1].value = 50; 
		goals.value[2].value = 60; 
	}, 500);
});

// Notificaciones
const notifications = ref([
	{
		title: "Título de notificación",
		date: "17/07/2024",
		message: "Lorem ipsum dolor sit amet...",
		redirectUrl: "http://localhost:5173/subirfichero", // Aquí se añade la URL de redirección
	},
	{
		title: "Título de notificación",
		date: "17/07/2024",
		message: "Lorem ipsum dolor sit amet...",
		redirectUrl: "http://localhost:5173/subirfichero", // Aquí se añade la URL de redirección
	},
]);

const additionalNotifications = computed(() => notifications.value.slice(1));
const extraNotifications = computed(() =>
	Math.max(0, notifications.value.length - 1)
);

const showAllNotifications = ref(false);
const toggleNotifications = () => {
	showAllNotifications.value = !showAllNotifications.value;
};
</script>
<style scoped></style>