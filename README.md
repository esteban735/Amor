<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Amor Infinito</title>
    <style>
        body {
            margin: 0;
            overflow: hidden; /* Para ocultar barras de desplazamiento */
            background-color: #ffe0e6; /* Un rosa muy claro para el fondo */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh; /* Ocupa el 100% del alto de la ventana */
            font-family: 'Arial', sans-serif;
            position: relative;
        }

        .love-text {
            color: #ff69b4; /* Rosa fuerte para el texto */
            font-size: 8vw; /* Tamaño de fuente responsivo */
            font-weight: bold;
            text-align: center;
            white-space: nowrap; /* Evita que el texto se rompa */
            position: absolute;
            animation: moveText 15s linear infinite; /* Animación de movimiento */
            opacity: 0.8;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .heart {
            position: absolute;
            color: #ff4d6a; /* Rojo/rosa para los corazones */
            font-size: 3vw; /* Tamaño de corazón responsivo */
            animation: floatHeart 10s ease-in-out infinite;
            opacity: 0; /* Empiezan invisibles */
            pointer-events: none; /* Los corazones no interactúan con el ratón */
        }

        /* Animación para el texto "Te amo" */
        @keyframes moveText {
            0% { transform: translateX(100vw); } /* Empieza fuera de la pantalla por la derecha */
            100% { transform: translateX(-100vw); } /* Termina fuera de la pantalla por la izquierda */
        }

        /* Animación para los corazones flotantes */
        @keyframes floatHeart {
            0% {
                transform: translateY(0) scale(0);
                opacity: 0;
            }
            20% {
                transform: translateY(-20vh) scale(1.2);
                opacity: 1;
            }
            80% {
                transform: translateY(-80vh) scale(0.8);
                opacity: 0.5;
            }
            100% {
                transform: translateY(-100vh) scale(0);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="love-text">Te amo ❤️ Te amo ❤️ Te amo ❤️</div>

    <script>
        const body = document.body;

        // Función para crear un corazón y añadirlo al DOM
        function createHeart() {
            const heart = document.createElement('div');
            heart.classList.add('heart');
            heart.innerHTML = '❤️'; // Unicode del corazón

            // Posición aleatoria en el eje X
            heart.style.left = Math.random() * 100 + 'vw';
            // Duración de la animación aleatoria para que no todos aparezcan a la vez
            heart.style.animationDuration = (Math.random() * 5 + 5) + 's';
            // Retraso de la animación para que aparezcan en diferentes momentos
            heart.style.animationDelay = (Math.random() * 5) + 's';

            body.appendChild(heart);

            // Eliminar el corazón después de que termine su animación para no acumular elementos
            heart.addEventListener('animationend', () => {
                heart.remove();
            });
        }

        // Crear corazones a intervalos regulares
        setInterval(createHeart, 300); // Crea un corazón cada 300 milisegundos

        // Duplicar el texto "Te amo" varias veces para la animación de movimiento infinito
        const loveTextDiv = document.querySelector('.love-text');
        const originalText = loveTextDiv.textContent;
        for (let i = 0; i < 10; i++) { // Duplicar 10 veces para que siempre haya texto en pantalla
            loveTextDiv.textContent += originalText;
        }

        // Ajustar la velocidad del texto para que no se vea cortado si la pantalla es muy grande
        window.addEventListener('resize', () => {
            const textWidth = loveTextDiv.scrollWidth;
            const screenWidth = window.innerWidth;
            const duration = (textWidth / screenWidth) * 5; // Ajustar la duración en función del ancho del texto
            loveTextDiv.style.animationDuration = Math.max(15, duration) + 's'; // Mínimo 15s
        });
        window.dispatchEvent(new Event('resize')); // Disparar el evento al cargar la página
    </script>
</body>
</html>
