<script lang="ts">
	import { SlideToggle } from '@brainandbones/skeleton';
	import { historyChapter, historyKomik } from '$lib/stores/history';
	import type { PageData } from './$types';
	export let data: PageData;
	let showHistoryKomik = true;
	let showHistoryChapter = true;
</script>

<svelte:head>
	<title>BacaBin</title>
</svelte:head>

<div class="content">
	<div class="md:w-[80%] mt-10 mb-24 mx-auto text-center">
		<h1>BacaBin</h1>
		<h5>@author: Binsar Dwi Jasuma</h5>
		<div class="my-10 tracking-wide">
			<h5>*Pesan Langsung Dari Developer. Silakan Disimak!!</h5>
			<p>
				Website ini merupakan website baca komik <strong class="uppercase">ilegal</strong> yang mengambil
				konten dari website lain baik legal maupun ilegal dan digunakan hanya untuk diri saya sendiri.
				Silakan berdonasi atau dukungan apapun untuk situs aslinya apabila Anda ingin membacanya di sini,
				bebas iklan
			</p>
		</div>
	</div>
	<div class="mb-10">
		<h3 class="mb-5">Silakan Pilih Server Website</h3>
		<div class="grid grid-cols-3 md:grid-cols-4 items-center lg:grid-cols-5 gap-10">
			{#each data.servers as server}
				<div class="transform transition duration-500 hover:scale-110">
					<a href="/{server.server}">
						{#if server.img}
							<img src={server.img} width="100%" alt="[img] {server.title}" />
						{:else}
							<h2>{server.title}</h2>
						{/if}
					</a>
				</div>
			{/each}
		</div>
	</div>

	<div class="mb-10">
		<h3>History Per Komik</h3>
		<SlideToggle bind:checked={showHistoryKomik} size="sm" accent="bg-gray-500" />
		<div>
			{#if showHistoryKomik}
				<ul>
					{#each $historyKomik as history}
						<li class="mb-2">
							<a href={history.link} class="hover:text-blue-500">
								<p>{history.title}</p>
								<p>Server: {history.server}</p>
							</a>
						</li>
					{/each}
				</ul>
			{:else}
				<p>Pencet toggle di atas untuk menampilkan</p>
			{/if}
		</div>
	</div>
	<div class="mb-10">
		<h3>History Per Chapter</h3>
		<SlideToggle bind:checked={showHistoryChapter} size="sm" accent="bg-gray-500" />
		<div>
			{#if showHistoryChapter}
				<ul>
					{#each $historyChapter as history}
						<li class="mb-2">
							<a href={history.link} class="hover:text-blue-500">
								<p>{history.title}</p>
								<p>Server: {history.server}</p>
							</a>
						</li>
					{/each}
				</ul>
			{:else}
				<p>Pencet toggle di atas untuk menampilkan</p>
			{/if}
		</div>
	</div>

	<footer class="mt-20">
		<h2>Let's Connected</h2>
		<table class="text-left mt-3">
			{#each data.connection as connection}
				<tr>
					<th>{connection.platform}</th>
					<td class="pr-5">:</td>
					<td
						><a
							href={connection.link}
							class="hover:text-blue-500 active:text-blue-800"
							target="_blank">{connection.text}</a
						></td
					>
				</tr>
			{/each}
		</table>
	</footer>
</div>
