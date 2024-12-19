# Pipeline de Jenkins para Despliegue de Ramas

Este repositorio contiene un script de pipeline de Jenkins diseñado para desplegar ramas específicas en un servidor remoto usando SSH. El pipeline permite una selección dinámica de ramas y proporciona retroalimentación detallada durante su ejecución.

---

## Características

- **Selección Dinámica de Ramas**: Permite al usuario especificar la rama a desplegar a través de un parámetro del pipeline.
- **Visualización de Información de la Construcción**: Captura y muestra detalles clave de la construcción, incluyendo la rama que se está desplegando y el usuario que activó la construcción.
- **Despliegue Remoto vía SSH**: Ejecuta un script de despliegue en un servidor remoto usando SSH.
- **Manejo de Errores**: Valida la ejecución de comandos SSH y proporciona mensajes de error significativos en caso de fallos.

---

## Visión General del Pipeline

El pipeline se divide en dos etapas principales:

### 1. **Información de la Construcción**
- Captura detalles sobre el disparador de la construcción, incluyendo el usuario que la inició.
- Actualiza el nombre de la construcción en Jenkins con la información relevante:
  - Número de la construcción
  - Rama que se está desplegando
  - Usuario que disparó la construcción

### 2. **Despliegue**
- Ejecuta un script de despliegue remoto vía SSH, pasando la rama seleccionada como parámetro.
- Valida el resultado del comando SSH.
- Captura y maneja excepciones para asegurar una correcta reportación de errores.

---

## Requisitos Previos

1. **Configuración de Jenkins**:
   - Una instancia de Jenkins con capacidad para ejecutar pipelines.
   - La clave SSH del usuario de Jenkins debe estar añadida a las claves autorizadas del servidor remoto.

2. **Servidor Remoto**:
   - El servidor debe tener el script de despliegue (`deploy.sh`) disponible y ejecutable.
   - El script debe soportar el despliegue de ramas. Por ejemplo:
     ```bash
     #!/bin/bash
     BRANCH=$1
     echo "Desplegando la rama: $BRANCH"
     git checkout $BRANCH
     git pull origin $BRANCH
     # Añadir pasos de despliegue aquí
     ```

---

## Uso

### Parámetros del Pipeline
El pipeline requiere el siguiente parámetro:
- **BRANCH**: El nombre de la rama a desplegar.

### Ejecución de Ejemplo
1. Dispara el pipeline en Jenkins.
2. Introduce el nombre de la rama (por ejemplo, `main`, `feature-xyz`) en el campo de parámetro `BRANCH`.
3. Observa el progreso y los resultados de la construcción en la salida de consola de Jenkins.

---

## Detalles del Script

---

## Manejo de Errores

1. **Validación del Comando SSH**:
   - Asegura que el script de despliegue en el servidor remoto se haya ejecutado correctamente.
   - Proporciona un mensaje de error si el comando devuelve un código de salida distinto de cero.

2. **Manejo de Excepciones**:
   - Captura las excepciones durante la ejecución del pipeline y las reporta con mensajes detallados.

---

## Contribuciones

No dudes en enviar problemas o solicitudes de extracción para mejorar el pipeline.

---

## Licencia

Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo [LICENSE](LICENSE) para más detalles.
