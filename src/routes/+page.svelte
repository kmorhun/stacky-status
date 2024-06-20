<div class="logo">
    <!-- image of logo -->
    <img src="stacky.png" alt="Stacky Logo">
</div>

<div class="statusList">
    {#each allProps as props}
        <StatusMarker props={props}></StatusMarker>
    {/each}
</div>

<style>
    img {
        margin-top: 5vw;
        display: block;
        margin-left: auto;
        margin-right: auto;
        width: 300px;
    }
    .statusList {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: center;
        font-family: 'Avenir', sans-serif;
        font-stretch: ultra-wide;
    }
</style>

<script>
    import StatusMarker from '$lib/StatusMarker.svelte';

    let allProps = [
        {
            systemName: "Mastodon (don't trust)",
            systemPort: 3000,
            mode: "Production",
            url: "https://beta.stacky.social/api/v1/timelines/public"
        },
        {
            systemName: "Mastodon Frontend (don't trust)",
            systemPort: 3000,
            mode: "Production",
            url: "https://beta.stacky.social"
        },
        {
            systemName: "Curate",
            systemPort: 3002,
            mode: "Production",
            url: "https://beta.stacky.social:3002/ping"
        }
        
    ]

    allProps.sort((a, b) => a.systemName.localeCompare(b.systemName));

</script>