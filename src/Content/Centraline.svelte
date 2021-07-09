<script>
    import { onMount } from "svelte";
    import Lista from "./Lista.svelte";
    import Modal from "./Modal.svelte";
    import Form from "./ModificaForm.svelte";

    let data = [];
    let idex;

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

    let showModal = false;

    let toggleModal = () => {
        showModal = !showModal;
    };

    const assignID = (e) => {
        showModal = !showModal;
        idex = e.detail;
    };

    async function submitMdifica(old_id, new_id, lat, lon) {
        let formData = new FormData();
        formData.append("apikey", "2HHWGTKFP7XQ");
        formData.append("ID", old_id);
        if (old_id != new_id) {
            formData.append("new_id", new_id);
        }
        formData.append("lat", lat);
        formData.append("lon", lon);

        const response = await fetch(
            "https://sqd.sensesquare.eu:5002/modifica_centralina",
            {
                method: "POST",
                body: formData,
            }
        );
    }

    const modifica = (e) => {
        let dati = e.detail;
        submitMdifica(idex, dati.id, dati.lat, dati.lon);
        showModal = !showModal;
        window.location.reload(true);
    };
</script>

<Modal {showModal} on:click={toggleModal}>
    <h4 style="font-family: arial, sans-serif;">Inserisci i nuovi dati</h4>
    <Form id_imp={idex} on:modifica={modifica} />
</Modal>

<Lista on:assignID={assignID} />

<style>
</style>
