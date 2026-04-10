# CONFIGURACIÓN INICIAL

Si el usuario solicita inicialización y este archivo contiene el título "CONFIGURACION INICIAL", primeramente lee y entiende toda la configuración, luego realice la instalacion de Skills, una vez se hayan instalado correctamente reestructura todo el CLAUDE.md con las siguientes secciones:

---
## Instalación de Skills

Repositorio oficial:
https://github.com/anthropics/skills

Las skills se encuentran dentro del directorio:
`skills/`

---

### Procedimiento de instalación automática

1. Crear la carpeta local de skills (si no existe):
```bash
mkdir -p .claude/skills
```
Clonar el repositorio temporalmente:
```bash
git clone https://github.com/anthropics/skills.git temp-skills
Definir las skills a instalar:
SKILLS=(
  skill-creator
  frontend-design
  webapp-testing
  doc-coauthoring
  internal-comms
  pdf
  docx
  xlsx
)
```
Instalar automáticamente solo las skills seleccionadas:
```bash
for skill in "${SKILLS[@]}"; do
  SRC="temp-skills/skills/$skill"
  DEST=".claude/skills/$skill"

  if [ ! -d "$SRC" ]; then
    echo "Skill no encontrada: $skill"
    continue
  fi

  if [ -d "$DEST" ]; then
    echo "Ya existe, se omite: $skill"
    continue
  fi

  cp -r "$SRC" ".claude/skills/"
  echo "Instalada: $skill"
done
```
Limpiar archivos temporales:
```bash
rm -rf temp-skills
```
### Reglas
- **No duplicar** skills ya existentes
- **Verificar** que los nombres coincidan exactamente con los del repositorio oficial
- Fallos en una skill **no deben detener** la instalación del resto
- El proceso debe ser **idempotente** (puede ejecutarse múltiples veces sin efectos secundarios)

> **Nota** Una vez se haya realizado correctamente esta sección, se borrará del CLAUDE.md


## 1. Datos Iniciales

- **Nombre:** Gerard Grau
- **Edad:** 22
- **Rol:** Programador

### Proyectos actuales
- Analizar la raíz del proyecto si hay acceso a archivos.
- Si no hay acceso, solicitar al usuario la estructura del proyecto.
- Listar nombres de proyectos detectados.

---

## 2. Uso de Skills

- **skill-creator**  
  Crear nuevas skills cuando una tarea sea repetitiva o automatizable.

- **frontend-design**  
  Diseñar o mejorar interfaces, estilos, layout y experiencia de usuario.

- **webapp-testing**  
  Testing end-to-end, validación de flujos y debugging en navegador.

- **doc-coauthoring**  
  Crear, editar o estructurar documentación técnica o funcional.

- **internal-comms**  
  Redacción de mensajes, documentación interna y comunicación clara.

- **pdf / docx / xlsx**  
  Generación o manipulación de documentos estructurados.

---

## 3. Estrategia de uso de Skills

- Priorizar solución sin skill si es trivial
- Usar skills solo cuando aporten ventaja clara
- Evitar uso innecesario de múltiples skills
- Mantener contexto claro antes de utilizarlas

---

## 4. Descripción de Proyectos

Analizar proyectos disponibles.

Formato:

### <Nombre del Proyecto>
- **Tecnologías**: Lista de tecnologías principales
- **Resumen y funcionalidades**: Descripción breve clara del proyecto

Si no hay acceso al código, solicitar información al usuario.

---

## 5. Prácticas vitales

- Pensar antes de actuar
- Leer archivos antes de modificarlos
- **NO** usar emojis en ningún caso
- Ser conciso en output, riguroso en razonamiento
- Preferir editar sobre reescribir
- No releer archivos innecesariamente
- Verificar código antes de finalizar
- Sin introducciones ni cierres innecesarios
- Soluciones simples y directas
- Al terminar correctamente, recomendar usar `/CLEAR`

---

## 6. Buenas prácticas

- Código bien indentado y consistente
- Incluir comandos relevantes cuando aplique
- Minimizar tokens sin perder claridad
- Comentarios solo cuando aporten valor
- No comentar lo obvio
- Optimizar sin cambiar comportamiento
- Mantener estructura, estilos y lógica intactos al optimizar
- Las instrucciones del usuario siempre prevalecen

---

## 7. Restricciones absolutas

- PROHIBIDO cualquier acción de producción (deploy, push, merge, etc.)

Una vez hayas terminado con todo, si CLAUDE.md no está en la carpeta .claude/, mueve el archivo a la carpeta


