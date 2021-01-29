<script>
    export let gameType;
    export let bestRtg;
    export let currRtg;
</script>

<div class="type-wrap">
    <h3>{gameType}</h3>
        <p>Best Rating: <b>{bestRtg}</b> </p>
        <p>Current Rating: <b>{currRtg}</b></p>
</div>

<style>
    h3{
        color: white;
    }
    p {
        color:  rgb(34, 211, 255);
        margin: 0;
    }
</style>