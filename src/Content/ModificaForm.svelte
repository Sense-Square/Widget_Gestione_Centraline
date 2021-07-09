<script>
    import { createEventDispatcher } from "svelte";
    let dispatch = createEventDispatcher();

    export let id_imp;
    let id = id_imp;
    let lat;
    let lon;
    const handleClick = () => {
        if (
            id == null ||
            id == "" ||
            typeof lat === "undefined" ||
            lat == null ||
            typeof lon === "undefined" ||
            lon == null
        ) {
            alert("Nessun campo può essere vuoto");
        } else {
            const data = {
                id,
                lat,
                lon,
            };
            dispatch("modifica", data);
        }
    };
</script>

<form on:submit|preventDefault={handleClick}>
    <label for="ID">ID:</label>
    <input id="ID" type="text" placeholder="ID" bind:value={id} />
    <br />
    <label for="lat">Latitudine:</label>
    <input
        id="lat"
        type="number"
        step="any"
        placeholder="Latitudine"
        bind:value={lat}
    />
    <br />
    <label for="lon">Longitudine:</label>
    <input
        id="lon"
        type="number"
        step="any"
        placeholder="Longitudine"
        bind:value={lon}
    />
    <br />
    <button>Modifica Centralina</button>
</form>

<style>
    label {
        font-family: arial, sans-serif;
        font-size: inherit;
        display: inline-block;
        width: 100px;
        text-align: right;
    }
    input {
        font-family: arial, sans-serif;
        font-size: inherit;
        padding: 0.4em;
        margin: 0 0 0.5em 0;
        box-sizing: border-box;
        border: 1px solid #ccc;
        border-radius: 2px;
    }

    input:disabled {
        color: #ccc;
    }
    button {
        font-family: arial, sans-serif;
        font-size: inherit;
        border: none;
        padding: 8px 15px 8px 15px;
        background: yellowgreen;
        color: #fff;
        box-shadow: 1px 1px 4px #DADADA;
        -moz-box-shadow: 1px 1px 4px #DADADA;
        -webkit-box-shadow: 1px 1px 4px #DADADA;
        border-radius: 3px;
        -webkit-border-radius: 3px;
        -moz-border-radius: 3px;
        padding: 7px;
        margin: 8px auto;
        float: center;
        cursor: pointer;
    }
    button:hover{
        background: greenyellow;
        color: #fff;
    }
</style>
