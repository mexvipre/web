<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Conteo Regresivo Mejorado</title>
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
<style>
  body {
    background-color: #ffffff;
    color: #0a0a0a;
    font-family: Arial, sans-serif;
  }
  .container {
    text-align: center;
    margin-top: 50px;
    position: relative; /* Posición relativa para contener las chispitas */
  }
  .spark {
    width: 10px; /* Ajustar el ancho de las chispitas */
    height: 10px; /* Ajustar la altura de las chispitas */
    position: absolute;
    border-radius: 50%;
    background-color: transparent;
  }

  .table {
    background-color: transparent; /* Eliminar el fondo gris de las tablas */
    border-collapse: collapse; /* Hacer que las líneas de la tabla no sean visibles */
  }
  .table th, .table td {
    border: none; /* Eliminar los bordes de las celdas */
  }
  .table td {
    font-family: "Times New Roman", Times, serif; /* Cambiar el tipo de letra de los números */
    font-size: 24px; /* Tamaño de fuente para los números */
  }
  .progress-bar {
    background-color: rgb(245, 229, 229);
    border-radius: 10px;
    margin-top: 20px;
    overflow: hidden;
    position: relative; /* Añadir posicionamiento relativo */
  }
  .progress {
    height: 30px;
    border-radius: 10px;
    text-align: center;
    line-height: 30px;
    color: #000;
    background-color: #4caf50;
    width: 0%;
    transition: width 1s ease;
  }
  .progress-text {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    color: black; /* Cambiar el color del texto según lo necesites */
  }
  .running-person {
    position: absolute;
    top: 30%; /* Colocar la imagen en la mitad vertical de la barra de progreso */
    transform: translateY(-50%); /* Ajustar la posición vertical para centrar la imagen */
    width: 53px; /* Ajustar el tamaño de la imagen según sea necesario */
    height: auto; /* Mantener la proporción de la imagen */
    z-index: 1; /* Asegurar que la imagen esté por encima de la barra de progreso */
  }

  /* Estilos para dispositivos móviles */
  @media (max-width: 768px) {
    .container {
      margin-top: 20px;
      width: 100%; /* Ajustar el ancho al 100% en dispositivos móviles */
      height: 60vh; /* Establecer la altura al 100% de la ventana gráfica */
      overflow-x: hidden; /* Evitar desplazamiento horizontal en dispositivos móviles */
      overflow-y: auto; /* Permitir desplazamiento vertical si es necesario */
    }
    .table {
      width: 100%; /* Ajustar el ancho al 100% en dispositivos móviles */
    }
    body {
      overflow-x: hidden; /* Evitar desplazamiento horizontal en dispositivos móviles */
    }
  }

</style>
</head>
<body>

<div class="container">


  <h3 style="font-size: 20px;"><B style="color: #4caf50;"><B></B><B><u>ATENCION PROGRAMADA</u></B></h3>
  <h6 style=" color :#000;">Orden Generada 8 de febrero de 2024 a las 9:00 AM</h6>
 
  <table class="table table-bordered">
    <thead>
      <tr>
        <th scope="col">Días</th>
        <th scope="col">Horas</th>
        <th scope="col">Minutos</th>
        <th scope="col">Segundos</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td id="days">0</td>
        <td id="hours">0</td>
        <td id="minutes">0</td>
        <td id="seconds">0</td>
      </tr>
    </tbody>
  </table>

  <div class="progress-bar">
    <div class="progress" id="progress"></div>
    <div class="progress-text" id="progressText"></div> <!-- Nuevo elemento para mostrar el porcentaje -->
    <img src="corredor.gif" class="running-person"> <!-- Agregar la imagen GIF del corredor -->
  </div>
  <h3 style="font-size: 15px;"><B style="color: #000000;"><B></B><B>Domingo 11/02/2024 09:00 hrs</B></h3>

  <table class="table table-bordered mt-5">
    <thead>
      <tr>
        <th scope="col"><B style="color: #4caf50;"><B>PROBLEMA REPORTADO POR EL CLIENTE</B></th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="font-size: 20px;">El Equipo No Enciende </td>

      </tr>
    </tbody>
  </table>

  <table class="table table-bordered mt-5">
    <thead>
      <tr>
        <th scope="col"><B style="color: #4caf50;">TRABAJO A REALIZAR</B></th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="font-size: 20px;">Mantenimiento General de tres PC <br> Mantenimiento General de Laptop</td>
      </tr>
    </tbody>
  </table>

</div>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
// Definir la fecha de inicio (8 de febrero de 2024 a las 9:00 AM)
const startTime = new Date("2024-02-08T09:00:00").getTime();
// Definir la fecha de finalización (11 de febrero de 2024 a las 9:00 AM)
const endTime = new Date("2024-02-11T09:00:00").getTime();

// Función para actualizar el contador regresivo y la barra de progreso
function updateCountdown() {
  const currentTime = new Date().getTime();
  
  // Calcular el tiempo transcurrido desde el inicio
  const elapsedTime = currentTime - startTime;
  
  // Calcular el tiempo total
  const totalTime = endTime - startTime;
  
  // Si el tiempo ha terminado, establecer valores a 0
  if (elapsedTime >= totalTime) {
    document.getElementById("days").innerText = "0";
    document.getElementById("hours").innerText = "0";
    document.getElementById("minutes").innerText = "0";
    document.getElementById("seconds").innerText = "0";
    clearInterval(interval);
    document.getElementById("progress").style.width = "100%";
    document.getElementById("progressText").innerText = "100%";
    return;
  }
  
  // Calcular días, horas, minutos y segundos restantes
  const days = Math.max(Math.floor((totalTime - elapsedTime) / (1000 * 60 * 60 * 24)), 0);
  const hours = Math.max(Math.floor(((totalTime - elapsedTime) % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)), 0);
  const minutes = Math.max(Math.floor(((totalTime - elapsedTime) % (1000 * 60 * 60)) / (1000 * 60)), 0);
  const seconds = Math.max(Math.floor(((totalTime - elapsedTime) % (1000 * 60)) / 1000), 0);
  
  // Actualizar los elementos HTML con los valores calculados
  document.getElementById("days").innerText = days;
  document.getElementById("hours").innerText = hours;
  document.getElementById("minutes").innerText = minutes;
  document.getElementById("seconds").innerText = seconds;
  
  // Calcular y actualizar el porcentaje de la barra de progreso
  const progressPercentage = ((currentTime - startTime) / (endTime - startTime)) * 100;
  document.getElementById("progress").style.width = progressPercentage.toFixed(2) + "%";
  
  // Mostrar el porcentaje actual en el centro de la barra de progreso
  document.getElementById("progressText").innerText = progressPercentage.toFixed(2) + "%";
  
  // Mover la imagen del corredor junto con el llenado de la barra de progreso
  const progressBarWidth = $(".progress-bar").width();
  const runningPersonWidth = $(".running-person").width();
  const leftPosition = (progressBarWidth - runningPersonWidth) * (progressPercentage / 100);
  $(".running-person").css("left", leftPosition + "px");
}

// Función para generar chispitas de colores de forma aleatoria
function generateSparks() {
  const colors = ['#FFFFFF', '#FFFFFF', '#FFFFFF', '#FFFFFF', '#FFFFFF']; // Colores de las chispitas
  const container = document.querySelector('.container');
  const sparkCount = 100; // Número de chispitas a generar
  const sparks = []; // Arreglo para almacenar las chispitas
  
  for (let i = 0; i < sparkCount; i++) {
    const spark = createSpark(container, colors);
    const speedX = (Math.random() - 0.5) * 1; // Velocidad horizontal aleatoria (-1 a 1)
    const speedY = (Math.random() - 0.5) * 1; // Velocidad vertical aleatoria (-1 a 1)
    moveSpark(spark, container.offsetWidth, container.offsetHeight, speedX, speedY, sparks);
  }
}

// Función para crear una chispita con color aleatorio
function createSpark(container, colors) {
  const spark = document.createElement('div');
  spark.classList.add('spark');
  spark.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
  spark.style.width = '10px'; // Ajustar el ancho de la chispita
  spark.style.height = '10px'; // Ajustar la altura de la chispita
  spark.style.left = Math.random() * container.offsetWidth + 'px';
  spark.style.top = Math.random() * container.offsetHeight + 'px';
  container.appendChild(spark);
  return spark;
}

// Función para mover las chispitas y hacer que reboten entre sí y en los bordes del contenedor
function moveSpark(spark, containerWidth, containerHeight, speedX, speedY, sparks) {
  // Función para actualizar la posición de la chispita en cada fotograma
  function updatePosition() {
    let posX = parseFloat(spark.style.left);
    let posY = parseFloat(spark.style.top);
    
    // Actualizar la posición de la chispita
    posX += speedX;
    posY += speedY;
    
    // Verificar los límites del contenedor y hacer que la chispita rebote
    if (posX < 0 || posX > containerWidth - parseFloat(spark.style.width)) {
      speedX *= -1; // Cambiar dirección horizontal
    }
    if (posY < 0 || posY > containerHeight - parseFloat(spark.style.height)) {
      speedY *= -1; // Cambiar dirección vertical
    }
    
    // Actualizar la posición de la chispita
    spark.style.left = posX + 'px';
    spark.style.top = posY + 'px';
    
    // Llamar a la función de actualización en el próximo fotograma de animación
    requestAnimationFrame(updatePosition);
  }
  
  // Iniciar el movimiento de la chispita
  updatePosition();
}

// Llamar a las funciones de actualización del contador y de generación de chispitas
updateCountdown();
generateSparks();

// Actualizar el contador cada segundo
const interval = setInterval(updateCountdown, 1000);
</script>

</body>
</html>
