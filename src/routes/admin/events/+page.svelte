<script>
    import { enhance } from '$app/forms';
    import { slide } from 'svelte/transition';
    import { put } from "@vercel/blob";

    let { data } = $props();
</script>

<h1 class="text-center text-4xl font-bold text-gray-900 my-6">Admin Dashboard</h1>

<a href="/admin/events/new" class="block mx-auto w-fit px-6 py-3 bg-gradient-to-r from-pink-500 to-purple-600 text-white font-semibold text-lg rounded-full shadow-lg transition-transform transform hover:scale-105">
    + Create Event
</a>

<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6 mt-6 px-4">
    {#each data.events as event (event.id)}
    <div class="bg-white rounded-2xl shadow-xl overflow-hidden transition-transform transform hover:scale-105">
        <img src={event.image} alt="" class="w-full h-56 object-cover">
        <div class="p-4">
            <p class="text-lg font-semibold text-gray-900">{event.title}</p>
            <p class="text-sm text-gray-500 italic">{event.locationName}</p>
            <form action="?/deleteEvent" method="POST" use:enhance class="mt-4">
                <input type="hidden" name="id" value={event.id} />
                <button type="submit" class="w-full py-2 bg-red-500 text-white font-semibold rounded-full transition hover:bg-red-600">
                    Delete
                </button>
            </form>
        </div>
    </div>
    {/each}
</div>