# ENTREGABLES: SISTEMA DE SOPORTE TÉCNICO AUTOMATIZADO CON IA

**Proyecto:** Automatización de soporte técnico con N8N, Notion y Cohere  
**Responsable:** Vicky Caparroz  
**Fecha:** Septiembre 2026  
**Versión:** 1.0

---

## 📋 DESCRIPCIÓN GENERAL

Este paquete contiene **5 documentos profesionales** que describen la arquitectura, operación, costos, seguridad y control de un **sistema automatizado de soporte técnico** que utiliza:

- **N8N:** Orquestación y flujo de trabajo
- **Notion:** Base de datos central (Tickets + Knowledge Base)
- **Cohere API:** Modelo de IA (Command R) para análisis y clasificación
- **Gmail:** Envío de respuestas a usuarios
- **Human-in-the-Loop (HITL):** Validación manual de calidad

**Flujo:** Google Sheets (entrada) → Notion (BD) → N8N (orquestación) → Cohere IA → HITL (revisión) → Gmail (respuesta)

---

## 📁 CONTENIDO DEL PAQUETE

### 1️⃣ **DIAGRAMA_ARQUITECTURA.pdf** (38 KB)
**Diagrama visual de la arquitectura del sistema**

**Contiene:**
- Capas del sistema (entrada, procesamiento, salida, errores, monitoreo)
- Flujo de datos desde Google Sheets hasta Gmail
- Componentes: Triggers, APIs, nodos IA, gestión de errores
- Integraciones autenticadas (credenciales)
- Leyenda de seguridad y datos

**Para quién:** Ejecutivos, arquitectos, stakeholders que necesitan entender el big picture

**Caso de uso:** Presentaciones, documentación de arquitectura, aprobaciones

---

### 2️⃣ **MANUAL_OPERATIVO_DATOS.pdf** (15 KB)
**Guía técnica completa de bases de datos y esquemas**

**Contiene:**

1. **Arquitectura de BD (Notion)**
   - Tabla TICKETS: 13 campos con tipos, descripciones, ejemplos
   - Tabla Base Conocimiento (KB): 11 campos, 8 artículos activos
   - Tabla Google Sheets: Estructura de entrada

2. **Esquemas JSON de integración**
   - Input: Google Sheets → N8N
   - Process: Agente IA output
   - Output: N8N → Notion
   - Output: N8N → Gmail

3. **Mapeo de datos completo**
   - Google Sheets ↔ Notion (cada columna)

4. **Manejo de errores**
   - Error Handlers por nodo
   - Tabla de registro de errores

5. **Flujo de datos sequence** (paso a paso)

6. **Consideraciones de seguridad**
   - Minimización de PII
   - Validación de datos
   - Control de acceso

7. **Monitoreo y auditoría**
   - Qué se registra automáticamente
   - Qué se registra manualmente
   - Auditoría mensual checklist

**Para quién:** Desarrolladores, DBAs, técnicos de N8N, DBA

**Caso de uso:** Implementación, debugging, mantenimiento, troubleshooting

---

### 3️⃣ **MATRIZ_COSTOS.pdf** (14 KB)
**Análisis financiero completo del sistema**

**Contiene:**

1. **Resumen ejecutivo**
   - Costo total mensual y anual
   - Desglose por componente (Cohere, N8N, Notion, HITL, etc)

2. **Desglose por integración**
   - Cohere API: cálculo detallado por tokens ($0.00188/ticket)
   - N8N Cloud: análisis de ejecuciones vs tier
   - Notion: costo por usuarios y plan
   - Google Workspace, Gmail, Google Sheets

3. **Análisis de modelos IA**
   - Cohere Command R (actual): $0.0005 in / $0.0015 out
   - Alternativas evaluadas: Claude, GPT-4o-mini, Llama
   - Comparativa costo/beneficio
   - Recomendación: Cohere es óptimo

4. **Human-in-the-Loop**
   - Costo por horas (8-10 hrs/mes @ $50/hr)
   - Oportunidades de automatización

5. **Proyecciones de escenarios**
   - Pequeño: 100 tickets/mes = $450/mes
   - Mediano: 500 tickets/mes = $701/mes ← **ACTUAL**
   - Grande: 2000 tickets/mes = $1.954/mes

6. **Oportunidades de ahorro**
   - Cambiar a GPT-4o-mini: -15% precisión, -$120/año
   - Autoaprobal inteligente: +30% eficiencia, +$1.500/año ahorro
   - Batch API: -20% tokens, +$50-100/año ahorro
   - Optimización prompt: -15% tokens, +$30-50/año ahorro

7. **ROI y justificación**
   - Costo implementación: $8.411/año
   - Ahorro por eficiencia: $18.000/año
   - **ROI neto año 1: $9.589 (114%)**

8. **Build vs Outsource**
   - Build (actual): $8.411/año, control total
   - Outsource (SaaS): $15-30K/año, menos control
   - Decisión: BUILD es 50% más económico

**Para quién:** CFO, gerentes de presupuesto, ejecutivos, vendedores (ROI)

**Caso de uso:** Justificación de presupuesto, comparativas, escalamiento

---

### 4️⃣ **SEGURIDAD_RESILIENCIA.pdf** (22 KB)
**Documentación completa de seguridad, cumplimiento y disaster recovery**

**Contiene:**

1. **Minimización de PII**
   - Datos capturados (solo: nombre, email, sector, descripción)
   - Datos NO capturados (teléfono, DNI, domicilio, datos médicos)
   - Ciclo de vida de datos (captura → migración → procesamiento → almacenamiento)
   - Conformidad GDPR/CCPA (Argentina)

2. **Encriptación en tránsito**
   - HTTPS nativo en todas las APIs
   - OAuth2 para Google Sheets y Gmail
   - Certificados SSL verificados

3. **Encriptación en reposo**
   - Notion: AES-256
   - N8N: Credenciales encriptadas
   - Gmail: Encriptación Google nativa

4. **Manejo de errores y resiliencia**
   - Error Handlers detallados por nodo
   - Tabla de Registro de Errores (Notion)
   - Reintentos automáticos (Gmail x2)
   - Fallbacks: Usar KB en caché, plantilla genérica

5. **Human-in-the-Loop**
   - Proceso de aprobación (3 opciones)
   - Criterios de validación (5 puntos)
   - Rúbrica de calidad (✓/✗)
   - Métricas HITL (% aprobación, tiempo revisión)

6. **Auditoría y logging**
   - Qué se registra automáticamente (N8N, Notion, Gmail, Errors)
   - Qué se registra manualmente (HITL, rechazo, escalamiento)
   - Auditoría recomendada (mensual)

7. **Disaster Recovery**
   - Escenarios críticos (Notion down, N8N down, Cohere down, etc)
   - RTO por escenario
   - Plan de backup (Notion diario, N8N semanal)
   - Restoration procedure (1-2 horas con backup)

8. **Rate Limiting**
   - Límites por proveedor (Cohere, Notion, Gmail)
   - Configuración actual (segura, sin risk)

9. **Incident Response**
   - Escalation tree (3 niveles)
   - Incident Log template
   - Email notificación de breach

10. **Checklist de seguridad**
    - Diario (5 min)
    - Semanal (15 min)
    - Mensual (30 min)
    - Trimestral (rotación credenciales)

11. **Conformidad y certificaciones**
    - No requiere SOC2, ISO27001, HIPAA
    - Recomendado: GDPR checklist, Privacy policy, DPA

**Para quién:** CISO, seguridad IT, auditoría, compliance, abogados

**Caso de uso:** Auditorías de seguridad, conformidad normativa, incident response

---

### 5️⃣ **DASHBOARD_CONTROL.pdf** (19 KB)
**Guía para crear y mantener dashboard de KPIs en Notion**

**Contiene:**

1. **KPIs definidos (4 categorías)**

   a) **Volumen y velocidad**
   - Tickets recibidos/día (target: 15-25)
   - Tickets procesados/día (target: 80% recibidos)
   - Tickets aprobados/día (target: 70-80% procesados)
   - Tiempo promedio (target: <4 hrs)

   b) **Calidad**
   - Tasa rechazo HITL (target: <5%)
   - Tasa escalamiento (target: <10%)
   - Tiempo revisión (target: <2 hrs)
   - % aprobación por categoría

   c) **Confiabilidad**
   - Tasa error N8N (target: <2%)
   - Uptime flujo (target: >99%)
   - Errores API (target: 0-1/día)
   - Emails entregados (target: >98%)

   d) **Negocio**
   - Costo por ticket (target: <$1.50)
   - Eficiencia IA vs manual (target: >70%)
   - ROI acumulado (target: >100% año 1)
   - Satisfacción HITL (target: >80%)

2. **Crear dashboard en Notion (paso a paso)**
   - Crear página "📊 Dashboard Control"
   - 4 tablas: Tickets Daily, Error Log, HITL Performance, KB Analytics
   - Crear vistas gráficas (Charts nativo)
   - Estructura visual del dashboard

3. **Fórmulas Notion para automatizar**
   - Contar tickets hoy
   - Tasa aprobación %
   - Tickets >24h sin procesar
   - Tiempo promedio en horas

4. **Alertas automáticas**
   - Alerta 1: Tasa error alta
   - Alerta 2: Tickets sin respuesta >48h
   - Alerta 3: Sin ejecuciones N8N
   - Alerta 4: Tasa rechazo alta
   - Alerta 5: Falta de backup
   - Configurar en N8N con Slack/Email

5. **Enlace público del dashboard**
   - Crear Shared View pública
   - Compartir con stakeholders (3 niveles: exec, ops, HITL)

6. **Monitoreo activo**
   - Rutina diaria (5 min)
   - Rutina semanal (15 min, reunión)
   - Rutina mensual (30 min, reporte)

7. **Ejemplo de dashboard actual**
   - Métricas reales (500 tickets/mes)
   - Status: ✅ Todos OK

8. **Integración con otras herramientas**
   - Google Sheets + Notion (IMPORTRANGE)
   - Power BI / Looker (futuro, si escala)
   - Slack integration (comandos)

9. **Mejoras futuras**
   - Machine Learning (predicción)
   - Slack nativo
   - Alertas automáticas
   - Dashboard móvil
   - Exportar reportes (PDF)

**Para quién:** Operaciones, gerentes de proyecto, stakeholders

**Caso de uso:** Monitoreo diario, reportes ejecutivos, toma de decisiones

---

## 🎯 CÓMO USAR ESTOS DOCUMENTOS

### Por rol:

**👔 EJECUTIVOS / CFO**
- Leer: Diagrama + Matriz de Costos
- Focus: ROI, uptime, costo/ticket
- Tiempo: 10-15 minutos

**🔧 DESARROLLADORES / TECH LEAD**
- Leer: Todas (pero especialmente Manual de Datos + Seguridad)
- Focus: Arquitectura, schemas, error handling, disaster recovery
- Tiempo: 1-2 horas

**📊 OPERACIONES / GERENTE DE PROYECTO**
- Leer: Dashboard + Matriz de Costos
- Focus: KPIs, alertas, monitoreo, escalamiento
- Tiempo: 30 minutos

**🔐 CISO / AUDITORÍA**
- Leer: Seguridad y Resiliencia
- Focus: PII, encriptación, cumplimiento, incident response
- Tiempo: 1 hora

**👥 REVISOR HITL**
- Leer: Manual de Datos + Dashboard (tu métrica personal)
- Focus: Criterios de validación, desempeño personal
- Tiempo: 15 minutos

---

## 🚀 PRÓXIMOS PASOS

1. **Revisión ejecutiva**
   - Enviar Diagrama + Matriz de Costos a stakeholders
   - Obtener aprobación presupuesto

2. **Implementación técnica**
   - Seguir Manual de Datos para crear BD en Notion
   - Implementar error handlers (Seguridad)
   - Desplegar flujo N8N

3. **Operación**
   - Crear Dashboard en Notion
   - Configurar alertas
   - Entrenar HITL en criterios

4. **Monitoreo**
   - Rutinas diarias/semanales/mensuales
   - Auditoría trimestral
   - Ajustes según KPIs

---

## 📞 CONTACTO Y SOPORTE

**Responsable del sistema:** Vicky Caparroz  
**Email:** vicky.caparroz@gmail.com  
**LinkedIn:** [link]

Para preguntas sobre:
- **Arquitectura:** Tech Lead
- **Datos:** DBA / Notion expert
- **Costos:** CFO
- **Seguridad:** CISO
- **Operación:** Project Manager

---

## 📜 CONTROL DE VERSIONES

| Versión | Fecha | Cambios |
|---------|-------|---------|
| 1.0 | Sept 2026 | Documento inicial |

---

**Nota de confidencialidad:** Estos documentos contienen información técnica y financiera sensible. Distribuir solo a stakeholders autorizados.

---

**Última actualización:** Septiembre 6, 2026
