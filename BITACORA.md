## P0
Mi predicción:
Cuando abro una página en el navegador, el cliente es el navegador porque es quien realiza la petición. El servidor es el programa que está ejecutándose y recibe esa petición. En la entrada viajan datos como el método de la petición, la URL y los headers, y en algunos casos también un body. En la salida el servidor envía una respuesta que contiene un código de estado, headers y un body con información como texto, JSON o HTML.
Lo que pasó:
Al abrir una página, el navegador realizó una petición al servidor y el servidor procesó esa petición y devolvió una respuesta que el navegador pudo mostrar.
Por qué pasó:
Porque el funcionamiento de un servidor web sigue el modelo Entrada → Proceso → Salida. La petición es la entrada, el código del servidor procesa lo recibido y la respuesta es la salida.


## P1
Mi predicción:
Creo que al abrir /, /hola y /lo-que-sea voy a recibir la misma respuesta: Hola desde el servidor.
Lo que pasó:
En las tres direcciones recibí la respuesta Hola desde el servidor.
Por qué pasó:
Porque en este momento el servidor no tiene diferentes condiciones para distinguir las rutas. Cada vez que recibe una petición ejecuta res.end('Hola desde el servidor'), sin importar cuál sea la URL solicitada.


## P2
Mi predicción:
Creo que al abrir una sola página aparecerá una línea en la terminal indicando que llegó una petición, mostrando también el método y la URL solicitada.
Lo que pasó:
Al abrir la página apareció en la terminal una línea indicando la petición realizada, por ejemplo Llegó una petición: GET /. La URL que apareció correspondió a la página que solicité.
Por qué pasó:
Porque la función que recibe las peticiones se ejecuta cada vez que llega una petición al servidor y el console.log muestra el método y la URL de esa petición.


## P3
Mi predicción:
Si solicito /actividades/ con el slash al final, creo que el servidor responderá Ruta no encontrada con código 404. Si solicito /ACTIVIDADES, también creo que responderá Ruta no encontrada con código 404.
Lo que pasó:
Al solicitar /actividades/ recibí Ruta no encontrada con código 404. Al solicitar /ACTIVIDADES también recibí Ruta no encontrada con código 404.
Por qué pasó:
Porque el servidor solamente tiene programada exactamente la ruta GET /actividades. La comparación de la URL distingue tanto el slash adicional al final como las letras mayúsculas y minúsculas. Por eso /actividades/ y /ACTIVIDADES no coinciden con /actividades y entran en la condición else, donde se establece el código 404.


Reflexión — Servidor sin Express
Una de las cosas tediosas fue tener que comparar manualmente el método y la URL utilizando condiciones como if y else if para decidir qué respuesta enviar.
Otra cosa tediosa fue tener que configurar manualmente la respuesta JSON, porque fue necesario establecer el header Content-Type y utilizar JSON.stringify() para convertir los datos a texto.
También fue frágil tener que programar manualmente las rutas que no existen y el código 404, porque debemos asegurarnos de que todas las posibilidades estén contempladas para devolver una respuesta correcta.


## P4

Mi predicción:
Creo que Express va a responder con un código de estado 404 (Not Found) cuando solicite la ruta /no-existe, porque en el código no se ha creado ninguna ruta para esa dirección.

Lo que pasó:
Al ingresar a http://localhost:3000/no-existe y revisar la pestaña Red/Network de las herramientas de desarrollador, Express respondió con el código de estado 404.

Por qué pasó:
Pasó porque Express no encontró una ruta que coincida con /no-existe. Cuando una ruta no está programada, Express responde automáticamente con 404, indicando que el recurso o la ruta solicitada no fue encontrada.


## P5 

Mi predicción:
Creo que el navegador se va a quedar cargando y no va a recibir ninguna respuesta, porque al comentar next(); la petición no podrá continuar hacia la ruta /.

Lo que pasó:
Al comentar next(); y solicitar /, el navegador se quedó cargando y no mostró la respuesta de “API Aventuras San Gil funcionando”. En la terminal sí apareció el registro del middleware con la hora, el método GET y la ruta /.

Por qué pasó:
Pasó porque next() permite que la petición continúe hacia el siguiente middleware o hacia la ruta correspondiente. Al quitarlo, la petición queda detenida en ese middleware y nunca llega a app.get('/').