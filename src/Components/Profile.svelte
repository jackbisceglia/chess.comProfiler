<script>
    export let img;
    export let name;
    export let streams;
</script>

<h1>
    {name}
</h1>
<h4>
    {streams
        ?
        "Is a Streamer"
        :
        "Not a Streamer"
    }
</h4>

<img src={img} alt="">

<style>
    h1, h4 {
        margin: 0;
        color: white;
    }
    h4 {
        font-weight: 500;
    }
    img {
        margin-top: 0.5rem;
        user-select: none;
        border-radius: 0.5rem;
    }
</style>