# Puerta a Puerta — Tablero de campaña

PWA para gestionar la operación territorial de una candidatura a alcaldía. Pensada para el Bajo Cauca: celulares de gama baja, señal intermitente, trabajo en calle.

**Desarrollada por Vibras Positivas HM — Derechos de Autor Reservados**

## Qué resuelve

El problema que hunde a los candidatos independientes no es la falta de propuestas: es no saber cuántos votos tienen de verdad hasta que ya es tarde. Esta app responde una sola pregunta, todos los días: *¿cuántos votos comprometidos hay, en qué puesto de votación están, y quién los está trayendo?*

## Módulos

| Módulo | Qué hace |
|---|---|
| **Tablero** | Malla de 100 casillas = avance hacia la meta (oro = confirmados, verde = probables). Líderes sin reportar en 14 días, puestos cubiertos, firmas, próximos recorridos. |
| **Puestos** | Puestos de votación con mesas, potencial de la Registraduría y meta propia. Compara meta contra potencial real. |
| **Líderes** | Equipo por barrio/vereda, puesto asignado, compromiso de votos y cumplimiento. Marca en rojo a quien lleva 14 días sin reportar. |
| **Compromisos** | Votante por votante: barrio, puesto donde vota, líder que lo trae, estado (por contactar / probable / confirmado). Búsqueda y filtros. |
| **Firmas** | Calcula sola la meta legal y registra entregas por recolector. |
| **Escucha** | Ranking de temas a partir de lo que pidió cada persona, filtrable por barrio, con las anotaciones textuales debajo. Es el insumo del programa de gobierno. |

## Cálculo de la meta de firmas

Para inscribir por Grupo Significativo de Ciudadanos se exige un número de firmas válidas equivalente al menos al **20% del resultado de dividir el número de ciudadanos aptos para votar entre el número de cargos por proveer**, y en ningún caso más de **50.000 firmas** (Ley 130 de 1994, art. 9; Resolución 2106 de 2021 RNEC). La app aplica esa fórmula con el censo que se cargue en Ajustes.

La app también muestra una **meta de trabajo 40% por encima** de la exigida, porque la verificación de la Registraduría anula apoyos por cédula ilegible, repetida o de otro municipio.

> Confirme el censo electoral vigente de Caucasia con la Registraduría antes de fijar la meta. El calendario electoral lo fija el CNE para cada elección.

## Datos y Habeas Data

- Todo se guarda **en el propio celular** (localStorage). No hay servidor, no hay nube, no hay cuenta.
- **Modo consulta** (por defecto): los teléfonos se muestran enmascarados (`•••• ••• 431`).
- **Modo admin**: pide la clave definida en Ajustes y destapa teléfonos, habilita el botón de WhatsApp y exporta el CSV con los números completos.
- Los formularios que recogen datos personales llevan el aviso de la **Ley 1581 de 2012**. Registre a alguien solo si autorizó que lo contacten.
- El respaldo `.json` contiene datos personales sin enmascarar: trátelo como documento reservado.

## Respaldo

Exportar respaldo `.json` una vez por semana y guardarlo en dos lugares. Si se pierde el celular o se borran los datos del navegador, **no hay forma de recuperar la información** sin ese archivo. También exporta los compromisos a `.csv` para abrir en Excel.

## Instalación / despliegue

1. Suba los archivos a la raíz del sitio:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icon-192.png`, `icon-512.png`, `icon-512-maskable.png`
2. **Falta generar los íconos** (fondo `#16233A`, marca en `#C8951B`) y la imagen OG de 1200×630 px en `https://vibraspositivashm.com/og/puerta-a-puerta-og.png`. Sin la imagen OG el enlace se ve vacío al compartirlo por WhatsApp.
3. Ajuste `og:url` en `index.html` a la URL real del despliegue.
4. Requiere HTTPS para que funcionen el service worker y la instalación. Netlify, GitHub Pages y el cPanel de Distrileco sirven.
5. Al abrirla en Android aparece la barra dorada "Instalar". En iPhone: Compartir → Agregar a pantalla de inicio.

## Primeros pasos con el candidato

1. Ajustes: nombre, movimiento, censo electoral, meta de votos, fecha de elección y clave de admin.
2. Cargar los puestos de votación con el potencial real de la Registraduría.
3. Cargar líderes y asignarles puesto y compromiso de votos.
4. De ahí en adelante: cada compromiso se registra **el mismo día que se consigue**, siempre con su tema.

## Stack

HTML/CSS/JS vanilla, sin dependencias ni build. Tipografía Barlow y Barlow Condensed (Google Fonts, con respaldo del sistema). Service worker con caché *cache-first*.
