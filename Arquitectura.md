

# Documento de Arquitectura del Sistema de Gestión de Órdenes y Entregas

## 1. Introducción  
Este documento describe la arquitectura inicial del sistema de gestión de órdenes y entregas, incluyendo requisitos funcionales, requisitos de calidad y restricciones clave que deben ser consideradas en el diseño del software.

**Equipo:** _02_ 

**Integrantes:** 
 - *Bernal Londoño Pedro - 2259548*
 - *López Ramírez Jota - 2259394*
 - *Martinez Murillo Alejandro - 2259565*
 - *Reyes Rodriguez Santiago - 2259738*
 - *Rivas Guzmán Esmeralda - 2259580*
 
**Fecha:** _[20/02/2025]_  

---

## 2. Requisitos Funcionales  
Los requisitos funcionales se presentan en forma de **historias de usuario**, especificando los **criterios de aceptación**.

### **Historias de Usuario**
| **ID**    | **Historia de Usuario**                                                                                                           | **Criterios de Aceptación**                                                                                                                                                                                                                                                                                            |
| --------- | --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **US-01** | Como cliente registrado, quiero iniciar sesión en la plataforma para acceder a mi historial de pedidos y realizar nuevas compras. | - El usuario debe ingresar un correo y contraseña válidos.<br>- Si las credenciales son correctas, el usuario es redirigido a su perfil.<br>- Si las credenciales son incorrectas, se muestra un mensaje de error sin revelar detalles específicos.<br>- El usuario puede solicitar un restablecimiento de contraseña. |
| **US-02** | Como cliente registrado, quiero realizar el pago de mi pedido de forma segura para completar mi compra. | - El sistema debe integrarse con un simulador de pagos para procesar transacciones.<br>- El cliente debe poder seleccionar métodos de pago.<br>- Si el pago es exitoso, se debe generar una orden de compra y enviar una confirmación al cliente.<br>- Si el pago falla, se debe mostrar un mensaje de error y permitir reintentar el pago.  |
| **US-03** | Como cliente registrado, quiero hacer seguimiento en tiempo real de mi pedido, para conocer el estado y la ubicación de mi entrega durante el proceso. | <br>- El usuario accede a una sección de seguimiento desde su perfil o historial de pedidos. <br>- Se muestra el estado actualizado del pedido (Procesando, enviado, en tránsito, entregado). <br>- Se integra un mapa que muestra la ubicación aproximada del repartidor en tiempo real. <br>- El sistema notifica al usuario si hay retrasos o incidentes en la entrega. <br>- Se ofrece la opción de contactar al repartidor o servicio al cliente en caso de inconvenientes o dudas.| 
| **US-04** | Como administrador del sistema, quiero asignar pedidos a repartidores disponibles para asegurar que las entregas se realicen de manera eficiente y puntual. | <br>- El administrador debe poder ver una lista de repartidores disponibles, incluyendo su ubicación actual y estado. <br>- La lista debe actualizarse en tiempo real para reflejar cambios en el estado de los repartidores. <br>- El administrador debe poder asignar manualmente pedidos a los repartidores disponibles. <br>- El sistema debe mostrar un mensaje de confirmación una vez que el pedido haya sido asignado correctamente.| 
| **US-05** | Como cliente, quiero registrarme y autenticarme en el sistema para poder realizar compras. | <br>- Se debe disponer de un formulario de registro que solicite datos obligatorios (nombre, correo electrónico, contraseña, etc.). <br>- El sistema debe validar los datos ingresados. <br>- Una vez registrado, el cliente debe poder iniciar sesión con sus credenciales. <br>- Se mostrarán mensajes de error claros si los datos son inválidos o si el correo ya está registrado.|
| **US-06** | Como cliente, quiero buscar y ver productos disponibles para encontrar rápidamente lo que necesito. | <br>- El sistema debe contar con un campo de búsqueda que acepte palabras clave. <br>- Se deben ofrecer filtros (por categoría, rango de precio, etc.) y opciones de ordenamiento (por precio, orden alfabético, etc.). <br>- Los resultados deben mostrar imagen, nombre, precio y disponibilidad de cada producto. <br>- El cliente debe poder acceder a una página de detalle con descripción completa y características.|
| **US-07** | Como cliente, quiero gestionar mi carrito de compras para agregar, modificar o eliminar productos antes de confirmar mi pedido. | <br>- Desde la página de detalle del producto, el cliente debe poder agregar productos al carrito. <br>- La vista del carrito debe mostrar el listado de productos, cantidades, precios individuales y el total actualizado en tiempo real. <br>- Se deben ofrecer opciones para modificar la cantidad de cada producto o eliminarlos del carrito. <br>- Debe existir un botón claro para proceder al proceso de pago.|
| **US-08** | Como cliente, quiero consultar el historial de mis pedidos para revisar mis compras anteriores y acceder a los detalles de cada orden. | <br>- En la sección de "Mis pedidos" se debe listar todo el historial con fecha, estado, monto y número de orden. <br>- Al seleccionar un pedido, se mostrará la información completa (productos, dirección de entrega, método de pago, etc.). |
| **US-09** | Como cliente, quiero gestionar mi perfil y mis direcciones de envío para agilizar futuras compras. | <br>- Se debe disponer de una sección de perfil donde el cliente pueda ver y editar sus datos personales (correo, teléfono). <br>- El sistema debe permitir agregar, editar y eliminar direcciones de envío. <br>- Cada cambio debe confirmarse mediante mensajes de éxito o error, validando la información ingresada. <br>- Los datos sensibles deben manejarse de forma segura, cumpliendo con estándares de seguridad.|
| **US-10** | Como cliente, quiero recibir notificaciones sobre el estado de mi pedido y cambios relevantes para estar informado en todo momento. | <br>- El sistema debe enviar notificaciones en tiempo real o vía correo electrónico ante eventos importantes (pedido confirmado, enviado, retrasado, entregado). <br>- Las notificaciones deben mostrarse también en un panel de alertas dentro del perfil del cliente. <br>- Cada notificación debe incluir información relevante, como número de orden, estado y fecha estimada de entrega.|
| **US-11** | Como cliente, quiero acceder fácilmente a la información de políticas de privacidad, términos de uso y garantías, para conocer mis derechos y cómo se gestionan mis datos. | <br>- Las políticas y términos deben estar disponibles a través de enlaces visibles en la plataforma, especialmente durante el proceso de registro y en el pie de página. <br>- La información debe estar redactada de forma clara y comprensible. <br>- Se debe solicitar la aceptación de estas condiciones en el registro o al momento de realizar acciones críticas (como la compra). |
| **US-12** | Como administrador, quiero poder agregar nuevos productos al sistema, para mantener actualizado el inventario de productos. | <br>- El administrador puede ingresar un nombre, descripción, precio, categoría y cantidad del producto. <br>- El sistema valida los campos obligatorios. <br>- No se deben permitir productos duplicados. <br>- Al crear un producto, el sistema muestra un mensaje de éxito y el producto se guarda en la base de datos. <br>- El producto es visible y accesible para otras funciones del sistema. |
| **US-13** | Como administrador, quiero poder ver una lista de todos los productos y sus detalles, para consultar la información del inventario. | <br>- El administrador puede buscar productos por nombre, categoría o ID. <br>- El sistema muestra la lista de productos con su nombre, precio,categoría, cantidad disponible y descripción. <br>- Se permite filtrar productos por categoría, nombre o disponibilidad. |
| **US-14** | Como administrador, quiero poder actualizar la información de un producto, para mantener actualizados los detalles de los productos en el sistema. | <br>- El administrador puede actualizar el nombre, precio, descripción, categoría y cantidad de un producto. <br>- El sistema valida que los datos ingresados sean correctos. <br>- El administrador puede guardar los cambios y recibir una confirmación de que se han actualizado correctamente. <br>- El producto actualizado está disponible para otras funciones del sistema. |
| **US-15** | Como administrador, quiero poder eliminar un producto del sistema, para mantener el inventario limpio de productos descontinuados. | <br>- El administrador puede seleccionar un producto y eliminarlo. <br>- El sistema solicita confirmación antes de proceder con la eliminación del producto. <br>- Al eliminar un producto, el sistema lo elimina permanentemente de la base de datos. <br>- El administrador recibe un mensaje de éxito después de eliminar el producto. <br>- El producto eliminado ya no está disponible en el inventario ni en otras funcionalidades del sistema. |
| **US-16** | Como administrador, quiero poder categorizar los productos, para organizar el inventario y facilitar la búsqueda de productos. | <br>- El administrador puede crear nuevas categorías para los productos. <br>- El administrador puede asignar productos a una o más categorías. <br>- El sistema permite visualizar todos los productos en una categoría específica. <br>- Los productos pueden ser filtrados por categoría. <br>- El administrador puede editar o eliminar una categoría. |
| **US-17** | Como administrador, quiero poder ver todas las órdenes realizadas en el sistema, para tener un registro completo de las transacciones. | <br>- El administrador puede ver una lista de todas las órdenes realizadas, con detalles como el ID de la orden, cliente, productos adquiridos, cantidad y precio total. <br>- Se debe permitir filtrar las órdenes por fecha o estado. |
| **US-18** | Como administrador, quiero poder ver el estado de las entregas en tiempo real, para monitorear el progreso de los envíos. | <br>- El administrador puede ver una lista de todas las entregas con su estado actual. <br>- Se debe permitir filtrar las entregas por estado. |
| **US-19** | Como administrador, quiero poder ver métricas de rendimiento del sistema, para monitorear su eficiencia. | <br>- El administrador puede ver métricas como el tiempo de respuesta y la disponibilidad del sistema. <br>- Se deben generar alertas si alguna métrica muestra un rendimiento por debajo de los estándares definidos. |
| **US-20** | Como repartidor, quiero poder registrarme en el sistema, para tener acceso a las funcionalidades de entrega. | <br>- El repartidor puede ingresar su nombre, dirección de correo electrónico, número de teléfono y una contraseña para registrarse. <br>- El sistema debe validar que el correo electrónico sea único y esté en formato válido. <br>- El sistema guarda correctamente los datos de registro en la base de datos. <br>- Después de la verificación, el repartidor puede iniciar sesión con sus credenciales. |
| **US-21** | Como repartidor, quiero poder iniciar y cerrar sesión en el sistema, para acceder a las órdenes asignadas. | <br>- El repartidor puede iniciar sesión utilizando su correo electrónico y contraseña. <br>- El sistema valida que las credenciales sean correctas antes de permitir el acceso. <br>- Si las credenciales son incorrectas, el sistema muestra un mensaje de error y permite intentarlo nuevamente. <br>- El repartidor puede cerrar sesión en cualquier momento, lo que lo redirige a la página de inicio de sesión. |
| **US-22** | Como repartidor, quiero ver las órdenes asignadas, para poder entregarlas de manera eficiente. | <br>- El repartidor puede acceder a una lista de las órdenes asignadas con detalles como el ID de la orden, cliente, productos y dirección de entrega. <br>- Las órdenes se muestran en orden cronológico o de prioridad según el sistema. <br>- La lista debe actualizarse automáticamente cuando se asignan nuevas órdenes. |
| **US-23** | Como repartidor, quiero poder actualizar el estado de las entregas, para informar al sistema y al cliente sobre el progreso. | <br>- El repartidor debe poder cambiar el estado de una orden (En camino, Entregada, No entregada). <br>- El sistema debe actualizar automáticamente el estado de la orden. <br>- El repartidor puede ver el historial de las órdenes entregadas. <br>- El sistema debe notificar al cliente cuando el estado de la entrega cambie. |



>  **Instrucciones:**  
> - Completar al menos **tres historias de usuario**.  
> - Asegurar que cada historia tenga criterios de aceptación claros y verificables.  

---

## 3. Requisitos de Calidad  
Los requisitos de calidad se presentan en forma de **historias de calidad**, siguiendo la estructura de Len Bass.

### **Historias de Calidad**
| **ID**   | **Fuente** | **Estímulo** | **Artefactos** | **Entorno** | **Respuesta** | **Medida de Respuesta** |
|----------|-----------|-------------|---------------|------------|-------------|-----------------|
| **RQ-01** | Desarrollador | Se solicita modificar la lógica de asignación de pedidos para incluir nuevos criterios de prioridad. | Código y configuración de reglas de negocio. | Tiempo de ejecución | Se debe modificar, probar y desplegar la nueva lógica de asignación. | El esfuerzo requerido no debe superar 2 horas de trabajo y no deben generarse más de 2 defectos nuevos. |
| **RQ-02** | Usuario | Se solicita el pedido de un producto en la plataforma. | Sistema de compra | Tiempo de ejecución | Se debe registrar la orden de compra y notificar al usuario la acción |  El esfuerzo requerido no debe superar los 600 milisegundos. |
| **RQ-03** | Repartidor | Se visualiza la ruta de entrega en tiempo real. | API de geolocalización | Conexión a internet inestable | Se debe alertar al repartidor sobre los problemas de conexión, mantener visible la ruta y reintentar la conexión. | El esfuerzo requerido no debe superar los 3 segundos para generar la alerta. Además, la API debe garantizar la disponibilidad con una conexión inestable.  | 
|**RQ- 04** | Administrador | Se agregan nuevos productos a la plataforma. | Sistema de productos e inventario | Tiempo de ejecucion | Se debe alertar al administrador sobre los cambios realizados y actualizar el stock con los nuevos productos ingresados | El esfuerzo requerido no debe superar los 600 milisegundos  |

>  **Instrucciones:**  
> - Completar al menos **tres historias de calidad**, alineadas con atributos clave como **rendimiento, escalabilidad y seguridad**.  
> - Definir cómo se medirá la respuesta esperada ante la situación planteada.  

---

## 4. Restricciones del Sistema  
Las restricciones establecen **limitaciones** en la arquitectura del sistema, ya sean tecnológicas, de negocio, regulatorias o de infraestructura.

### **Lista de Restricciones**
| **Tipo de Restricción** | **Descripción** |
|------------------------|----------------|
| Tecnológica | El sistema debe desarrollarse utilizando **Spring Boot y PostgreSQL**, debido a la infraestructura actual de la empresa y su compatibilidad con otros sistemas internos. |
| Tecnológica |  Se debe utilizar OAuth2 y JWT para la validación de identidad. |
| De infraestructura | El sistema debe desplegarse en AWS utilizando contenedores Docker y Kubernetes, garantizando escalabilidad y alta disponibilidad.|

>  **Tipos de restricciones:**  
> - **Tecnológicas:** Lenguajes, frameworks o herramientas que deben utilizarse.  
> - **De negocio:** Normativas o estándares de la empresa.  
> - **Regulatorias:** Cumplimiento de normativas legales o de seguridad.  
> - **De infraestructura:** Limitaciones en hardware, red o almacenamiento.  


---

## 5. Formato de Entrega  
- **Formato:** Markdown (`.md`) en el repositorio de Codelabs, El documento debe llamarse `Arquitectura.md`.  
- **Extensión máxima:** 3 páginas.  

---

## **Tiempo estimado para completar el ejercicio: 50 minutos**  
**15 min** → Definir **3 historias de usuario con criterios de aceptación**.  
**15 min** → Definir **3 historias de calidad alineadas con atributos clave**.  
**10 min** → Identificar **2 restricciones relevantes**.  
**10 min** → Revisión y ajustes finales del documento.  

