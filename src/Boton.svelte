<script>
export let tipo = "insertar";
import { onMount, getContext} from "svelte";
const URL = getContext("URL");
let handler = () => {};  
function insertar() {
    console.log("insertar")
        let opciones = {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(documento),
        }
        fetch(URL.Articulos, opciones)
        .then(res => res.json())
        .then(datos => console.log(datos))
        .catch(error => console.log(error));
    }
    function setup(){
        switch (tipo){
            case 'insertar': handler = insertar; break;
            case 'modificar': handler = modificar; break;
            case 'eliminar': handler = eliminar; break;
            default:
        }
    }
    onMount(setup)
    function eliminar() { console.log("eli")}
    function modificar() { console.log("mod")}
</script>

<input type="button" value={tipo} on:click {insertar}>