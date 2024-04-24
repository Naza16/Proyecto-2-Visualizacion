<script>
  import * as d3 from "d3";
  import { onMount } from "svelte";

  let alumnos = [];

  let grosor = d3.scaleLinear().range([5, 20]);

  let colorProductividad = d3.scaleOrdinal()
    .domain(["POSITIVA", "NEGATIVA"])
    .range(["#F23737", "#7AFF28"]);

  let colorContenido = d3.scaleOrdinal()
    .domain(["Videos", "Musica", "Peliculas", "Juegos", "Series", "Articulos", "Podcasts", "Redes Sociales", "Noticias", "Chat Bot", "Campus Virtual"])
    .range(["#540000", "#670000", "#7D0000", "#920000", "#AE0000", "#C30000", "#D70000", "#E30000", "#EC0000", "#FF3232", "#FF3232"]);

  let colorFrecuencia = d3.scaleOrdinal()
    .domain(["Varios dias de la semana", "Una vez al dia", "Dos veces al dia"])
    .range(["#0B69AE", "#0094FF", "#98D3FE"]);

  let colorPlataforma = d3.scaleOrdinal()
    .domain(["Spotify", "YouTube", "Netflix", "TikTok", "Twitter", "Pinterest", "Sigedu"])
    .range(["#9caf88", "#ff1f1f", "#870f10", "#a865b5", "#9bc7ec", "#990000", "#e2edeb"]);

  let colorTiempo = d3.scaleOrdinal()
    .domain(["3","2","4","5","1"])
    .range(["#316511","#479219","#63CA24","#6CE522","#7AFF28"])

  let colorJustificacion = d3.scaleOrdinal()
    .domain(["Entretenimiento","Variedad de contenido","Facilidad de Uso ","Abarcativo","Preferencias","Interaccion Social","Calidad","Musica","Creacion","Estudios"])
    .range(["#640075","#550063","#740087","#A900C5","#C201E2","#84009A","#C700E8","#C700E8","#C700E8","#C700E8"])

  onMount(async () => {
    const data = await d3.csv("./data/EncuestaVisualizacion.csv", d3.autoType);
    const minMaxHoras = d3.extent(data, d => d.Tiempo);
    grosor.domain(minMaxHoras);
    alumnos = data;
  });
</script>

<main>
  <body>
  <div class="header">
    <h2 class="headline">
      <b>Screentime de los estudiantes</b>
    </h2>
    <p class="bajada">Explorando los hábitos de nuestros alumnos en plataformas online.</p>
  </div>
  <div class = "containers-grid">


    <h2>
      <p class="Titulo-container">Tipo de contenido que más consumen</p>
    </h2>

    <h2>
      <p class="Titulo-container">Frecuencia con la que consumen el contenido</p>
    </h2>

    <h2>
      <p class="Titulo-container">Tiempo que le dedican al contenido en linea</p>
    </h2>

  <div class="container">

    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
        style="border-width: {grosor(alumno.Tiempo)}px; 
               background-color: {colorContenido(alumno.Contenido)};
               border-color: {colorContenido(alumno.Contenido)};">
      </div>
    </div>
    {/each}
    <img src="/images/Group 11.png" alt="Group 11" class="center-image" style="width: 160px; height:160px;">
  </div>

  <div class="container">
    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
        style="border-width: {grosor(alumno.Tiempo)}px; 
               background-color: {colorFrecuencia(alumno.Frecuencia)};
               border-color: {colorFrecuencia(alumno.Frecuencia)};">
      </div>
    </div>
    {/each}
    <img src="/images/Group 12.png" alt="Group 11" class="center-image" style="width: 160px; height:160px;">
  </div>

  <div class="container">
    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
        style="border-width: {grosor(alumno.Tiempo)}px; 
               background-color: {colorTiempo(alumno.Tiempo)};
               border-color: {colorTiempo(alumno.Tiempo)};">
      </div>
    </div>
    {/each}
    <img src="/images/Group 13.png" alt="Group 11" class="center-image" style="width: 160px; height:160px;">
  </div>

  <h2>
    <p class="Titulo-container">Plataforma que mas consumen</p>
  </h2>

  <h2>
    <p class="Titulo-container">Justificacion del uso</p>
  </h2>

  <h2>
    <p class="Titulo-container">Su productividad se ve afectada?</p>
  </h2>

  <div class="container">  
    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
        style="border-width: {grosor(alumno.Tiempo)}px; 
               background-color: {colorPlataforma(alumno.Plataforma)};
               border-color: {colorPlataforma(alumno.Plataforma)};">
      </div>
    </div>
    {/each}
    <img src="/images/desktop.png" alt="Plataforma" class="center-image" style="width: 160px; height:160px;">
  </div>

  <div class="container">
    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
        style="border-width: {grosor(alumno.Tiempo)}px; 
               background-color: {colorJustificacion(alumno.Justificacion)};
               border-color: {colorJustificacion(alumno.Justificacion)};">
      </div>
    </div>
    {/each}
    <img src="/images/Group 14.png" alt="Group 14" class="center-image" style="width: 160px; height:160px;">
  </div>

  <div class="container">
   
    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
        style="border-width: {grosor(alumno.Tiempo)}px; 
               background-color: {colorProductividad(alumno.Productividad)};
               border-color: {colorProductividad(alumno.Productividad)};">
      </div>
    </div>
    {/each}
    <img src="/images/Group 15.png" alt="Group 15" class="center-image" style="width: 160px; height:160px;">
  </div>
  </div>
  </body>
</main>

<style>


  .containers-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr); /* Tres columnas */
    gap: 30px; /* Espacio entre columnas y filas */
    align-items: center;

  }

  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: -20px;
  }

  

  .headline {
    font-size: 30px;
    line-height: 1.2;
    font-weight: normal;
    text-align: center;
  }

  .Titulo-container {
    text-align: center; /* Centra el texto */
    order: -1; /* Asegura que siempre esté al principio */
    position:bottom;
}

  .bajada {
    font-size: 30px;
    font-weight: normal;
    text-align: center;
    margin-top:-25px;
  }

  .container {
    background-color: black;
    position: relative;
    width: 300px;
    height: 300px;
    border-radius: 50%;
    display: flex;
    flex-direction: column;
    justify-content: flex-start; /* Asegura que todo comienza desde arriba */
    align-items: center; /* Centra horizontalmente, pero el título debe estar al principio */
    margin: auto;
    overflow: hidden;
    padding-top: 10px; /* Espacio adicional en la parte superior si es necesario */
}

  .person-container {
    position: absolute;
    top: 50%;
    border-radius: 50%;

    left: 50%;
  }

  .person {
    width: 25px;
    height: 25px;
    border-radius: 50%;
    background-color: transparent;
  }

  .center-image {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    max-width: 80%;
    max-height: 80%;
  }
</style>
