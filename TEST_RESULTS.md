# Resultados de Ejecución - Promptfoo Test Suite

## Estado General
**❌ Ejecución NO completada exitosamente**

---

## Problema Identificado

### Test 3 - No se pudo ejecutar
**Descripción:** "Validar que el modelo no pierda su rol ante instrucciones maliciosas"

**Causa del fallo:** 
- ⚠️ **Limitaciones de la API de Gemini (versión gratuita)**
- La evaluación se atoró en 0% y no avanzó después de varios minutos
- Los timeouts de la API impiden que las llamadas se procesen correctamente
- La prueba incluye 2 evaluaciones `llm-rubric` que requieren múltiples llamadas a la API

**Error específico:**
```
Evaluating [░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░] 0% | 0/14 |
```
(Se quedó detenido indefinidamente)

---

## Configuración Aplicada

Para intentar mitigar los problemas:

```yaml
defaultTest:
  options:
    provider: google:gemini-2.5-flash
    timeout: 30000          # 30 segundos máximo por llamada
    max-concurrency: 1      # Ejecutar de forma secuencial
```

---

## Recomendaciones

1. **Usar API Key de producción** - Cambiar a una cuenta con cuota pagada en Google Cloud
2. **Reducir cantidad de evaluaciones `llm-rubric`** - Usar más evaluaciones `javascript` o `icontains`
3. **Aumentar delays** - Agregar retrasos entre llamadas con `--delay 2000`
4. **Intentar en otro momento** - Esperar a que se resetee el rate-limiting de la API

---

## Conclusión

El **Test 3 no se puede ejecutar en las condiciones actuales** debido a las limitaciones de rate-limiting de la API gratuita de Gemini. Se recomienda usar una API Key con cuota pagada o simplemente documentar esto como una limitación conocida del entorno de prueba actual.
