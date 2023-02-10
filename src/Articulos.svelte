<script>
    import {onMount} from "svelte";
    import Buscar from "./Buscar.svelte";

    let patron = "Camisa";
    let data = [];
let datosFiltrados = [];
    let getArticulos = async () => {
        const respose = await fetch ('https://tiendabackend.fly.dev/api/articulos/')
        data = await respose.json()
    }

    onMount(getArticulos)
    
    $: datosFiltrados = data.filter(articulo => RegExp(patron, "i").test(articulo.nombre))
</script>
<Buscar bind:busqueda={patron}/>
<hr><br>

{#each datosFiltrados as articulo}
<p>Articulo: {articulo.nombre}</p><br>
<p>Precio: {articulo.precio}</p><br><br>
{/each}