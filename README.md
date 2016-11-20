#EventBus Android lib

EventBus es es una herramienta cuya finalidad es la de lanzar y capturar eventos entre diferentes clases. Está basada en el patrón bus de eventos y su implementación consiste en que uno o varios objetos se suscriben a un canal a través del cual escuchan, y otro, en el momento en el que suceda algo que desea notificar, lanza un evento a través de este canal y todos aquellos que estaban escuchando reaccionarán haciendo aquello que tenían programado al suscribirse a éste. EventBus no solo nos facilita la tarea de notificar a los suscriptores acerca del evento si no que nos permite enviar información asociada a ese evento a través del canal y decidir en qué hilo se ejecutará la respuesta.

###Ventajas y desventajas de EventBus

Un bus de eventos es una herramienta muy útil y potente, pero el abuso de esta forma de trabajar y las malas prácticas al hacer uso de esta herramienta pueden convertirla en un arma de doble filo.
* **Flexibilidad:** es algo que se intuye en el momento en el que comprendemos su funcionamiento. Con EventBus se pueden realizar numerosas funcionalidades, incluso generar toda una forma de trabajar basada en estos eventos. Sin embargo, esto puede ser contraproducente, ya que EventBus te permite abstraerte de las herramientas de paso de mensajes y de notificaciones que brinda Android y el lenguaje en general; y, si se abusa, se puede generar una fuerte dependencia de esta herramienta, pudiendo incluso convertirse en el núcleo de nuestra aplicación.

* **Simplicidad:** es una ventaja clara que nos brinda en este caso EventBus como herramienta, ya que en solo tres sencillos pasos ya podemos hacer uso de esta herramienta. En cualquier parte se llama al método post de la instancia de EventBus y se propaga un evento. En cualquier parte de la app nos suscribimos en el momento que deseemos y, generando un método con una simple anotación, reaccionamos a dicho evento especificando en qué hilo se da la respuesta.

* **Agilidad:** gracias a los beneficios mencionados anteriormente, ahorramos muchas líneas de código, clases y lógica de interacción que, al fin y al cabo, se traduce en un menor tiempo de desarrollo. Pero haciendo hincapié en lo anterior, lo que parece ahorrarnos trabajo de desarrollo, si no se hace correctamente y se abusa de ello, se puede convertir en tiempo de depuración; ya que, en el momento en el que algo falla, podríamos desear haberlo hecho de la otra forma.

###Ejemplo
```javascript
// Class is typically registered by the container.
class EventBusChangeRecorder {
  @Subscribe public void recordCustomerChange(ChangeEvent e) {
    recordChange(e.getChange());
  }
}
// somewhere during initialization
eventBus.register(new EventBusChangeRecorder());
// much later
public void changeCustomer() {
  ChangeEvent event = getChangeEvent();
  eventBus.post(event);
}
```
