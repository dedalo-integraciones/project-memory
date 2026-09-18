# 🌐 Icaria — Visión Arquitectónica

**Creado:** 2026-09-19  
**Estado:** Visión inicial, sin implementación  
**Relación:** Icaria es la plataforma madre; Cuadra es su primer caso de uso.

## ¿Qué es Icaria?

Plataforma multi-uso que puede servir para:
- Pedidos de presupuestos
- Pedidos de comida (Cuadra)
- E-commerce simple
- Cualquier flujo de catálogo + pedidos + notificación por WhatsApp

## Casos de uso en producción (previos a Icaria)

### Negocio 1: 600 artículos en Firebase
**Problema:** Cuota de lectura impredecible y cara. Cada consulta al catálogo suma lecturas; con tráfico moderado, la factura mensual se dispara.  
**Estado actual:** En producción, odiado.

### Negocio 2: 100 artículos en Google Sheets
**Problema:** No da confianza para producción. Sin transacciones, sin queries reales, sin control de concurrencia, sin historial de cambios.  
**Estado actual:** En producción, frágil.

## Por qué Icaria necesita un backend nuevo

Los backends probados tienen problemas estructurales:

- **Firebase:** caro por lectura (Firestore), complejo de configurar, vendor lock-in fuerte.
- **Google Sheets:** frágil, sin transacciones, sin queries, sin control de acceso fino.
- **Supabase:** free tier con cold start (la base de datos se duerme tras inactividad, primera consulta tarda varios segundos).

## Turso como candidato (visión 2026-09-19, 6:30)

**Origen:** Descubrimiento estudiando, convicción matinal.  
**Por qué despierta interés:**
- SQLite serverless (libSQL) con replicas en el edge.
- Lectura ilimitada en free tier (9 billones de filas leídas/mes).
- Wake time instantáneo (no se duerme como Supabase).
- Multitenant natural: cada comercio puede tener su propia DB o su schema dentro de una DB compartida.
- Pareja natural con Vercel (deploy en el edge, mismo stack).

**Estado:** Visión registrada, no decisión tomada. Validar límites y precios contra la doc oficial cuando lleguemos a fase 2 de Cuadra.

## Relación con Sheets (fase 1 vs fase 2)

Sheets sigue siendo el **editor que el comerciante ya sabe usar** en fase 1. Turso entra como **capa de servicio** en fase 2, con un puente de sync, no un acantilado de migración. El comerciante sigue editando su Sheet; Icaria lee de Turso, que se mantiene sincronizada.