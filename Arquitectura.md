

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

