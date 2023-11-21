<script lang="ts">
    import Toy1 from "./Toy1.svelte";
    import Toy2 from "./Toy2.svelte";

    const tabs = [
        { label: "tab1", content: Toy1 },
        { label: "tab2", content: Toy2 },
    ];

    let currentTab = 0;
</script>

<main>
    {#each tabs as { label, content }, index}
        <button
            on:click={() => {
                currentTab = index;
            }}>{label}</button
        >
    {/each}

    {#each tabs as { label, content }, index}
        {#if currentTab === index}
            <svelte:component this={content} />
        {/if}
    {/each}
</main>

<style>
</style>
