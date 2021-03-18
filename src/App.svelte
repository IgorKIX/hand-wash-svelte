<script>
    import HowTo from './HowTo.svelte';
    import Timer from './Timer.svelte';

    let audio;

    function playSound() {
        audio.play();
    }
</script>

<style>
    h1, h3 {
        text-align: center;
    }
</style>

<h1>Handwashing App</h1>

<Timer on:time_end={playSound}/>

<HowTo />

<h3>
    <a href="https://www.who.int/gpsc/clean_hands_protetion/en/">
        Picture source
    </a>

    <a href="https://freesound.org/people/metrostock99/sounds/345086/">
        Sound source
    </a>
</h3>

<audio bind:this={audio}>
    <source src="sound.wav" />
</audio>

