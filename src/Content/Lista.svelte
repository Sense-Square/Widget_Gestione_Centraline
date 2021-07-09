<script>
    import { onMount, createEventDispatcher } from "svelte";
    let dispatch = createEventDispatcher();

    let data = [];

    onMount(async () => {
        let formData = new FormData();
        formData.append("apikey", "2HHWGTKFP7XQ");
        formData.append("fonte", "ssq");

        const response = await fetch(
            "https://sqd.sensesquare.eu:5001/elenco_centraline",
            {
                method: "POST",
                body: formData,
            }
        );
        if (response.status == 200) {
            data = await response.json();
        }
    });

    const search = () => {
        let input = document.getElementById("Select").value;
        input = input.toLowerCase();
        let x = document.getElementsByClassName("element");
        let i;
        for (i = 0; i < x.length; i++) {
            if (
                !x[i]
                    .getElementsByTagName("h5")[0]
                    .innerHTML.toLowerCase()
                    .includes(input)
            ) {
                x[i].style.display = "none";
            } else {
                x[i].style.display = "list-item";
            }
        }
    };

    async function submitElimina(id) {
        let formData = new FormData();
        formData.append("apikey", "2HHWGTKFP7XQ");
        formData.append("ID", id);

        const response = await fetch(
            "https://sqd.sensesquare.eu:5002/elimina_centralina",
            {
                method: "POST",
                body: formData,
            }
        );
    }

    const handleModifica = (id) => {
        dispatch("assignID", id);
    };

    const handleElimina = (id) => {
        submitElimina(id);
        window.location.reload(true);
    };
</script>

<br />
<input
    type="text"
    id="Select"
    on:keyup={search}
    placeholder="Ricerca centralina.."
/>
<br />
<ul id="Centraline">
    {#each data as c}
        <div class="element">
            <li class="centralina">
                <div class="container">
                    <div class="segment">
                        <b><h5>{c.ID}</h5></b>
                        <p>
                            Latitudine: {c.lat} <br /> Longitudine: {c.lon}
                        </p>
                    </div>
                    <div class="segment">
                        <button
                            on:click={() => {
                                handleElimina(c.ID);
                            }}>Elimina</button
                        >
                        <button
                            on:click={() => {
                                handleModifica(c.ID);
                            }}>Modifica</button
                        >
                    </div>
                </div>
            </li>
        </div>
    {/each}
</ul>

<style>
    #Select {
        background-repeat: no-repeat;
        font-size: 16px;
        padding: 12px 20px 12px 20px;
        border: 1px solid #ddd;
        border-radius: 3px;
        position: relative;
        display: block;
        margin: 0 auto;
        margin-top: 2px;
    }

    #Centraline {
        list-style-type: none;
        height: 60%;
        width: 70%;
        line-height: 16px;
        border: 1px solid #ccc;
        padding: 0;

        overflow: scroll;
        overflow-x: hidden;
        position: relative;
        display: block;
        margin: 0 auto;
    }

    #Centraline li {
        font-family: arial, sans-serif;
        border: 1px solid #ddd;
        margin-top: -1px;
        /* Prevent double borders */
        background-color: #f6f6f6;
        padding: 18px;
        text-decoration: none;
        font-size: 14px;
    }
    .container {
        align-items: center;
        display: flex;
    }

    .segment {
        width: 250px;
    }

    button {
        background-color: greenyellow;
        border-radius: 5px;
        border: none;
        border-radius: 2px;
        margin: 5px;
        padding: 7px;
        float: right;
        cursor: pointer;
    }

    button {
        font-family: arial, sans-serif;
        font-size: inherit;
        border: none;
        background: yellowgreen;
        color: #fff;
        box-shadow: 1px 1px 4px #DADADA;
        -moz-box-shadow: 1px 1px 4px #DADADA;
        -webkit-box-shadow: 1px 1px 4px #DADADA;
        border-radius: 3px;
        -webkit-border-radius: 3px;
        -moz-border-radius: 3px;
        margin: 5px;
        padding: 7px;
        float: right;
        cursor: pointer;
    }
    button:hover{
        background: greenyellow;
        color: #fff;
    }
</style>
