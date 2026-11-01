
# MEMORIA TÉCNICA
# TORNEO ZONE

**Aplicación móvil para crear, organizar y participar en torneos de videojuegos y juegos de cartas**

**Proyecto Intermodular — Desarrollo de Aplicaciones Multiplataforma (DAM)**

**Integrantes:**
- Pablo Jose Rico Mejia
- Jose Patricio Galan Rodriguez
- Nicolas Safonov Gusev

---

# Capítulo 1: Introducción

## 1.1. Presentación del Problema y Justificación

Los videojuegos y las competiciones organizadas en torno a ellos constituyen un ámbito de ocio digital con una comunidad amplia. Según la Asociación Española de Videojuegos (AEVI), durante 2024 el mercado español del videojuego alcanzó una facturación de 2.408 millones de euros y reunió aproximadamente a 22,1 millones de jugadores; alrededor del 45 % de la población española jugaba a videojuegos [1]. Estas cifras muestran la dimensión social y económica del sector y justifican explorar herramientas digitales que faciliten la organización de actividades competitivas para sus comunidades.

En paralelo, los torneos de videojuegos y de juegos de cartas pueden organizarse mediante una combinación de mensajería instantánea, redes sociales, hojas de cálculo y comunicaciones directas. Aunque estas herramientas resuelven tareas puntuales, mantener la información repartida puede dificultar el seguimiento de las inscripciones, la consulta de las normas, la preparación de los emparejamientos y la actualización de los resultados. En grupos pequeños, parte de estas tareas suele depender del trabajo manual de la persona organizadora.

La necesidad identificada no consiste únicamente en publicar un evento, sino en disponer de un flujo común que relacione los datos del torneo, sus participantes, las rondas y los resultados. Desde el punto de vista técnico, esto requiere un modelo de datos coherente, validaciones para evitar inscripciones duplicadas o superar el límite de plazas, control de permisos según el rol del usuario y una lógica de competición que actualice correctamente los enfrentamientos tras registrar cada resultado.

Por ello se propone desarrollar **Torneo Zone**, una aplicación móvil Android que centralice las operaciones esenciales de un torneo en una única plataforma. La aplicación busca reducir la dispersión de información y el trabajo administrativo, mejorar la consulta del estado de cada competición y ofrecer una experiencia sencilla tanto a participantes como a organizadores.

La propuesta abarca juegos de cartas y videojuegos; el MVP se limitará a un conjunto controlado de funciones para poder implementar y validar la solución dentro del alcance del proyecto.

## 1.2. Objetivos del Proyecto

### 1.2.1. Objetivo General

Diseñar, desarrollar y validar una aplicación móvil Android denominada **Torneo Zone** que permita a los usuarios registrarse, crear y descubrir torneos de juegos de cartas y videojuegos, inscribirse en ellos y gestionar sus enfrentamientos y resultados desde una plataforma centralizada, utilizando Kotlin, Jetpack Compose, una arquitectura MVVM y servicios de backend con Firebase SQL Connect y PostgreSQL.

### 1.2.2. Objetivos Específicos (Criterios SMART)

1. **OE-01 (Interfaz y usabilidad):** Implementar, antes de finalizar la fase de desarrollo del MVP, las pantallas de registro/inicio de sesión, perfil, listado y detalle de torneos, inscripción y seguimiento de enfrentamientos mediante Kotlin y Jetpack Compose. Las funciones principales deberán poder recorrerse en pruebas funcionales sin bloqueos y con mensajes claros ante errores de validación. Se aplicarán buenas prácticas de accesibilidad: etiquetas comprensibles, contraste suficiente, tamaños de texto legibles y controles táctiles adecuados.

2. **OE-02 (Persistencia e integridad de datos):** Definir e implementar el modelo relacional en PostgreSQL y su acceso mediante Firebase SQL Connect antes de integrar todas las pantallas. El modelo representará, como mínimo, usuarios, torneos, inscripciones, enfrentamientos y resultados. Las pruebas verificarán que se rechazan inscripciones duplicadas, no se supera la capacidad máxima y los cambios se conservan al volver a consultar los datos.

3. **OE-03 (Servicios y seguridad):** Incorporar autenticación de usuarios y autorización por roles de participante, organizador y administrador en el MVP. Antes de la entrega, se comprobará que un usuario no autenticado no puede realizar operaciones reservadas y que un participante no puede modificar torneos ni resultados ajenos.

4. **OE-04 (Gestión de torneos y enfrentamientos):** Desarrollar, antes de la validación final, el flujo de creación de torneos, inscripción, generación de emparejamientos, registro de resultados y actualización de clasificación. La primera versión utilizará eliminación directa. Se probarán torneos con distintas cantidades de participantes, incluidos números impares, para verificar que no se crean enfrentamientos duplicados y que el ganador avance correctamente.

5. **OE-05 (Verificación y entrega):** Ejecutar antes de la entrega pruebas funcionales documentadas para los cinco casos de uso prioritarios (CU-01 a CU-05), registrando resultado esperado, resultado obtenido y defectos detectados. El objetivo se considerará alcanzado cuando los casos críticos de acceso, inscripción, creación de torneo y registro de resultados superen las pruebas de aceptación definidas por el equipo.

## 1.3. Descripción de la Solución Propuesta y Propuesta de Valor

Torneo Zone será una aplicación móvil orientada a centralizar la creación, organización y participación en torneos de juegos de cartas y videojuegos.

Los usuarios podrán registrarse, acceder a su perfil y consultar las competiciones disponibles. Cada torneo incluirá información como nombre, juego, modalidad, fecha, reglas, formato y número máximo de participantes.

Los organizadores podrán crear y gestionar sus torneos, revisar las inscripciones, generar los enfrentamientos y registrar los resultados.

Los participantes podrán consultar la información del evento, inscribirse cuando las plazas estén disponibles, visualizar sus enfrentamientos, registrar el resultado de su enfrentamiento y seguir la evolución de la competición hasta conocer al ganador.

El sistema distinguirá los permisos según el rol del usuario para evitar que participantes sin autorización modifiquen la configuración o los resultados de otros participantes.

La solución automatiza o centraliza tareas que, en una organización manual, pueden depender de mensajes, listas independientes o cálculos realizados por el organizador:

- Control de plazas.
- Relación entre participantes y torneos.
- Creación del cuadro de enfrentamientos.
- Almacenamiento de resultados.
- Actualización de la clasificación.

La propuesta de valor consiste en ofrecer un punto de acceso único, disponible desde el móvil, con información estructurada y un flujo de trabajo consistente.

## 1.4. Alcance y Límites del Sistema

El alcance inicial se define mediante un **Producto Mínimo Viable (MVP)**.

Se priorizan las funciones indispensables para completar el ciclo principal de una competición, desde el acceso del usuario hasta la publicación del ganador.

Esta decisión permite limitar la complejidad, comprobar primero los riesgos técnicos y entregar una versión evaluable dentro del calendario académico.

### Funciones incluidas en el MVP (Must Have)

- **CU-01.** Registro, inicio de sesión y perfiles, con separación de permisos por rol.

- **CU-02.** Creación y gestión básica de torneos, con nombre, juego, modalidad, fecha, reglas, formato y límite de participantes.

- **CU-03.** Exploración, consulta, filtrado e inscripción en torneos, con validación de plazas y prevención de inscripciones duplicadas.

- **CU-04.** Generación automática de enfrentamientos; inicialmente se priorizará la eliminación directa y se contemplará la gestión de participantes impares.

- **CU-05.** Registro y validación de resultados, avance de ganadores, visualización del cuadro y determinación del ganador final.

### Funciones fuera del alcance inicial o aplazadas (Could Have / Won't Have en el MVP)

- Chat interno y mensajería entre participantes.
- Notificaciones push avanzadas y recordatorios automáticos.
- Formatos complejos como ligas, grupos, sistema suizo o torneos con múltiples fases.
- Estadísticas avanzadas, perfiles competitivos ampliados y analítica histórica.
- Función de guardado de listas de equipos o barajas para torneos con OTS.

La priorización se basa en el método **MoSCoW**.

Las funciones **Must Have** son necesarias para demostrar el objetivo principal del proyecto.

Las **Should Have** podrán incorporarse si las tareas esenciales están terminadas y probadas.

Las **Could Have** se reservan para una ampliación posterior, ya que aumentan el trabajo de diseño, integración o pruebas.

Las **Won't Have** de esta versión se excluyen expresamente para no comprometer la estabilidad ni el calendario del MVP.

Entre los límites conocidos se encuentran la dependencia de la conectividad para consultar y actualizar los datos remotos, la necesidad de configurar correctamente los permisos de acceso y el hecho de que la primera versión se centrará en torneos gestionados dentro de la aplicación, sin conexión automática con los servidores de los videojuegos ni verificación externa de los resultados.

---

# Capítulo 2: Antecedentes y Estado del Arte

## 2.1. Revisión de Sistemas Existentes

### 2.1.1. Challonge

**Tipo:** Comercial SaaS / Suscripción mensual o anual.

**Plataforma:** Web.

**URL oficial:** https://challonge.com/

Challonge es una plataforma referente en el sector que permite crear páginas de torneos, gestionar participantes y resultados y trabajar con formatos de eliminación simple, doble eliminación, todos contra todos y formato suizo.

Entre sus fortalezas destacan la madurez funcional y la variedad de formatos.

Como limitaciones en comparación a nuestra propuesta, es una plataforma externa con una experiencia y un modelo de servicio propios y no una aplicación Android desarrollada específicamente para las necesidades de los participantes de torneos más pequeños como es nuestra propuesta [2].

### 2.1.2. Bracket

**Tipo:** Open source (AGPL-3.0).

**Plataforma:** Web.

**URL oficial:** https://docs.bracketapp.nl/

Bracket es una aplicación web de código abierto que permite la creación de torneos, la incorporación de formatos de equipos y jugadores, la elección de formatos como eliminación, sistema suizo o todos contra todos, la planificación de partidos y la publicación de resultados y clasificaciones.

Su fortaleza es ofrecer funciones competitivas amplias y una orientación al control de la propia solución.

La limitación para TNZ es que su propuesta está organizada como aplicación web, mientras que TNZ se plantea como cliente Android nativo [3].

### 2.1.3. Método manual

**Tipo:** Método manual apoyado en hojas de cálculo.

**Plataforma:** Ordenador o móvil.

Este método permite registrar participantes, preparar emparejamientos y publicar resultados sin desarrollar una aplicación especializada.

Sin embargo, exige que una persona mantenga los datos, actualice el cuadro y comunique los cambios.

Si varias copias circulan a la vez, pueden aparecer versiones contradictorias, inscripciones duplicadas o errores al avanzar de ronda.

El ejemplo que he utilizado para realizar la comparativa es el torneo OWC 2026 del videojuego Osu! [4].

## 2.2. Análisis Comparativo (Benchmarking)

| Criterio | Challonge | Bracket | Método manual | Torneo Zone |
|---|---|---|---|---|
| Plataforma | Web | Web | Hoja de cálculo de Google | Android (Kotlin + Compose) |
| Coste de licencia | Nivel gratuito con publicidad + planes de pago | Gratuito y open source (AGPL-3.0) | Gratuito | Sin licencia comercial prevista |
| Rendimiento | Medio (depende de la conexión a Internet) | Rápido (depende del despliegue) | Medio (con grandes volúmenes de datos no es viable) | Alto (Kotlin + Compose) |
| Persistencia | Sí (Cloud) | Sí (Postgres) | No | PostgreSQL |
| Accesibilidad | No implementada | No implementada | Nula | Accesibilidad prevista según WCAG 2.1 |
| Informes PDF | Sí (descarga SVG) | No | Manual | No prevista en MVP |
| Integración | Dispone de API para integrar y gestionar torneos desde aplicaciones externas | Permite utilizar sus funcionalidades dentro de su propio entorno | Manual | Firebase Data Connect y SDK Android previstos |

La comparación muestra que las soluciones existentes ya cubren una parte importante de la gestión de torneos.

Challonge destaca por su oferta de formatos y por integrar páginas de torneo, participantes y resultados.

Bracket ofrece una alternativa orientada a la gestión de cuadros y publicación de resultados.

Las hojas de cálculo pueden resolver torneos pequeños, pero requieren mantenimiento manual.

TNZ no pretende competir en amplitud funcional en su primera versión: busca ofrecer un flujo móvil cohesionado y centrarse en cinco casos de uso esenciales.

## 2.3. Justificación del Stack Tecnológico

### 2.3.1. Interfaz de usuario: Kotlin y Jetpack Compose

Queríamos que fuera una aplicación a la que todo el mundo pudiera acceder, por eso pensamos en una aplicación móvil y dado que, hoy en día, Kotlin con Jetpack Compose son los estándares recomendados por Google para el desarrollo nativo de aplicaciones Android, nos lanzamos a ello.

Kotlin [5] es un lenguaje de programación moderno de tipo estático que usan más del 60 % de los desarrolladores profesionales de Android, orientado a objetos y funcional, permite escribir lógica limpia y directa, con una fuerte seguridad contra nulos ya que te obliga a declarar explícitamente si una variable puede recibir null.

A su vez, Jetpack Compose [6] es un kit de herramientas moderno diseñado para simplificar el desarrollo de IU.

Combina un modelo de programación reactivo con la concisión y facilidad de uso del lenguaje de programación Kotlin.

Es totalmente declarativo, lo que significa que describes tu IU si llamas a una serie de funciones que transforman datos en una jerarquía de IU.

Cuando los datos subyacentes cambian, el framework vuelve a ejecutar estas funciones automáticamente y actualiza la jerarquía de la IU por ti.

### 2.3.2. Capa de Persistencia: PostgreSQL

PostgreSQL es la base de datos relacional de objetos de código abierto más avanzada del mundo.

Está diseñado para ofrecer un rendimiento de nivel empresarial y se valora por sus funciones sólidas y confiabilidad [7].

Hemos decidido SQL frente a NoSQL por la complejidad en las relaciones que tenemos que tratar.

Un usuario se inscribe a un equipo. Un equipo participa en un torneo. El torneo genera partidas (Matches), y cada partida vincula a dos equipos y produce un resultado.

Si intentas hacer esto en NoSQL, duplicarás tantos datos que, si un usuario cambia de equipo a mitad del torneo, podrías corromper todo el árbol de emparejamientos.

También necesitamos de cierta integridad transaccional.

Postgres asegura que la base de datos procese una operación a la vez de forma segura, evitando inscripciones duplicadas o resultados corruptos.

Con SQL también puedes calcular tablas de posiciones, diferencias de puntos o ratios de victoria con una sola consulta estructurada.

### 2.3.3. Capa de Backend y Servicios: Firebase Data Connect

Un torneo online también necesita ser dinámico.

Vamos a usar Firebase para reflejar en tiempo real el marcador en vivo de una partida, gestionar las alertas push, para avisar a los jugadores que la partida está a punto de comenzar, si el rival está listo o se han generado los brackets.

Y con Firebase Auth tenemos resuelto de manera sencilla el registro de usuarios, perfiles, login con Google, Apple o contraseñas [8].

Lo hemos elegido frente a Node.js o ASP.NET porque de esta forma nos ahorramos diseñar la arquitectura de red desde cero y gestionar manualmente la concurrencia y el estado de las conexiones de todos los participantes.

Y enfocados en el MVP, delegar sobre Firebase la autenticación nos permite liberarnos de una gran carga de trabajo en backend, permitiéndonos que nos centremos en otros requisitos funcionales de la aplicación.

### 2.3.4. Librerías y Servicios Auxiliares: Coil, Firebase Cloud Messaging (FCM), KotlinX Serialization, AndroidX Lifecycle y ViewModel

Coil [9] es una librería ligera desarrollada en Kotlin para cargar y mostrar avatares de usuarios o logotipos de juegos de forma asíncrona dentro de Jetpack Compose.

Con FCM gestionaremos las alertas push.

AndroidX Lifecycle y ViewModel permitirán aplicar correctamente el patrón MVVM y asegurar que los datos no se pierdan al girar la pantalla o cambiar de pestaña.

Kotlin Serialization se utilizará para parsear objetos JSON de forma nativa en Kotlin sin complicaciones.

---

# Referencias bibliográficas

**[1]** Asociación Española de Videojuegos (AEVI). "El sector del videojuego creció en 2024 con una facturación récord de más de 2.408 millones de euros y 22 millones de jugadores". 2025.

https://aevi.org.es/el-sector-del-videojuego-crecio-en-2024-con-una-facturacion-record-de-mas-de-2-408-millones-de-euros-y-22-millones-de-jugadores/

**[2]** Challonge. "Funciones de los torneos". Documentación de Challonge.

https://docs.challonge.com/es/features/tournaments

**[3]** Bracket. "Introduction". Bracket Documentation.

https://docs.bracketapp.nl/docs/

**[4]** OWC 2026. "OSU! World Cup 2026 | information". Hojas de cálculo de Google.

https://docs.google.com/spreadsheets/d/136yKaeBtlxHo7o7TQxHflLOw1T67ahn8vF2FTJ0IjFc/edit?gid=1075626328

**[5]** Kotlin. Documentación de Android Developers.

https://developer.android.com/kotlin?hl=es-419

**[6]** Jetpack Compose. Documentación de Android Developers.

https://developer.android.com/codelabs/jetpack-compose-basics?hl=es-419#0

**[7]** PostgreSQL. Google Cloud.

https://cloud.google.com/discover/what-is-postgresql?hl=es-419

**[8]** Firebase. Sngular.

https://www.sngular.com/es/insights/313/firebase

**[9]** Coil. Artículo sobre la biblioteca de carga de imágenes para Android.

https://dharmeshbasapati.medium.com/coil-the-modern-image-loading-library-for-android-8fab79638f05
