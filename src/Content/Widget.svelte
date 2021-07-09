<script>

    /* NON MODIFICARE -> INIZIO */ 
    import { createEventDispatcher } from 'svelte';
    import InserimentoCentralina from './InserimentoCentralina.svelte';
    import Centraline from './Centraline.svelte';
    export let visible = false;
	const dispatch = createEventDispatcher();
    const showResult = () => dispatch("showResult");
    const inserimentod = () => dispatch("inserimentotrue");
    const showError = (text) => dispatch("showError", {text}); 
    const showMaintenance = (text) => dispatch("showMaintenance", {text}); 
    const showLoading = (text) => dispatch("showLoading", {text}); 
    const showProgressBar = (text, value=0) => dispatch("showProgressBar", {text, value});
    const updateProgressBar = (text, value=0) => dispatch("updateProgressBar", {text, value}); 
    /* NON MODIFICARE -> FINE */ 

    /* ESEMPIO FUNZIONAMENTO ->  INIZIO */
    import { Button } from 'svelte-materialify';
    setTimeout(() => {
        showResult();
    }, 1000);
    /* ESEMPIO FUNZIONAMENTO ->  FINE */
    let inserimento=false;
    let modifica=false;

</script>

<main style={visible ? "" : "display: none"}>

    <div class="container">
        <div class="bottone">
            <button class="button" on:click={() => {inserimento = false; modifica=false}}>
                <div class="button__arrow button__arrow--left"></div>
            </button>
        </div>
        <div class="testo">
            <p text-align="center"> Gestione Centraline</p>
        </div>
    </div>
    {#if inserimento==true}
        <InserimentoCentralina />
    {/if}
    {#if modifica==true}
        <Centraline />
    {/if}
    {#if inserimento==false && modifica==false }
    <div class="containerbutton">
        <div class="center">
            <button on:click={() => {inserimento = true}}>Inserimento Centraline</button>
        </div>
    </div>
    <div class="containerbutton">
        <div class="center">
            <button on:click={() => {modifica = true}}>Modifica Centraline</button>
        </div>
    </div>      
    {/if}

    

</main>

<style>

    main {
        width: 100%;
        height: 100%;
    }

    .container {
        color: greenyellow;
        font-size:larger;
        font-weight: bold;
        text-align: center;
        margin: auto;
        text-shadow: 1px;
        border: 2px solid green;
        border-radius: 3px;
        width: 80%;
        margin-top: 9px;
        margin-bottom: 9px;
    }

    .containerbutton { 
        position: relative; 
        height: 50px;
        margin-bottom: 10px;
        
    }

    .center { 
        margin: 0;
        position: absolute;
        top: 50%;
        left: 50%;
        -ms-transform: translate(-50%, -50%);
        transform: translate(-50%, -50%);
    }

    button {
        font-family: arial, sans-serif;
        font-size: inherit;
        border: none;
        padding: 8px 15px 8px 15px;
        background: rgb(138, 207, 0);
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
        background: rgb(65, 206, 0);
        color: #fff;
    }

    .button {
    /* Center the content */
        align-items: left;
        float: left;
        justify-content: center;
        margin-left: 3%;
    }

    .button__arrow {
        /* Transparent background */
        background-color: transparent;

        /* Size */
        height: 12px;
        width: 12px;
    }

    .button__arrow--left {
        /* Edges */
        border-bottom: 1px solid rgba(0, 0, 0, 0.3);
        border-left: 1px solid rgba(0, 0, 0, 0.3);
        transform: translateX(25%) rotate(45deg);
    }

    .bottone {
        width:15%;
    }

    .testo{
        width:60%;
        
    }

</style>