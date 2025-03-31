Preguntas del taller
Estudiante : Jhonatan Steven Baron Suarez

1. ¿Cómo detecta Traefik los servicios configurados en Docker Compose?

La herramienta utiliza lo que se encuentra como docker provider para descubrir dinámicamente los servicos que se están ejecutando en Docker;
con esto se entiende que Traefik se conecta  con el socket de Docker y lee los labels que se definen en los archivos docker-compose.yml 
de nuestros servicios. Los lables añ igual  indican a Traefik cómo enrutar el tráfico a cada servicio.
es decir que  se escuchan los eventos de Docker y posteriormente se utilizan dichos labels para configurar de forma automática
las  rutas y servicios.

2. ¿Qué rol juegan los middlewares en la seguridad y gestión del tráfico?

Los middlewares son intemediarios que permiten modificar la actividad  entrante y saliente en un software a modo de un filtro. y son muy importantes
en la seguridad de un programa  asi como tambien en la gestion del trafico dado el mismo.
Dentro de sus particularidades sepuede encontrar que permiten implementar autenticación como con Traefik y el basicAuth, tambien dejan Limitar la tasa de solicitudes o rate limit,
gestionar redirecciones http a https; asi como permiten hacer la misma gestión de tráfico y/o balanceo de carga.


3. ¿Cómo se define un router en Traefik y qué parámetros son esenciales?

Segun la documentación de traefik se entiende que funciona tipo como un dispositivo de borde, es decir que permite gestionar cómo se enrutan las solicitudes entrantes a los servicios.
el mismo router se  define mediante etiquetas en los servicios de Docker-compose.yml o en archivos de configuración dinámica.
Dentro de los  parámetros encontramos que rule define la regla con la cual el router se active por ejemplo, Host(\serviciocreado.com`)`).y service que especifica
el nombre del servicio al que se debe enviar el tráfico además de los entrypoints que definen los puntos de entrada o puertos por los que el router escucha las solicitudes.

4. ¿Cuál es la diferencia entre un router y un servicio en Traefik?

Router: Este puede indicar a qué servicio se debe enviar una petición entrante, basándose en reglas definidas.
Servicio: Es el que nos representa la instancia de una aplicación que está ejecutándose por ejemplo  en Docker, osea es el destino final al que el router envía el tráfico.


5. ¿Cómo se pueden agregar más reglas de enrutamiento para diferentes rutas?

Las reglas de enrutamiento se pueden agregar usando : traefik.http.routers.<nombre>.rule dentro de los servicios del Docker-compose. dentro de los ejemplos es entendible que
se pueden combinar múltiples reglas usando operadores lógicos como && (AND) y || (OR).
como por ejemplo :

######
labels:
  - "traefik.http.routers.mi-router.rule=Host(\`serviciocreado.com\`) && PathPrefix(\`/api\`)""
######
donde en el ejemplo se entiende que se enrutaran las solicitudes a serviciocreado.com/api 
