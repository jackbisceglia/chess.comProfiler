<script>
    import { userNameQuery } from '../Stores/searchTerm';
    let searchTerm = '';
    export let toggleSearched;

</script>

<p>Enter your chess.com username</p>
<input on:change={(e) => searchTerm = e.target.value} placeholder="Chess.com username" type="text">
<button on:click={() => {
    userNameQuery.set(searchTerm)
    toggleSearched();
    }}>
    submit
</button>

<style>
    p {
        user-select: none;
        font-size: 1.1rem;
        color: rgb(231, 231, 231);
    }

    input {
        width: 14rem;
        border-radius: 0.25rem;
        outline: rgba(255,0,0,1);
        margin: 0 0.5rem;
    }

    button {
        margin: 0 0.5rem;
        width: 4.5rem;
        color: #1f1f1f;
        background-color: rgba(255,155,19,1);
        outline: 0;
        border-radius: 0.25rem;
        border: none;
        outline: none;
        font-weight: 400;
        cursor: pointer;
    }
</style>