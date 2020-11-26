# Documentación del sistema

@TODO

# Cuellos de botella

Los cuellos de botella que creemos que pueden aparecer son:
- Capacidad del balanceador de carga, parece que AWS tiene un límite inicial de unas 15k peticiones por segundo.
- Capacidad de Redis. El límite de Redis parece estar en unas 800k peticiones por segundo.

#  Optimizaciones abordadas y futuras

Hemos optimizado el balanceo usando el servidor DNS. También podemos valorar usar Nginx que parece que podría llegar al millón de peticiones por segundo.

Otra optimización sería usar un cluster de servidores de Redis pero no conseguiríamos mejor rendimiento si tenemos que cumplir con que todos los turnos son secuenciales pues tendríamos que trabajar con lotes de turnos y sincronizar entre los servidores.

# Estrategia de escalado

La estrategia que nos parece más adecuada es escalar en base a la media de peticiones por segundo de nuestra arquitectura, cuando lleguemos al 80% del máximo teórico se añadiría una instancia nueva. Según nuestras pruebas un servidor de nuestra aplicación es capaz de servir unas 14k peticiones por segundo. Si tenemos dos servidores y llegamos a una media 22.4k peticiones por segundo durante 2 minutos (nuestro máximo serían 24k peticiones por segundo) añadiríamos una instancia nueva. Y desescalaríamos cuando el número medio de peticiones durante dos minutos baje al 40%, en nuestro ejemplo serían 11.2k peticiones por segundo.

Otra estrategia interesante es usar la latencia. Usando la latencia no tendríamos problema al combinar escalador vertical y escalado horizontal. Sabemos que una máquina más potente es capaz de hacer que nuestra aplicación aumente el número de peticiones por segundo que es capaz de servir. Esto nos obligaría a cambiar la estrategia de autoescalado basada en la media de peticiones por segundo cada vez que cambiemos el tipo de instancia de la flota. Si usamos la latencia desaparece este problema y nos permite combinar instancias de distinta potencia. 

Para usar el autoescalado basado en latencia tendríamos que hacer pruebas para ver cuál es la latencia natural de nuestra aplicación y cuál es la latencia máxima antes de saturar el sistema.
