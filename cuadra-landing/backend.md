# 🔧 Icaria — Evaluación de Backend

**Creado:** 2026-09-19  
**Estado:** Candidato: Turso (visión), no decisión final  
**Última actualización:** 2026-09-19

## Problemas de backends actuales

### Firebase (Firestore)
**Experiencia:** Negocio con 600 artículos en producción.  
**Problema:** Cuota de lectura impredecible y cara. Cada consulta al catálogo suma lecturas; con tráfico moderado, la factura mensual se dispara.  
**Veredicto:** No vuelve.

### Google Sheets
**Experiencia:** Negocio con 100 artículos en producción.  
**Problema:** Frágil para producción. Sin transacciones, sin queries reales, sin control de concurrencia, sin historial de cambios.  
**Veredicto:** Aceptable para fase 1 como editor del comerciante (bajo costo, herramienta familiar), pero no como base de datos de servicio.

### Supabase
**Experiencia:** Free tier con cold start.  
**Problema:** La base de datos se duerme tras inactividad; la primera consulta tarda varios segundos en despertar. Experiencia de usuario rota.  
**Veredicto:** No vuelve en su forma actual.

## Turso — Candidato principal

**Descubierto:** 2026-09-19, 6:30, estudiando.  
**Convicción:** "Es Turso."

### Por qué Turso

| Problema de otros | Cómo lo resuelve Turso |
|---|---|
| Firebase caro por lectura | Lectura ilimitada en free tier (9B filas/mes) |
| Supabase se duerme | Wake time instantáneo (no hay cold start) |
| Sheets sin queries | SQL real, transacciones, índices |
| Vendor lock-in | libSQL es open source (fork de SQLite) |
| Deploy en el edge | Replicas globales, latencia baja |

### Arquitectura propuesta (fase 2)
