# Cómo habilitar el esquema (outline) en VS Code para documentos LaTeX

## Problema
Al trabajar con documentos LaTeX en VS Code, muchos usuarios no pueden ver el esquema o tabla de contenidos en la barra lateral, una característica que sí está disponible en editores como Overleaf.

## Causa del problema
El problema principal era una configuración incorrecta o incompleta en VS Code para la extensión LaTeX Workshop, que es la que proporciona la funcionalidad de esquema para archivos LaTeX.

## Solución

### 1. Instalar la extensión necesaria
Asegúrate de tener instalada la extensión "LaTeX Workshop" de James Yu en VS Code.

### 2. Configuración de settings.json
Agrega o modifica las siguientes líneas en tu archivo de configuración de VS Code (`settings.json`):

```json
{
    "[latex]": {
        "editor.defaultFormatter": "nickfode.latex-formatter"
    },
    
    // Configuración de LaTeX Workshop
    "latex-workshop.view.pdf.viewer": "tab",
    "latex-workshop.latex.autoBuild.run": "onFileChange",
    "latex-workshop.latex.clean.command": "pdflatex -interaction=nonstopmode -file-line-error -synctex=1",
    
    // Configuración del esquema (outline)
    "latex-workshop.view.outline.visible": true,
    "latex-workshop.view.outline.showSectionsInMiniMap": true,
    "latex-workshop.view.outline.showFiles": true,
    "latex-workshop.view.outline.icons": true,
    "latex-workshop.view.outline.sections": [
        "part*",
        "chapter*",
        "section*",
        "subsection*",
        "subsubsection*",
        "part",
        "chapter",
        "section",
        "subsection",
        "subsubsection"
    ],
    
    // Configuración de compilación
    "latex-workshop.latex.recipe.default": "pdflatex -> bibtex -> pdflatex x2",
    "latex-workshop.latex.recipes": [
        {
            "name": "pdflatex -> bibtex -> pdflatex x2",
            "tools": ["pdflatex", "bibtex", "pdflatex", "pdflatex"]
        },
        {
            "name": "pdflatex",
            "tools": ["pdflatex"]
        }
    ],
    
    "latex-workshop.latex.tools": [
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": ["%DOCFILE%"]
        }
    ],
    "workbench.editorAssociations": {
        "*.copilotmd": "vscode.markdown.preview.editor",
        "*.pdf": "latex-workshop-pdf-hook"
    },
}
```

### 3. Cómo acceder al esquema
Una vez configurado, puedes acceder al esquema de estas formas:

1. **Usando el icono de la barra lateral**:
   - Haz clic en el icono de "Estructura" o "Outline" en la barra lateral (parece un documento con líneas)

2. **Usando el comando de paleta**:
   - Presiona `Ctrl+Shift+P` (o `Cmd+Shift+P` en Mac)
   - Escribe "LaTeX Workshop: Focus on Outline View" y presiona Enter

3. **Desde el menú contextual**:
   - Haz clic derecho en el editor
   - Selecciona "Mostrar esquema" o "Show Outline"

## Explicación de la solución

1. **Configuración del esquema**:
   - `view.outline.visible`: Hace visible el esquema en la barra lateral
   - `view.outline.sections`: Define qué niveles de secciones se mostrarán en el esquema
   - `view.outline.showSectionsInMiniMap`: Muestra las secciones en el minimapa del editor
   - `view.outline.showFiles`: Muestra los archivos en el esquema
   - `view.outline.icons`: Muestra iconos junto a los elementos del esquema

2. **Configuración de compilación**:
   - Se configuró `pdflatex` como compilador por defecto
   - Se agregaron recetas de compilación que incluyen `bibtex` para referencias
   - Se habilitó la compilación automática al guardar cambios

## Solución de problemas

Si el esquema no aparece después de estos pasos:

1. Asegúrate de que el documento tiene secciones definidas con `\section{}`, `\subsection{}`, etc.
2. Guarda el documento para que se actualice el esquema
3. Verifica que no hay errores en el archivo `settings.json`
4. Reinicia VS Code después de hacer cambios en la configuración

## Conclusión
Con esta configuración, tendrás una experiencia similar a Overleaf, pudiendo navegar fácilmente por las diferentes secciones de tu documento LaTeX directamente desde la barra lateral de VS Code.
