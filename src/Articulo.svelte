<script>
    export let articulo = {nombre:"", precio: 0};
  </script>

<input id="nombre" type="text" placeholder="Nombre" value={articulo.nombre}/>
<input id="precio" type="number" placeholder="Precio" value={articulo.precio}/>

<slot></slot>