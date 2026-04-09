# New Skill — Guía de Creación

## Estructura mínima

```
.claude/skills/<nombre>/
  <nombre>.md   # instrucciones que Claude lee
```

Si el skill necesita datos externos (índice, scripts): añadir archivos adicionales en la misma carpeta.

---

## Plantilla de skill

```markdown
# <Nombre> Skill — <Propósito en una línea>

## Cuándo usar
<condición que activa este skill>

---

## <Sección de contenido>
<referencia, tabla, pasos, etc.>
```

---

## Registro en CLAUDE.md

Añadir bajo la sección correspondiente (o crear nueva):

```markdown
## <Nombre> Skill

Ver `.claude/skills/<nombre>/<nombre>.md` cuando <condición de activación>.
```

---

## Reglas

- El `.md` del skill solo contiene lo que Claude necesita leer, no documentación para humanos
- Si hay documentación para humanos, va en un `README.md` separado dentro de la carpeta
- Nombre de carpeta y archivo en kebab-case, coincidentes
- La condición de activación en CLAUDE.md debe ser específica para evitar lecturas innecesarias
