<script>
    import { onMount } from "svelte";
    import { navigate } from "svelte-routing";
    import { fly } from "svelte/transition";
    import Button from "../components/Button.svelte";
    import { playAudio } from "../lib/ui/helpers";
    const PLAY_DELAY = 500;
    onMount(() => {
        // We wait a little bit in order not to overlap the different aural feedback
        setTimeout(async () => await playAudio("invalid"), PLAY_DELAY);
    });

    function onDone() {
        navigate("/home");
    }
</script>

<main transition:fly={{ y: 200, duration: 500 }}>
    <section>
        <i class="icon-cross" />
        <p>INVALID CREDENTIAL</p>
    </section>
    <footer>
        <Button label="Done" onClick={() => navigate("/home")} />
    </footer>
</main>

<style>
    main {
        display: flex;
        flex-direction: column;
        overflow-y: auto;
        -webkit-overflow-scrolling: touch;
        height: 100%;
        width: 100%;
        background: black;
    }

    section {
        z-index: 2;
        height: 100%;
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    section > p {
        z-index: 2;
        position: relative;
        justify-content: center;
        align-items: center;
        font-family: "Proxima Nova", sans-serif;
        font-weight: 600;
        font-size: 1.9vh;
        line-height: 3.4vh;
        color: #fff;
    }

    .icon-cross {
        font-size: 64px;
    }

    footer {
        position: fixed;
        width: 100%;
        bottom: 0;
        z-index: 6;
    }
</style>
