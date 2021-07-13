

<main>
    
    <div class="form-style-2">
        <div class="form-style-2-heading">Inserisci una nuova centralina</div>
        <script>
            
            function Modulo() {
    
                // Variabili associate ai campi del modulo
                var id = document.modulo.id.value;
                var lon = document.modulo.lon.value;
                var lat = document.modulo.lat.value;
    
    
                var id_reg_exp = /^(([A-Z ]{8})+)([0-9 ]{6})$/;
                var lon_reg_exp = /^([0-9 ]{1,10})+\.([0-9 ]{1,10})$/;
                var lat_reg_exp = /^([0-9 ]{1,10})+\.([0-9 ]{1,10})$/;
    
                //Effettua il controllo sul campo ID
                if (!id_reg_exp.test(id) || (id == "") || (id == "undefined")) {
                    alert("Inserire un id con un formato corretto.");
                    document.modulo.id.select();
                    return false;
                }
                //Effettua il controllo sul campo LONGITUDINE
                else if (!lon_reg_exp.test(lon) || (lon == "") || (lon == "undefined")) {
                    alert("Inserire longitudine con un formato corretto.");
                    document.modulo.lon.select();
                    return false;
                }
                //Effettua il controllo sul campo LATITUDINE
                else if (!lat_reg_exp.test(lat) || (lat == "") || (lat == "undefined")) {
                    alert("Inserire latitudine con un formato corretto.");
                    document.modulo.lat.select();
                    return false;
                }
                else {
    
                    var data = new FormData();
                    data.append("apikey", "N5SP82ZQN20V");
                    data.append("ID", id);
                    data.append("lat", parseFloat(lat));
                    data.append("lon", parseFloat(lon));
                    
                    var requestOptions = {
                    method: 'POST',
                    body: data,
                    redirect: 'follow'
                    };
    
                    fetch("https://sqd.sensesquare.eu:5002/inserimento_centralina", requestOptions)
                        .then(response => response.text())
                        .then(result => console.log(result))
                        .catch(error => console.log('error', error));
                    alert("Richiesta inviata");
                }
            }
        </script>
        <form action="" method="post" name="modulo">
            <label ><span>ID <span class="required">*</span></span><input type="text" class="input-field" name="id" value="" placeholder="e.g. NNRRRCCC123456"/></label>
            <label ><span>Latitudine <span class="required">*</span></span><input type="text" class="input-field" name="lat" value="" placeholder="e.g. 2.17403"/></label>
            <label ><span>Longitudine <span class="required">*</span></span><input type="text" class="input-field" name="lon" value="" placeholder="e.g. 41.40338" /></label>
            <label><span> </span><input type="submit" value="Submit" onClick="Modulo()" /></label>
        </form>
    </div>
    
</main>

<style>

    main {
        width: 100%;
        height: 100%;
    }

    .form-style-2 {
            max-width: 80%;
            height: 80%;
            padding: 20px 12px 10px 20px;
            font: 13px Arial, Helvetica, sans-serif;
            margin-left: 10%;
            
        }
        .form-style-2-heading{
            font-weight: bold;
            font-style: italic;
            border-bottom: 2px solid #ddd;
            margin-bottom: 20px;
            font-size: 15px;
            padding-bottom: 3px;
            color:darkgreen;
        }
        .form-style-2 label{
            display: block;
            margin: 0px 0px 15px 0px;
        }
        .form-style-2 label > span{
            width: 100px;
            font-weight: bold;
            float: left;
            padding-top: 8px;
            padding-right: 5px;
        }
        .form-style-2 span.required{
            color:red;
        }
        
        .form-style-2 input.input-field{
            width: 48%;
        }
        .form-style-2 input.input-field{
            box-sizing: border-box;
            -webkit-box-sizing: border-box;
            -moz-box-sizing: border-box;
            border: 1px solid greenyellow;
            box-shadow: 1px 1px 4px #EBEBEB;
            -moz-box-shadow: 1px 1px 4px #EBEBEB;
            -webkit-box-shadow: 1px 1px 4px #EBEBEB;
            border-radius: 3px;
            -webkit-border-radius: 3px;
            -moz-border-radius: 3px;
            padding: 7px;
            outline: none;
        }
        .form-style-2 .input-field:focus{
            border: 1px solid #0C0;
        }
        
        .form-style-2 input[type=submit]{
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
        }
        .form-style-2 input[type=submit]:hover{
            background: greenyellow;
            color: #fff;
        }

</style>