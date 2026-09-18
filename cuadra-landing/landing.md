# 🏠 Cuadra — Landing

**Creado:** 2026-09-19  
**Estado:** Hero completado, secciones Purpose/Cta/Footer completadas, pendiente pulido estético.  
**URL:** https://cuadra-one.vercel.app/  
**Repo código:** cuadra-one (privado)

## Visión

Plataforma independiente de pedidos para negocios de barrio: hamburgueserías, pizzerías, sushi, cafeterías, bebidas, heladerías. Primer caso de uso de Icaria.

### Por qué el nicho es poderoso

1. **Cada comercio tiene valor desde el día 1, solo, sin red.** No necesitamos masa crítica de locales y usuarios; un kiosco que pone su QR en el flyer ya obtuvo valor. Eliminamos el problema del huevo y la gallina.

2. **La matemática de la comisión:** Ticket promedio $8.000, apps corporativas cobran ~30% = $2.400 por pedido. Con 17 pedidos por mes que hoy le pasan por Rappi/PedidosYa, Cuadra ($40.000/mes) se paga sola. Todo lo que venga después es plata que queda en el bolsillo del comerciante.

3. **No pedimos generar demanda nueva: convertimos la demanda que YA tiene.** El local de barrio ya tiene clientes (estados de WhatsApp, MDs, IG/FB, flyers). Cuadra le da el canal propio donde ese tráfico se transforma en pedido sin fricción.

4. **El flyer de papel es nuestro caballo de Troya.** Nadie digitalizó el flyer porque nadie lo miró como activo. El QR convierte el papel (que el barrio ya reparte y conserva pegado en la heladera) en un canal medible.

5. **"En mi barrio no hay ninguna" es nuestro foso defensivo.** Nuestra distribución es caminar la cuadra, hablar con el dueño. Eso no escala para corporaciones, pero para nosotros es barato y letal. El que llega primero se queda con los QR impresos.

6. **Estructura de costos:** Sheets como backend = costo casi cero, y el comerciante entiende la herramienta. $40.000/mes es margen casi puro.

## Stack

- **Frontend:** React + Vite + TypeScript (strict) + Tailwind v4 + motion
- **UI:** Componente draggable-card de Aceternity UI
- **Deploy:** Vercel (deploy automático por push)
- **Backend fase 1:** Google Sheets pública (<150 artículos por comercio, bajo costo, herramienta familiar)
- **Backend fase 2 (visión):** Turso (ver [docs/icaria/backend.md](../icaria/backend.md))

## Estructura de la landing

Exactamente 4 secciones, sin excepciones:

1. **Hero:** Mantel a cuadros servido de fondo, 7 tarjetas de rubros arrastrables encima (ahora serán 8 con la tarjeta 8 de invitación), copy centrado arriba, chip de affordance, zoom al click.
2. **Purpose:** Objetivo de Cuadra en 3 pilares + frase de cierre.
3. **Cta:** Llamado a la acción con flag SHOW_PRICING para mostrar/ocultar precios.
4. **Footer:** Mínimo, tagline + cierre + links placeholder.

## Decisiones congeladas

### Hero
- **Mesa:** Foto real de mantel a cuadros servido (hero.webp), vista cenital o casi cenital, con plato vacío, celular, servilleta.
- **Tarjetas:** 7 rubros + 1 tarjeta de invitación (pendiente). Asset completo 576×883 en proporción nativa, sin recortes ni textos agregados.
- **Disposición:** Anillo de 8 slots barajados por carga con jitter y rotación, centro despejado para el copy.
- **Interacciones:** Drag libre con rebote en la caja de mesa, zoom al click (lightbox centrado), chip de affordance con fade 3s.
- **Mobile:** Grid estático de 2 columnas barajado, sin drag.

### Purpose
- Gradiente cálido (amber-50 → orange-50), 3 pilares en cards con hover, emojis como íconos.
- Pilares: "Tu vidriera, con tu marca", "Cero comisiones", "Del flyer al pedido".

### Cta
- Gradiente fuerte (orange-600 → red-600), botón blanco redondeado.
- Flag SHOW_PRICING: si true, muestra bloque de precio; si false, oculto.

### Copy
- Badge: "Canal de pedidos propio para negocios de barrio"
- H1: "Tu menú, tu link, tu QR. Tus pedidos, tuyos."
- Sub: "Publicá tus productos, compartí el link por WhatsApp y poné el QR en tu flyer. Sin comisiones por venta: el pedido entra directo a tu mostrador."

## Decisiones abiertas

### SHOW_PRICING (estado: inclinada a true con lista de incluidos)
**Contexto:** Mifud muestra precios ($8.999/mes el plan comparable). Cuadra son $40.000/mes + $350.000 ingreso = 4,4× mensual. Esconder precios nos hace parecer caros por silencio; mostrarlos con lista de "qué incluye" (diseño de menú, carga completa, QR impreso, actualización por WhatsApp, cero comisión) convierte el precio en servicio continuo, no alquiler.  
**Pendiente:** Decidir texto final del bloque de incluidos.

### Tamaño final de tarjetas (pendiente Lighthouse)
**Estado:** Proporción 576:883 congelada; tamaño en píxeles abierto a medición.  
**Método:** Correr Lighthouse en la URL de Vercel, medir performance/LCP/CLS, ajustar el clamp de ancho para optimizar.

### Navbar/hamburguesa (pendiente)
**Estado:** No implementado.  
**Contexto:** La landing es corta (4 secciones), quizás no necesite navegación. Depende de cómo fluya el scroll y si el Cta necesita ancla visible.

### Tarjeta 8 (pendiente Prompt 2b)
**Estado:** Diseñada en charla, no implementada.  
**Concepto:** Sin foto, con identidad propia (borde punteado o retazo de mantel), texto "ESTE ESPACIO ES PARA TU NEGOCIO" o "ACÁ FALTA EL TUYO". Click lleva al Cta con scroll suave. Participa del shuffle como las otras.

## Competencia: Mifud

**URL:** https://www.mifud.net/  
**Análisis:** 2026-09-19

### Modelo
SaaS self-service: le sacás foto a la carta de papel, IA carga platos y precios, 14 días gratis sin tarjeta, planes desde $5.999/mes (el comparable a Cuadra es $8.999/mes).

### Fortalezas de Mifud
- Onboarding fricción cero (foto + IA, sin visita).
- Barrera de entrada mínima (prueba gratis, precio bajo).
- FAQ que mata objeciones en la landing.

### Debilidades de Mifud (fortalezas de Cuadra)
- Self-service: alguien tiene que aprender el panel. Cuadra vende "yo me siento con vos y te lo dejo funcionando".
- Menú como template SaaS vs pieza de diseño con identidad del local.
- Landing genérica vs experiencia memorable (mesa servida).

### El número incómodo
Cuadra: $40.000/mes + $350.000 ingreso. Mifud comparable: $8.999/mes. Son 4,4× mensual y ~7,7× el primer año.  
**Respuesta:** Reescribir el Cta con lista de "qué incluye" (diseño, carga, QR impreso, actualización por WhatsApp, cero comisión). Ahí los $40.000 se leen como servicio continuo, no alquiler.

### Aviso estratégico
Mifud es self-service online: cualquier comerciante puede googlearlo esa misma noche y comparar precios. Nuestro foso no es la geografía, es la persona: el día que dude entre $8.999 solo-y-con-panel y $40.000 con-vos-al-lado, gana el que mejor haya explicado qué compra.

## Bitácora de prompts

### Completados
- **Prompt 0** (scaffold + stack + deploy): Vite + React + TS + Tailwind v4 + motion + Aceternity draggable-card. Deploy a Vercel.
- **Prompt 1** (hero inicial): Mantel de fondo, 7 tarjetas, copy, chip de affordance.
- **Prompt 1b** (fix contenido y disposición): Tarjetas acotadas al mantel, sin textos no autorizados.
- **Prompt 1d** (drag restaurado + aleatoriedad): Fix del drag nativo del img, disposición aleatoria por carga.
- **Prompt 1e** (anillo perimetral): Layout en anillo de 8 slots, centro despejado.
- **Prompt 1g** (proporción nativa): Asset completo 576:883, sin recortes.
- **Prompt 1h** (zoom al click): Lightbox centrado al click, cierre por X/ESC/backdrop.
- **Prompt 1i** (zoom a prueba de drag): Fix del click tras drag, gracia anti doble-click.
- **Prompt 2** (Purpose + Cta + Footer): Secciones restantes completadas, flag SHOW_PRICING operativo.

### En cola
- **Prompt 2b** (tarjeta 8): Implementar la tarjeta de invitación con texto "ESTE ESPACIO ES PARA TU NEGOCIO".
- **Prompt 3** (demos vivas): Conectar tarjetas a rutas `/demo/{rubro}` con Google Sheets en tiempo real (refetch cada N segundos).
- **Prompt 4** (pulido estético + medición): Divisor de mantel entre secciones, precio como ticket de compra, pilares con inclinación polaroid, medición Lighthouse para tamaño final de tarjetas.

## Mediciones (pendiente)

| Fecha | Performance | LCP | CLS | Viewport | Nota |
|---|---|---|---|---|---|
| (vacío) | — | — | — | — | Esperando Lighthouse sobre cuardra-one.vercel.app |

## Changelog

- **2026-09-19:** Creación del documento. Registradas visión, decisiones congeladas, decisiones abiertas, análisis de Mifud, bitácora de prompts.