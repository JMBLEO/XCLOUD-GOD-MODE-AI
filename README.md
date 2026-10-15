<div align="center">

# 🎮 XCLOUD GOD MODE AI
### *El Mega-Script Definitivo para Xbox Cloud Gaming (xCloud) & Xbox Remote Play (XRemote)*

[![Version](https://img.shields.io/badge/Versi%C3%B3n-39.0.0--Ultimate-107C10?style=for-the-badge&logo=xbox&logoColor=white)](https://github.com/JMBLEO/XCLOUD-GOD-MODE-AI)
[![License](https://img.shields.io/badge/Licencia-MIT-blue?style=for-the-badge)](https://github.com/JMBLEO/XCLOUD-GOD-MODE-AI/blob/main/LICENSE)
[![Platform](https://img.shields.io/badge/Plataforma-Web%20%7C%20PC%20%7C%20M%C3%B3vil%20%7C%20SmartTV-0078D4?style=for-the-badge&logo=windows11&logoColor=white)](https://www.xbox.com/play)
[![Tampermonkey](https://img.shields.io/badge/Soporte-Tampermonkey%20%7C%20Violentmonkey-00485B?style=for-the-badge)](https://www.tampermonkey.net/)

<p align="center">
  <b>Desbloqueo real de 1440p / 4K / 8K • Shaders GPU IA en Tiempo Real (0ms Latencia) • Emulación Háptica DualSense 5</b>
</p>

---

[🚀 Características](#-características-principales-v390) •
[🙏 Créditos y Proyectos Base](#-agradecimientos-y-proyectos-base-créditos-especiales) •
[📦 Instalación](#-instalación-rápida) •
[🧠 Arquitectura IA y Vídeo](#-arquitectura-de-shaders-ia-y-desbloqueo-1440p4k8k) •
[🛡️ Seguridad Anti-Ban](#️-seguridad-y-modo-anti-ban)

</div>

---

## 🌟 ¿Qué es XCLOUD GOD MODE AI?

**XCLOUD GOD MODE AI** es un motor unificado (*Userscript*) de alto rendimiento para navegadores web que fusiona las mejores técnicas de ingeniería inversa de la escena de **Xbox Cloud Gaming** y **Xbox Remote Play (XRemote)** con pipelines matemáticos de reconstrucción de imagen por GPU y personalización avanzada de mandos.

Diseñado bajo una arquitectura **"Zero Black-Screen"** (Cero Pantallas Negras), interviene directamente sobre el flujo nativo de WebRTC y el compositor del navegador sin introducir *input lag*.

---

## 🙏 Agradecimientos y Proyectos Base (Créditos Especiales)

> [!IMPORTANT]
> **Este proyecto NO habría sido posible sin el increíble trabajo de investigación, código abierto e ingeniería inversa de los desarrolladores y repositorios que sentaron las bases de la comunidad de Xbox Streaming.**  
> **XCLOUD GOD MODE AI** nace como un tributo e integración maestra de las ideas, parches y algoritmos desarrollados por estos gigantes:

| Proyecto / Repositorio | Autor / Comunidad | Contribución e Inspiración en este Mega-Script |
| :--- | :--- | :--- |
| 🏆 **[Better xCloud](https://github.com/redphx/better-xcloud)** | **@redphx** | La piedra angular absoluta. Base del sistema de intercepción WebRTC/SDP, estadísticas en vivo, parches de controles, soporte Co-Op local, audio booster y mejoras de calidad de vida (QoL). |
| 📡 **[XStreaming](https://github.com/Geocld/XStreaming)** | **@Geocld** | Referencia fundamental para los protocolos de negociación de transmisión en **xCloud** y **XHome (Remote Play)**, optimización de baja latencia y manejo de sesiones remotas. |
| 🎮 **XBPlay** | **Studio08** | Inspiración clave para el desbloqueo de parámetros de alta definición (1080p HQ / 1440p), perfilado de servidores *Series X (Anaconda)* y filtros de nitidez en streaming. |
| ⚡ **XFly Engine** | **Comunidad XFly** | Motor de optimización de *Playout Delay Hint* (`playoutDelayHint = 0`) en los receptores RTP de WebRTC para lograr respuesta instantánea de cuadro. |
| 🟢 **[Greenlight](https://github.com/unknownskl/greenlight)** | **@unknownskl** | Documentación y estructura de los canales de entrada (`inputChannel`), configuración de cliente XHome/xCloud y manejo de *tokens* de streaming. |
| 🧠 **[Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN)** | **@xinntao** | Inspiración matemática de sus arquitecturas `srvgg_arch.py` (*SRVGGNetCompact*) y `anime_video_model` para diseñar nuestros **Shaders SVG Multi-Etapa** de limpieza y reconstrucción de bordes en tiempo real. |
| 🎬 **[ComfyUI-SeedVR2 VideoUpscaler](https://github.com/numz/ComfyUI-SeedVR2_VideoUpscaler)** | **@numz / @adrientoupet** | Referencia de su módulo `color_fix.py` y realce de detalle para programar el **Estabilizador de Luminancia y Croma (SeedVR2 Color Fix)** sobre flujos de video comprimidos. |

*Si utilizas y disfrutas este script, te invitamos a visitar los repositorios originales mencionados arriba y dejarles una estrella ⭐ por su invaluable aporte a la comunidad.*

---

## 🚀 Características Principales (v1.1)

### 1. 🖥️ Desbloqueo Nativo 1440p (QHD), 4K (UHD) y 8K (Full UHD)
* **Inyección Directa en la Interfaz de Xbox (`StreamResolutionSelector`):** Modifica el selector oficial de resolución de Xbox Cloud Gaming agregando botones funcionales para **1440p (12 GB/h)**, **4K (20 GB/h)** y **8K (35 GB/h)**.
* **Doble Compatibilidad (Cloud Gaming + XRemote):** Intercepta tanto `/sessions/cloud/` como `/sessions/home/` para que tus juegos en la nube y el juego remoto desde tu consola funcionen a la máxima resolución.
* **Certificación `MediaCapabilities` & Detección >FHD:** Engaña a la API `navigator.mediaCapabilities.decodingInfo` devolviendo `{ supported: true, smooth: true, powerEfficient: true }` y detecta monitores superiores a 1080p para habilitar el supersampling sin restricciones.

### 2. 🧠 Shaders IA en Tiempo Real (0ms Latencia & Cero Pantalla Negra)
A diferencia de las redes neuronales pesadas en Python/CUDA que requieren segundos por fotograma, hemos traducido la lógica visual de **Real-ESRGAN** y **SeedVR2** a **Pipelines SVG acelerados por GPU** que operan directo sobre el `<video>` nativo:
* 🌟 **Real-ESRGAN (SRVGG Compact):** Doble paso de micro-denoise gaussiano + matriz de convolución simétrica que limpia artefactos de compresión y reconstruye texturas realistas.
* 🎌 **Real-ESRGAN (AnimeVideo / Cel-Shading):** Aplana el ruido de bloque en colores sólidos y remarca los trazos oscuros (ideal para *Persona*, *Genshin Impact*, *Hi-Fi Rush*, *Dragon Ball*).
* 🎬 **SeedVR2 Detail Enhancer + Color Fix:** Matriz de transferencia de componentes y corrección de croma que recupera los colores lavados por la compresión H.264/HEVC/AV1 sin quemar los blancos.
* ⚡ **AMD FidelityFX CAS & Unsharp Mask (USM):** Los clásicos filtros de contraste adaptativo listos para usar.

### 3. 📊 Ghost HUD / OSD de Prioridad Absoluta (Capa Suprema)
* **Primera Función en Ejecutarse:** El monitor de estadísticas se inicializa en el milisegundo cero al negociar la conexión WebRTC (`addIceCandidate` y `play`), antes que cualquier filtro o escalador.
* **Inmune al Reescalado y Pantalla Completa:** Se inyecta dinámicamente como el nodo superior del contenedor de stream/fullscreen con `z-index: 2147483647 !important`, `isolation: isolate` y aceleración 3D (`translate3d`), garantizando que **jamás quede oculto ni deformado** al forzar 1440p, 4K u 8K.
* **14 Métricas con Iconos Dinámicos:** Reloj, Tiempo Jugado, Batería, Ping, Jitter, Resolución en vivo, FPS, Bitrate, Tiempo de Decodificación (ms), Paquetes Perdidos, Cuadros Caídos, Descarga/Subida acumulada y Detección Automática de Red (Wi-Fi / Ethernet / Datos).

### 4. 🧹 Auto-Detox Post-Juego (Limpieza Inteligente de Caché)
* **Activación Automática al Cerrar un Juego:** Detecta al instante cuando sales de una partida o se cierra la sesión WebRTC.
* **Purga Selectiva Sin Tocar tu Cuenta:** Elimina de la `Cache Storage API` y de la memoria RAM todas las imágenes pesadas del catálogo (`.png`, `.jpg`, `.webp`), videos promocionales (`.mp4`, `.webm`), fuentes tipográficas (`.woff2`), buffers de video residuales y registros de telemetría/QoS.
* **100% Seguro para tus Datos:** Mantiene intactas tus cookies, tu inicio de sesión de Microsoft/Xbox Live, los ajustes nativos de xCloud y toda tu configuración de **God Mode**.

### 5. 📳 Emulación Háptica DualSense 5 y Controles Pro
* **Fix Definitivo de Vibración Infinita:** Parcheado directamente sobre el prototipo raíz `GamepadHapticActuator.prototype.playEffect`, eliminando fugas de memoria y cortes de vibración tras los primeros segundos.
* **Perfiles Hápticos:**
  * *Xbox Estándar:* Vibración original.
  * *DualSense 5 (Háptica HD):* Potencia las micro-frecuencias (`weakMagnitude x1.45`) y equilibra los motores pesados para simular la respuesta táctil texturizada del mando de PS5.
  * *Pro / Competitivo:* Pulsos cortos y secos (máx. 140ms) para no perder precisión apuntando.
* **Polling Rate hasta 250 Hz (4 ms):** Reduce el retraso de lectura del mando con ajuste de Zonas Muertas (Anti-Drift) e inversión de botones estilo Nintendo Switch.
* **Pop-ups de Detección de Hardware:** Notificaciones flotantes al conectar Mandos de Xbox, PlayStation, Nintendo, Volantes de Carrera, Mandos de Avión (HOTAS), Teclado o Ratón.

### 6. 🪟 Interfaz Glassmorphism (Modo Ventana Libre)
* **Efecto Acrílico / Mica:** Panel principal, notificaciones Toast, botón flotante y barra OSD diseñados con transparencia real (`backdrop-filter: blur(24px) saturate(180%)`) y bordes con relieve luminoso que dejan traslucir el juego de fondo.
* **Ventana Arrastrable y Redimensionable:** Arrastra el panel desde su barra superior a cualquier rincón de tu monitor o cambia su tamaño libremente desde la esquina inferior derecha con diseño auto-responsivo (`@container`).

---

## 🛡️ Seguridad y Modo Anti-Ban

Hemos separado estrictamente el **Teclado** y el **Ratón** e incorporado el interruptor crítico **🛡️ Solo M&K Nativo (Evitar Baneos)**:
* Cuando está **Activado**, el script bloquea cualquier intento de emulación de mando mediante teclado/ratón en juegos exclusivos de consola, enviando entradas de M&K únicamente en títulos que cuentan con soporte nativo oficial de PC/Consola en xCloud (evitando sanciones en títulos competitivos).
* Asimismo, los **Controles Táctiles** están divididos entre **Táctil Nativo** (solo juegos compatibles) y **Joystick Virtual Superpuesto** (cualquier juego).

---

## 🌍 Enrutamiento Global y Códecs de Nueva Generación

* **Buscador Estricto en Tiempo Real:** Filtra al instante entre más de **65 pasarelas IP (`X-Forwarded-For`)** de nodos MS Azure, Google Cloud, AWS, Cloudflare e ISPs locales (Chile, Argentina, Brasil, EE.UU., México, Europa, Japón, Corea, Australia) y **20 Data Centers físicos de Azure**.
* **Selector de Códecs Avanzado:** Auto-detección del máximo códec soportado por tu GPU o forzado manual de **VVC (H.266)**, **AV2**, **AV1**, **H.265 (HEVC)**, **VP9** y perfiles **H.264**.
* **Rango Dinámico Universal (HDR):** Selector para **SDR**, **HDR10**, **Dolby Vision** y **HLG** con detector automático del soporte físico de tu monitor y alerta preventiva de alteración de color.

---

## 📦 Instalación Rápida

1. Instala una extensión gestora de scripts en tu navegador (recomendamos **[Tampermonkey](https://www.tampermonkey.net/)** o **[Violentmonkey](https://violentmonkey.github.io/)** en Chrome, Edge, Brave o Firefox).
2. Haz clic en el icono de la extensión y selecciona **"Crear un nuevo script..."** (*Create a new script*).
3. Borra todo el contenido por defecto, copia el código íntegro del script desde este repositorio ([`xcloud-god-mode-ai.user.js`](https://github.com/JMBLEO/XCLOUD-GOD-MODE-AI)) y pégalo.
4. Presiona **`Ctrl + S`** (o *Archivo > Guardar*).
5. Entra a **[xbox.com/play](https://www.xbox.com/play)**. Verás el nuevo botón **⚙️ MJS 🌐 1440p** en la barra superior derecha y el engranaje flotante magnético **⚙️** en el borde izquierdo de tu pantalla.

---

## ⚖️ Aviso Legal (Disclaimer)

Este script es una herramienta de código abierto creada por y para la comunidad con fines educativos y de mejora de accesibilidad/rendimiento en el navegador. No está afiliado, respaldado ni patrocinado por **Microsoft Corporation** ni **Xbox**. El uso de funciones experimentales como el bypass regional de IP o la emulación de controles en juegos no soportados queda bajo la responsabilidad de cada usuario.

<div align="center">
  <sub>Desarrollado con ❤️ por <b><a href="https://github.com/JMBLEO">JMBLEO</a></b> • Impulsado por el legado Open Source de la comunidad xCloud.</sub>
</div>
