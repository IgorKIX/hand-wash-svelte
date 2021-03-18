<script>
    import { createEventDispatcher } from "svelte";

    import ProgressBar from './ProgressBar.svelte';

    const TOTAL_SECONDS = 20;

    const dispatch = createEventDispatcher();

    let secondsLeft = TOTAL_SECONDS;

    let isTimerRunning = false;

    $: progress = ((TOTAL_SECONDS - secondsLeft) / TOTAL_SECONDS) * 100;

    function handleStartClick() {
        if (!isTimerRunning) {
            isTimerRunning = true;

            let timer = setInterval(() => {
                secondsLeft--;

                if (!secondsLeft) {
                    clearInterval(timer);
                    dispatch("time_end");

                    isTimerRunning = false;
                    secondsLeft = TOTAL_SECONDS;
                }
            }, 1000);
        }
    }
</script>

<style>
    h2 {
        margin: 0;
    }

    .start-btn {
        background-color: rgb(43, 132, 248);
        width: 100%;
        margin: 10px 0;
    }

    .start-btn[disabled] {
        opacity: .8;
        cursor: not-allowed;
    }
</style>

<div bp=grid>
    <h2 bp="offset-5@md 4@md 12@sm">
        Seconds left: {secondsLeft}
    </h2>
</div>

<ProgressBar {progress} />

<div bp="grid">
    <button
        bp="offset-5@md 4@md 12@sm"
        class="start-btn"
        disabled={isTimerRunning} 
        on:click={handleStartClick}>
        Start
    </button>
</div>
