<script lang="ts">
	import Icon from '@iconify/svelte';
	import flechita from '/public/flechita.svg';
	import { onMount } from 'svelte';
	import { user, fetchUser } from '../stores/user';
	let showProfile = false;

	onMount(() => {
		fetchUser();
		console.log($user);
	});
</script>

<div
	class="container flex flex-row items-center justify-between border-b-0 border-b-[#2f3e2f] px-15 py-5"
>
	<h1 class="mr-15 items-center text-center">
		{#if !$user}
			<span class="text-[#2f3e2f]">Bienvenido</span>
		{:else}
			<span class="text-[#2f3e2f]">
				{#if $user.sexo == 'male'}
					Bienvenido,
				{:else}
					Bienvenida,
				{/if}
			</span>
			<span class="text-[#c2b280]">{$user.nombre}</span>
		{/if}
	</h1>

	<div class="flex gap-x-20 text-lg">
		<button class="flex cursor-pointer flex-row items-center justify-center gap-1.5 font-bold">
			principal
			<Icon icon="bx:leaf" class="h-5 w-5" />
		</button>

		<div class="group relative">
			<button class="flex cursor-pointer items-center gap-1 font-bold text-[#2f3e2f]">
				estadísticas
				<img src={flechita} alt="flechita" class="-top-0.4 relative h-3.5 w-3.5" />
			</button>

			<!-- botón gris -->
			<div
				class="absolute -top-1 -left-2.5 z-10 hidden flex-col rounded-md bg-[#b9c3c8] px-3 py-1 group-hover:flex"
			>
				<div class="flex flex-row items-center gap-1">
					<span class="font-bold text-[#2f3e2f]">estadísticas</span>
					<img src={flechita} alt="flechita" class="-top-0.4 relative h-3.5 w-3.5" />
				</div>

				<div
					class="mt-1 hidden w-full min-w-52 flex-col rounded-md bg-[#7A9660] shadow-md group-hover:flex"
				>
					<a href="/voltaje" class="rounded-t-md px-4 py-2 font-bold text-white hover:bg-[#6b8755]">
						<span class="text-white">Voltaje Generado</span>
					</a>

					<a
						href="/consumo-dia"
						class="rounded-t-md px-4 py-2 font-bold text-white hover:bg-[#6b8755]"
					>
						<span class="text-white">Consumo por día</span>
					</a>

					<a href="/consumo-mes" class="px-4 py-2 font-bold text-white hover:bg-[#6b8755]">
						<span class="text-white">Consumo por mes</span>
					</a>

					<a href="/alertas" class="rounded-b-md px-4 py-2 font-bold text-white hover:bg-[#6b8755]">
						<span class="text-white">Alertas de consumo</span>
					</a>
				</div>
			</div>
		</div>

		<div class="group relative">
			<button class="flex cursor-pointer flex-row items-center justify-center gap-1 font-bold">
				editar
				<img src={flechita} alt="flechita" class="-top-0.4 relative h-3.5 w-3.5" />
			</button>

			<div
				class="absolute -top-1 -left-2.5 z-10 hidden flex-col rounded-md bg-[#b9c3c8] px-3 py-1 group-hover:flex"
			>
				<div class="flex flex-row items-center gap-1">
					<span class="font-bold text-[#2f3e2f]">editar</span>
					<img src={flechita} alt="flechita" class="-top-0.4 relative h-3.5 w-3.5" />
				</div>

				<div
					class="mt-1 hidden w-full min-w-52 flex-col rounded-md bg-[#7A9660] shadow-md group-hover:flex"
				>
					<a href="/login" class="rounded-t-md px-4 py-2 font-bold hover:bg-[#6b8755]">
						<span class="text-white">Iniciar Sesión</span>
					</a>
					<a href="/sign_up" class="rounded-b-md px-4 py-2 font-bold text-white hover:bg-[#6b8755]">
						<span class="text-white">Crear Cuenta</span>
					</a>
				</div>
			</div>
		</div>
	</div>

	<div class="group relative">
		<button class="cursor-pointer" on:click={() => (showProfile = !showProfile)}>
			{#if $user}
				<img src={$user.foto_perfil} alt="Foto de perfil" class="h-10 w-10 rounded-full" />
			{:else}
				<Icon icon="bx:user" class="h-10 w-10 cursor-pointer rounded-full" />
			{/if}
		</button>

		{#if showProfile}
			<div class="mt-1 flex-col rounded-md bg-[#b9c3c8] absolute -top-4.5 -right-4.5 shadow-md min-w-52 p-0.5">
				<div class="flex flex-row justify-around items-center">
					{#if $user}
						<span class="p-5">{$user.nombre}</span>
					{:else}
						<span class="p-5">Usuario</span>
					{/if}
					<button class="cursor-pointer flex flex-row" on:click={() => (showProfile = !showProfile)}>
						{#if $user}
							<img src={$user.foto_perfil} alt="Foto de perfil" class="h-10 w-10 rounded-full" />
						{:else}
							<Icon icon="bx:user" class="h-10 w-10 cursor-pointer rounded-full" />
						{/if}
					</button>
				</div>


				<div class="flex flex-col justify-center items-center">
					{#if $user}
						<a href="/logout" class="flex justify-center px-4 py-2 font-bold text-white hover:bg-[#6b8755] rounded-2xl w-full items-center">
							<Icon icon="bx:log-out" class="h-5 w-5" />
							<span class="text-red-500 rounded-2xl text-center">Cerrar Sesión</span>
						</a>
					{:else}
						<a href="/login" class="flex justify-center px-4 py-2 font-bold text-white hover:bg-[#6b8755] rounded-2xl w-full items-center">
							<span class="text-white rounded-2xl text-center">Iniciar Sesión</span>
						</a>
					{/if}
				</div>
			</div>
		{/if}
	</div>

</div>
<div class="h-0.5 w-228 bg-gray-500"></div>
