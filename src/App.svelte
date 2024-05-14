<script>
  import * as d3 from "d3";
  import { onMount } from "svelte";

  let alumnos = [];
  let grosor = d3.scaleLinear().range([5, 20]);

  let colorProductividad = d3.scaleOrdinal()
    .domain(["Positiva", "Negativa", "Depende", "No lo se", "No respondio"])
    .range(["#7AFF28", "#F23737","#999999","#CFCECE","#5F5F5F"]);

  let colorContenido = d3.scaleOrdinal()
    .domain(["Videos", "Musica", "Peliculas", "Juegos", "Series", "Articulos", "Podcasts", "Redes Sociales", "Noticias", "Chat Bot", "Campus Virtual", "No respondio"])
    .range(["#540000", "#670000", "#7D0000", "#920000", "#AE0000", "#C30000", "#D70000", "#E30000", "#EC0000", "#FF3232", "#FF3232","#5F5F5F"]);

  let colorFrecuencia = d3.scaleOrdinal()
    .domain(["Varios dias de la semana", "Una vez al dia", "Dos veces al dia", "No respondio"])
    .range(["#0B69AE", "#0094FF", "#98D3FE","#5F5F5F"]);

  let colorPlataforma = d3.scaleOrdinal()
    .domain(["Spotify", "YouTube", "Netflix", "TikTok", "Twitter", "Pinterest", "Sigedu", "No respondio"])
    .range(["#1ED760", "#FF0000", "#E50913", "#333333", "#1D9BF0", "#BD081C", "#FEBF10","#5F5F5F"]);
  
  let colorTiempo = d3.scaleOrdinal()
    .domain(["3","2","4","5","1", "No respondio"])
    .range(["#316511","#479219","#63CA24","#6CE522","#7AFF28","#5F5F5F"])

  let colorJustificacion = d3.scaleOrdinal()
    .domain(["Entretenimiento","Variedad de contenido","Facilidad de Uso ","Abarcativo","Preferencias","Interaccion Social","Calidad","Musica","Creacion","Estudios", "No respondio"])
    .range(["#640075","#550063","#740087","#A900C5","#C201E2","#84009A","#C700E8","#C700E8","#C700E8","#C700E8","#5F5F5F"])

  onMount(async () => {
    const data = await d3.csv("./data/EncuestaVisualizacion.csv", d3.autoType);
    const minMaxHoras = d3.extent(data, d => d.Tiempo);
    grosor.domain(minMaxHoras);
    alumnos = data;
  });

</script>

<main>

  <div class="header">
    <h2 class="headline">
      <b>Consumo de medios digitales.</b>
    </h2>
    <p class="bajada">Explorando los hábitos de los alumnos en plataformas online.</p>
  </div>

  <div class = "containers-grid">
    <h3>
      <p class="Titulo-container2"> Tipo de contenido preferido </p>
    </h3>
    <h3>
      <p class="Titulo-container2"> Frecuencia de actividad en linea </p>
    </h3>
    <h3>
      <p class="Titulo-container2"> Tiempo que le dedican </p>
    </h3>

  <div class="container" >
    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
           style="border-width: {grosor(alumno.Tiempo)}px; 
                  background-color: {colorContenido(alumno.Contenido)};
                  border-color: {colorContenido(alumno.Contenido)};">
          <span class="tooltip">
            {alumno.Nombre} - {alumno.Contenido}
          </span>
      </div>
    </div>
    {/each}    
  <img src="/images/Group 11.png" alt="Group 11" class="center-image" style="width: 80px; height:80px;">
  </div>

  <div class="container">
    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
           style="border-width: {grosor(alumno.Tiempo)}px; 
                  background-color: {colorFrecuencia(alumno.Frecuencia)};
                  border-color: {colorFrecuencia(alumno.Frecuencia)};">
          <span class="tooltip">
            {alumno.Nombre} - {alumno.Frecuencia}
          </span>
      </div>
    </div>  
    {/each}
    <img src="/images/Group 12.png" alt="Group 12" class="center-image" style="width: 80px; height:80px;">
  </div>

  <div class="container">
    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
           style="border-width: {grosor(alumno.Tiempo)}px; 
                  background-color: {colorTiempo(alumno.Tiempo)};
                  border-color: {colorTiempo(alumno.Tiempo)};">
          <span class="tooltip">
            {alumno.Nombre} - {alumno.Tiempo}
          </span>
      </div>
    </div>  
    {/each}
    <img src="/images/Group 13.png" alt="Group 11" class="center-image" style="width: 80px; height:80px;">
  </div>

  <h3>
    <p class="Titulo-container"> Plataformas favortias </p>
  </h3>
  <h3>
    <p class="Titulo-container">Justificación del uso</p>
  </h3>
  <h3>
    <p class="Titulo-container"> Analisis de productividad </p>
  </h3>

  <div class="container">  
    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
           style="border-width: {grosor(alumno.Tiempo)}px; 
                  background-color: {colorPlataforma(alumno.Plataforma)};
                  border-color: {colorPlataforma(alumno.Plataforma)};">
          <span class="tooltip">
            {alumno.Nombre} - {alumno.Plataforma}
          </span>
      </div>
    </div>  
    {/each}
    <img src="/images/desktop.png" alt="Plataforma" class="center-image" style="width: 80px; height:80px;">
  </div>

  <div class="container">
    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
           style="border-width: {grosor(alumno.Tiempo)}px; 
                  background-color: {colorJustificacion(alumno.Justificacion)};
                  border-color: {colorJustificacion(alumno.Justificacion)};">
          <span class="tooltip">
            {alumno.Nombre} - {alumno.Justificacion}
          </span>
      </div>
    </div>  
    {/each}
    <img src="/images/Group 14.png" alt="Group 14" class="center-image" style="width: 80px; height:80px;">
  </div>

  <div class="container">
    {#each alumnos as alumno, index}
    <div class="person-container" style="transform: translateX(-50%) translateY(-50%) translate({135 * Math.cos(2 * Math.PI * index / alumnos.length)}px, {135 * Math.sin(2 * Math.PI * index / alumnos.length)}px);">
      <div class="person"
           style="border-width: {grosor(alumno.Tiempo)}px; 
                  background-color: {colorProductividad(alumno.Productividad)};
                  border-color: {colorProductividad(alumno.Productividad)};">
          <span class="tooltip">
            {alumno.Nombre} - {alumno.Productividad}
          </span>
      </div>
    </div>  
    {/each}
    <img src="/images/Group 15.png" alt="Group 15" class="center-image" style="width: 80px; height:80px;">
  </div>
  </div>
  
  <hr class = "hr-style">
  <footer class = "footer2">
    <p class = "Leyenda"> Leyenda </p>
    <p class = "Text-footer"> A continuación, se explicaran la total utilización de los elementos:</p>
    <ul>
    <li><div class = "Color-gradient"> </div> <p class = "Texto-Leyenda"> Este gradiente de color es en representación al color de una de las categorias que hay 
      (más especificamente, la de Contendio) A medida de que el color es más oscuro, quiere decir que mucha gente coincidio en la misma respuesta. Mientras que, si 
      si el color es más claro, nos encontramos con la situacion contraria.
    </p></li>
    <div class="container2">
      <div class="circle"></div> 
      <div class="circle" style="background-color:#540000;"></div> 
      <div class="circle" style="background-color:#0B69AE;"></div> 
      <div class="circle" style="background-color:#FEBF10;"></div> 
      <div class="circle" style="background-color:#640075"></div> 
      <div class="circle" style="background-color:#5F5F5F"></div> 
    </div>    
    <li><p class = "Texto-Leyenda"> Los circulos, representan a las personas que han respondido/participado de nuestra encuesta. Ademas de ello,
       cada categoria tiene colores que son totalmente distintos uno del otro, para simbolizar que son independientes entre sí.</p></li>
  </ul>

  </footer>
  <hr class = "hr-style">
  <footer class = "footer">
    <p class  = "Text-footer"> Esta página fue creada por Lucas Brea y Nazaret Seranusoglu.</p>
    <p class = "Text-footer"> Para poder contactarnos, cuenta con los siguientes medios de comunicación:</p>
    <ul>
      <li class = "Text-footer2">Gmail de Nazaret: Nazaretseranusoglu@gmail.com</li>
      <li class = "Text-footer2">Gmail de Lucas: Lucasjbrea@gmail.com</li>
    </ul>
  </footer>
</main>

<style>

  main{
    padding-bottom:100px;
  }

  .containers-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr); 
    gap: 30px; 
    align-items: center;
    margin-top: -50px;
  }

  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    position: bottom;
    padding-bottom: -400px;
  }

  .headline {
    font-size: 30px;
    line-height: 1.2;
    font-weight: normal;
    text-align: center;
    padding-bottom: -300;
  }

  .Titulo-container {
    text-align: center;
    order: -1; 
    position:bottom;
    padding-top:120px
}

  .Titulo-container2 {
    text-align: center;
    order:-1;
    position: bottom;
    padding-top: 30px;
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
    width: 400px;  
    height: 400px;
    border-radius: 50%;
    display: flex;
    flex-direction: column;
    justify-content: center;  
    align-items: center;  
    z-index: 0;
}

.container2{
    display: flex;           
    justify-content: center; 
    align-items: center;     
    height: 10vh;          
}

.person-container {
    position: absolute;
    top: 50%;
    left: 50%;
    border-radius: 50%;
    display: inline-block; 
    z-index: 0;
  }

  .person {
    width: 35px;
    height: 35px;
    border-radius: 50%;
  }

  .center-image {
    position: absolute;
    bottom: -60px;  
    left: 50%;
    transform: translateX(-50%);
    z-index: -10;  
    max-width: 100%;  
    max-height: 100%;  
}

.footer {
    width: 100%; 
    text-align: center; 
    padding: 20px; 
    margin-top:50px;
}

.Text-footer {
    font-size: 16px;       
    font-weight: bold;       
    text-align: center;    
    font-family: Helvetica, Arial, sans-serif;
}

.Text-footer2 {
    font-size: 15px;      
    font-family: Helvetica, Arial, sans-serif;  
    padding-right: 10px;
    content: '•';
    color: white;
}

.Texto-Leyenda{
  font-size: 20;
  font-family:Helvetica, Arial, sans-serif;   
  color:white;
  text-align: left;
}

.tooltip {
    display: none; 
    position:absolute;  
    top: 190%; 
    transform: translate(-50%, -50%);
    background-color: black;
    color: white;
    padding: 5px;
    border-radius: 5px;
    white-space: nowrap;
    z-index: 9999; 
}

.person:hover .tooltip {
    display: block; 
}

.footer2 {
  margin-top: 120px;
  font-family: Helvetica, Arial, sans-serif;
}

.Leyenda {
  margin-bottom: 35px;
  font-size: 20px;
  font-weight:bolder;
  font-family: Helvetica, Arial, sans-serif;
  text-align: center;
  color:white;
  text-decoration: underline;
}

.Color-gradient {
  width: 100%;
  height: 50px;
  background: linear-gradient(to right, #540000,  #FF3232);
  margin-top: 30px; 
  margin-bottom: 30px;
  border-radius: 25px;
}

.hr-style{
  max-width: 100%;
  height: 2px; 
  background-color: #FFFFFF; 
  margin-top: 180px;;
}

.circle {
  width: 35px;       
  height: 35px;      
  background-color: #316511; 
  border-radius: 50%; 
  border: 2px solid; 
  margin-bottom:5px;
}
</style>
