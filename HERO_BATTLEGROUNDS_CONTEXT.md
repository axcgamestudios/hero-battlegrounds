# HERO BATTLEGROUNDS — CONTEXT & ASSET INTEGRATION GUIDE

**Repositorio de recursos:** https://github.com/axcgamestudios/hero-battlegrounds  
**Tipo de proyecto:** 3D Superhero Battleground Web  
**Motor gráfico previsto:** Three.js  
**Dirección artística:** AAA, cinematográfica, inspirada en Unreal Engine 5, Marvel's Spider-Man y The Strongest Battlegrounds.

---

# 1. OBJETIVO DEL DOCUMENTO

Este documento sirve como contexto permanente para cualquier IA que trabaje en Hero Battlegrounds.

Su objetivo es explicar cómo inspeccionar, organizar, importar y utilizar todos los recursos del repositorio, además de establecer cómo implementar:

- Personajes 3D.
- Modelos y escenarios.
- Objetos y decoración.
- Materiales y texturas.
- Efectos especiales (VFX).
- Animaciones de personajes.
- Animaciones de combate.
- Cutscenes cinematográficas.
- Cámaras dinámicas.
- Efectos de impacto y destrucción.

**IMPORTANTE:** El repositorio contiene recursos, no necesariamente todos los sistemas de programación del juego. La IA debe inspeccionar también el proyecto principal antes de implementar cualquier cosa.

# 2. ESTRUCTURA DEL REPOSITORIO

Repositorio:

https://github.com/axcgamestudios/hero-battlegrounds

La estructura de raíz identificada es:

```text
hero-battlegrounds/
│
├── buildings/
│
├── environment/
│
├── military/
│   └── kenney-desert-shooter-pack/
│
├── props/
│   └── kenney-city-kit-roads/
│
├── arkham_city_batman.glb
├── iron_man.glb
├── model.glb
├── spiderman_brand_new_day.glb
├── superman.glb
│
├── design-skill.md
├── README.md
└── .gitignore
```

La colección está basada en recursos de entornos urbanos y militares, incluyendo elementos de construcción, carreteras, vegetación, decoración y modelos 3D.

No se debe asumir que todos los archivos de las carpetas tienen el mismo formato.

La IA debe inspeccionar recursivamente las carpetas antes de integrarlas.

# 3. PERSONAJES 3D

En la raíz se identificaron estos modelos:

| Archivo | Peso identificado |
|---|---:|
| arkham_city_batman.glb | 7.71 MB |
| iron_man.glb | 11.6 MB |
| spiderman_brand_new_day.glb | 7.41 MB |
| model.glb | 1.91 MB |
| superman.glb | Pendiente de verificar |

Los modelos deben utilizarse como recursos visuales independientes.

## Inspección obligatoria

Antes de utilizar cada personaje, comprobar:

- Número de meshes.
- Materiales y texturas.
- Esqueleto y rig.
- Animaciones incluidas.
- Nombres de los clips.
- Escala y orientación.
- Dimensiones reales.
- Punto de origen.
- Bounding box.
- Peso total.

No asumir que un modelo incluye animaciones solamente porque es un personaje humanoide.

## Sistema de personajes

Cada personaje debe tener:

- Modelo 3D.
- Controlador de animaciones.
- Animación idle.
- Movimiento.
- Animaciones de ataque.
- Animaciones de daño.
- Animación de lanzamiento.
- Animación de caída.
- Animación de recuperación.
- Animación de muerte cuando corresponda.
- Efectos visuales propios.

Si no existen animaciones compatibles, buscar o crear animaciones apropiadas. No inventar clips inexistentes.

# 4. EDIFICIOS Y ENTORNOS

## buildings/

Utilizar esta carpeta para identificar piezas arquitectónicas.

Posibles funciones:

- Edificios.
- Fachadas.
- Paredes.
- Estructuras.
- Elementos modulares.
- Decoración urbana.

La IA debe identificar cada modelo real antes de asignarle una función.

## environment/

Inspeccionar los elementos ambientales y clasificarlos según su contenido real.

Categorías sugeridas:

- Vegetación.
- Terreno.
- Cielo.
- Elementos naturales.
- Decoración ambiental.
- Texturas.

## military/kenney-desert-shooter-pack/

Inspeccionar el paquete completo.

Clasificar sus recursos por:
- Objetos.
- Decoración.
- Elementos militares.
- Estructuras.
- Terreno.
- Vegetación.
- Otros elementos encontrados.

## props/kenney-city-kit-roads/

Utilizar los recursos de esta carpeta para construir escenarios urbanos.

Buscar:
- Carreteras.
- Intersecciones.
- Aceras.
- Señalización.
- Elementos de calles.
- Decoración urbana.
- Piezas modulares.

No crear objetos duplicados si ya existen recursos equivalentes.

# 5. INSPECCIÓN Y ORGANIZACIÓN DE TODOS LOS ARCHIVOS

Antes de integrar el repositorio, realizar un inventario completo.

Examinar extensiones:

- GLB.
- GLTF.
- BIN.
- PNG.
- JPG.
- WEBP.
- HDR.
- EXR.
- FBX.
- OBJ.
- MTL.
- WAV.
- MP3.
- OGG.
- JSON.

Crear `ASSET_INVENTORY.md`.

Para cada archivo registrar:

| Propiedad | Descripción |
|---|---|
| Nombre | Nombre original |
| Ruta | Ubicación |
| Formato | GLB, PNG, HDR, etc. |
| Peso | MB |
| Materiales | Materiales encontrados |
| Texturas | Dependencias |
| Animaciones | Clips disponibles |
| Función | Uso recomendado |
| Licencia | Licencia verificada |

No modificar los nombres originales de los recursos.

Mantener un registro centralizado para que el código pueda localizar cada asset.

# 6. INTEGRACIÓN CON THREE.JS

Utilizar `GLTFLoader` para importar los modelos GLB.

Ejemplo:

```js
import { GLTFLoader } from "three/addons/loaders/GLTFLoader.js";

const loader = new GLTFLoader();

loader.load(
  "/assets/characters/iron_man.glb",
  (gltf) => {
    const character = gltf.scene;

    scene.add(character);

    const animations = gltf.animations;

    console.log("Animations:", animations);
  }
);
```

Adaptar las rutas y las importaciones a la versión de Three.js instalada.

## Materiales

Conservar los materiales originales siempre que sea posible.

Comprobar:

- Base color.
- Metallic.
- Roughness.
- Normal maps.
- Emissive.
- Ambient occlusion.
- Texturas faltantes.

Utilizar materiales PBR y una iluminación coherente.

Evitar convertir todos los materiales en metálicos o excesivamente brillantes.

## Escala y colisiones

Separar:

- Modelo visual.
- Collider.
- Esqueleto.
- Animaciones.

Utilizar colisiones simplificadas para mejorar el rendimiento.

Comprobar que los personajes tengan una escala consistente con el escenario.

# 7. SISTEMA CENTRALIZADO DE VFX

Los efectos especiales deben estar separados de la lógica de combate.

Crear un sistema llamado `VFXManager`.

Organizar los efectos por categorías:

```text
vfx/
│
├── impacts/
│   ├── light/
│   ├── heavy/
│   └── ground/
│
├── energy/
│   ├── charge/
│   ├── beam/
│   ├── aura/
│   └── explosion/
│
├── projectiles/
│
├── shockwaves/
│
├── elemental/
│   ├── fire/
│   ├── ice/
│   ├── lightning/
│   └── wind/
│
├── debris/
│
├── smoke/
│
└── cinematic/
```

Estas carpetas son una organización propuesta. Solo crear las categorías que tengan recursos reales.

## Cómo debe funcionar

Cada efecto debe ser independiente y reutilizable.

Ejemplo conceptual:

```js
VFXManager.play("energy.explosion", {
  position: impactPosition,
  scale: 1.5,
  duration: 2,
  quality: "high"
});
```

Cada efecto debe controlar:

- Posición.
- Rotación.
- Escala.
- Duración.
- Velocidad.
- Color.
- Intensidad.
- Animación.
- Limpieza automática.

No crear un único efecto gigante que contenga todos los poderes.

Cada habilidad debe poder seleccionar sus propios efectos.

## Efectos que deben existir

### Impactos
- Golpes ligeros.
- Golpes pesados.
- Impactos contra paredes.
- Impactos contra el suelo.
- Chispas.
- Polvo.

### Energía
- Cargas de energía.
- Auras.
- Rayos.
- Explosiones.
- Ondas expansivas.
- Proyectiles.

### Elementales
- Fuego.
- Hielo.
- Electricidad.
- Viento.
- Humo.

### Destrucción
- Escombros.
- Fragmentos.
- Grietas.
- Polvo.
- Ondas de choque.

No utilizar efectos que no correspondan a la habilidad del personaje.

# 8. ANIMACIONES DE COMBATE

El sistema de animaciones debe ser independiente de los efectos visuales.

Utilizar `AnimationMixer` para los modelos que tengan clips compatibles.

Crear un controlador que gestione:

- Idle.
- Walking.
- Running.
- Jumping.
- Falling.
- Landing.
- Attacking.
- Blocking.
- Taking damage.
- Knockback.
- Finisher.
- Death.

No asumir que todos los personajes utilizan exactamente las mismas animaciones.

Cada personaje puede tener un conjunto diferente de movimientos.

Utilizar cross-fades para transiciones suaves.

Evitar que varias animaciones incompatibles se reproduzcan simultáneamente.

# 9. SISTEMA DE CUTSCENES CINEMATOGRÁFICAS

**Esta es una de las partes más importantes del proyecto.**

Quiero cutscenes con una calidad cinematográfica similar a las presentaciones de combate de Marvel's Spider-Man y The Strongest Battlegrounds.

No quiero simples cámaras siguiendo al jugador.

Quiero escenas dirigidas, coreografiadas y animadas.

## 9.1 CutsceneDirector

Crear un controlador central:

```text
cinematic/
│
├── CutsceneDirector.js
├── CutsceneTimeline.js
├── CinematicCamera.js
├── CharacterChoreography.js
├── CutsceneAudio.js
├── CutsceneEffects.js
│
└── sequences/
    ├── ultimate/
    ├── finishers/
    ├── introductions/
    └── special_attacks/
```

Adaptar los archivos a la arquitectura real.

El director debe poder:

- Iniciar una secuencia.
- Pausar.
- Cancelar.
- Saltar.
- Terminar.
- Restaurar los controles.
- Restaurar la cámara.
- Restaurar el HUD.

Debe evitar que el gameplay y la cutscene controlen simultáneamente la misma cámara.

## 9.2 Cámara cinematográfica

Implementar diferentes tipos de planos:

**Plano general**
- Presenta la arena.
- Muestra la posición de ambos personajes.
- Establece el espacio de combate.

**Plano medio**
- Muestra el cuerpo y los movimientos.
- Sigue ataques y desplazamientos.

**Primer plano**
- Rostro.
- Puños.
- Manos cargando energía.
- Expresiones.

**Cámara dinámica**
- Travelling lateral.
- Cámara orbital.
- Cámara baja.
- Seguimiento del personaje.
- Push-in.
- Pull-out.
- Whip pan.
- Cambios rápidos de plano.

Utilizar interpolaciones suaves y trayectorias mediante curvas.

Evitar movimientos aleatorios y bruscos.

## 9.3 Efectos cinematográficos

Incorporar:

- Slow motion.
- Hit-stop.
- Camera shake.
- Motion blur opcional.
- Bloom.
- Destellos.
- Partículas.
- Escombros.
- Ondas expansivas.
- Cambios de iluminación.
- Efectos de sonido sincronizados.
- Barras cinematográficas opcionales.

Los efectos deben tener intensidad controlada.

No llenar toda la pantalla de partículas.

## 9.4 Coreografía de combate

Las cutscenes deben incluir movimientos reales de los personajes.

Ejemplos:

- El personaje carga un ataque.
- La cámara se acerca.
- El rival reacciona.
- El héroe se desplaza rápidamente.
- Se produce un golpe.
- La cámara cambia de ángulo.
- El rival sale despedido.
- El escenario recibe el impacto.
- El héroe termina con una pose.
- La cámara vuelve al gameplay.

Los movimientos deben estar sincronizados con las animaciones disponibles.

Si no existe una animación necesaria, crearla o conseguir una compatible.

No sustituir la animación de un personaje por una simple rotación de su modelo.

# 10. EJEMPLO DE CUTSCENE: ULTIMATE

Duración orientativa: 8-10 segundos.

| Tiempo | Acción |
|---|---|
| 0.0 s | El héroe comienza a cargar energía |
| 0.8 s | Primer plano del rostro y las manos |
| 1.6 s | El rival se prepara para defenderse |
| 2.2 s | El héroe se lanza |
| 3.0 s | Primer impacto |
| 3.1 s | Hit-stop y cámara lenta |
| 3.5 s | Explosión de energía |
| 4.5 s | El rival sale despedido |
| 5.5 s | Cámara sigue al rival |
| 6.5 s | Impacto contra el escenario |
| 7.5 s | Plano bajo del héroe |
| 8.5 s | Regreso gradual al gameplay |

Esta secuencia debe ser un ejemplo de estructura, no una coreografía obligatoria para todos los personajes.

Cada personaje debe tener su propia identidad.

# 11. SINCRONIZACIÓN ENTRE CUTSCENES Y GAMEPLAY

La cutscene no debe controlar el sistema de daño.

El sistema de combate sigue siendo responsable de:

- Hitboxes.
- Daño.
- Cooldowns.
- Estados de los personajes.
- Resultados de ataques.
- Reglas multijugador.

La cutscene únicamente presenta visualmente esos resultados.

Flujo recomendado:

1. El jugador activa la ultimate.
2. El sistema de combate verifica que puede utilizarse.
3. Se inicia la secuencia.
4. Se ejecutan las animaciones.
5. Se sincronizan los efectos.
6. El sistema de combate aplica el resultado correspondiente.
7. Se reproduce la reacción del rival.
8. Termina la secuencia.
9. Se restaura el control del jugador.

Si hay multijugador, la autoridad del combate debe seguir siendo el servidor o sistema autoritativo existente.

Evitar que cada cliente aplique daño por su cuenta durante la cutscene.

# 12. CALIDAD VISUAL AAA

La dirección artística debe mantener una apariencia profesional.

Prioridades:

- Iluminación cinematográfica.
- Materiales PBR.
- Reflejos.
- Sombras de contacto.
- Bloom controlado.
- Partículas de calidad.
- Animaciones fluidas.
- Escenarios detallados.
- Efectos de destrucción.
- Buen contraste visual.
- Cámara cinematográfica.

Evitar:
- Exceso de colores neón.
- Modelos excesivamente brillantes.
- Partículas que oculten los personajes.
- Interfaces genéricas.
- Animaciones robóticas.
- Efectos de baja calidad.
- Escenarios vacíos.

# 13. OPTIMIZACIÓN

El proyecto debe seguir siendo un juego web.

Priorizar WebGL como renderizador compatible.

WebGPU puede utilizarse como mejora opcional.

Aplicar:

- Instancing.
- Object pooling.
- Carga bajo demanda.
- Reutilización de materiales.
- Compresión de texturas.
- Optimización de geometría.
- LOD cuando corresponda.
- Control de partículas simultáneas.
- Sombras selectivas.
- Postprocesado escalable.

Cada modelo individual debe respetar el límite de 25 MB.

No eliminar recursos para mejorar el rendimiento sin comprobar primero otras opciones.

No reducir arbitrariamente la calidad gráfica.

Crear ajustes gráficos:

- Low.
- Medium.
- High.
- Ultra.

Los efectos deben adaptarse automáticamente al nivel elegido.

# 14. LICENCIAS Y DERECHOS

Antes de publicar o distribuir recursos:

- Verificar la licencia del repositorio original.
- Verificar las licencias individuales.
- Mantener atribuciones cuando sean necesarias.
- No asumir que los modelos de personajes famosos son de uso comercial libre.
- Distinguir recursos originales de recursos externos.

El hecho de que un modelo esté disponible públicamente en GitHub no significa que se pueda redistribuir sin restricciones.

# 15. FLUJO DE TRABAJO PARA LA IA

Cuando una IA reciba este documento, debe seguir estas fases.

## FASE A — AUDITORÍA

1. Inspeccionar el proyecto principal.
2. Inspeccionar todas las carpetas del repositorio.
3. Crear el inventario de assets.
4. Comprobar el tamaño de cada archivo.
5. Previsualizar los modelos.
6. Identificar materiales y texturas.
7. Comprobar las animaciones disponibles.
8. Identificar las licencias.

No modificar nada todavía.

## FASE B — ORGANIZACIÓN

1. Crear una estructura de recursos clara.
2. Separar personajes, edificios, objetos y efectos.
3. Crear el manifiesto de recursos.
4. Establecer rutas consistentes.
5. Evitar duplicados.

## FASE C — INTEGRACIÓN

1. Integrar primero un personaje de prueba.
2. Comprobar materiales y escala.
3. Comprobar animaciones.
4. Integrar los edificios y objetos.
5. Integrar los efectos especiales.
6. Crear el VFXManager.
7. Crear el CutsceneDirector.
8. Implementar una cutscene de prueba.
9. Integrar progresivamente el resto.

## FASE D — VALIDACIÓN

Comprobar:

- Que el juego inicia.
- Que todos los recursos cargan.
- Que no hay texturas faltantes.
- Que los personajes se animan correctamente.
- Que los efectos se reproducen.
- Que las cutscenes terminan correctamente.
- Que la cámara se restaura.
- Que los controles funcionan después de cada secuencia.
- Que no hay errores de memoria.
- Que el combate sigue funcionando.
- Que el rendimiento es aceptable.

# 16. REGLAS INNEGOCIABLES

1. No reconstruir el juego desde cero.
2. No cambiar las mecánicas existentes.
3. No eliminar modelos ni texturas.
4. No sustituir personajes sin autorización.
5. No modificar el sistema de combate para implementar efectos visuales.
6. No mezclar todos los VFX en un solo archivo.
7. No crear cutscenes basadas únicamente en movimientos de cámara.
8. No asumir animaciones que no existen.
9. No introducir dependencias incompatibles.
10. No sacrificar el rendimiento innecesariamente.
11. Mantener la compatibilidad con Three.js.
12. Verificar todos los cambios antes de finalizar.

---

# OBJETIVO FINAL

Hero Battlegrounds debe evolucionar hacia un battleground 3D web con presentación AAA.

Los personajes deben tener modelos detallados, animaciones fluidas y habilidades visualmente espectaculares.

Los escenarios deben sentirse como auténticas arenas de combate superheroicas.

Los poderes deben tener efectos individuales, detallados y sincronizados con los ataques.

Las ultimates y finishers deben tener cutscenes cinematográficas con coreografías, cámaras dinámicas, animaciones, sonido, partículas y destrucción ambiental.

El resultado debe sentirse como un videojuego comercial de superhéroes, manteniendo la arquitectura, las mecánicas y el rendimiento del juego web original.

**Prioridad absoluta: calidad visual, animaciones, efectos de combate y presentación cinematográfica sin romper el gameplay existente.**
