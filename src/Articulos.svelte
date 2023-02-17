<script>
    import { onMount, getContext } from "svelte";
    import Buscar from "./Buscar.svelte";
    import { data } from "./store.js";
    import Articulo from "./Articulo.svelte";
    import Boton from "./Boton.svelte";
    let articuloInsertar = {}

    const URL = getContext("URL");
    let patron = "Camisa";
    let datosFiltrados = [];

    let getArticulos = async () => {
        const respose = await fetch(URL.articulos);
        $data = await respose.json();
    };

    onMount(getArticulos);

    $: datosFiltrados = $data.filter((articulo) =>
        RegExp(patron, "i").test(articulo.nombre)
    );
</script>

<Buscar bind:busqueda={patron} />
<hr />
<br />
<Articulo bind:articulo = {articuloInsertar}>
<Boton documento={articuloInsertar}/>
</Articulo>
<hr />
{#each datosFiltrados as articulo}
    <Articulo bind:articulo = {articulo}>
    <Boton tipo="modificar" documento={articulo}/>
    <Boton tipo="eliminar" documento={articulo}/><br />
    </Articulo>
    <hr />
{/each}
