# Jenkins Pipeline para Despliegue de Ramas

Este repositorio contiene un script de pipeline para Jenkins diseñado para desplegar ramas específicas en un servidor remoto utilizando SSH. El pipeline permite la selección dinámica de ramas y proporciona comentarios detallados durante la ejecución.

---

## Características

- **Selección Dinámica de Ramas**: Permite al usuario especificar la rama a desplegar a través de un parámetro del pipeline.  
- **Visualización de Información de la Construcción**: Captura y muestra detalles clave de la construcción, incluida la rama a desplegar y el usuario que la activó.  
- **Despliegue Remoto vía SSH**: Ejecuta un script de despliegue en un servidor remoto utilizando SSH.  
- **Manejo de Errores**: Valida la ejecución del comando SSH y proporciona mensajes de error significativos en caso de fallos.

---

## Descripción General del Pipeline

El pipeline se divide en dos etapas principales:

### 1. **Información de la Construcción**
- Captura detalles sobre quién activó la construcción, incluido el usuario.
- Actualiza el nombre visible de la construcción en Jenkins con información relevante:
  - Número de construcción.
  - Rama a desplegar.
  - Usuario que activó la construcción.

### 2. **Despliegue**
- Ejecuta un script de despliegue remoto mediante SSH, pasando la rama seleccionada como parámetro.
- Valida el resultado del comando SSH.
- Gestiona excepciones para asegurar una correcta notificación de errores.

---

## Requisitos Previos

### 1. Configuración en Jenkins
- Una instancia de Jenkins capaz de ejecutar pipelines.
- La clave SSH del usuario de Jenkins añadida al archivo `authorized_keys` del servidor remoto.

### 2. Configuración del Servidor Remoto
- El servidor debe tener disponible y ejecutable el script de despliegue (`deploy.sh`).
- El script debe soportar el despliegue de ramas. Ejemplo de script:

```bash
#!/bin/bash
BRANCH=$1
echo "Desplegando la rama: $BRANCH"
git checkout $BRANCH
git pull origin $BRANCH
# Añadir aquí los pasos de despliegue
---

## Uso

### Parámetros del Pipeline
El pipeline requiere el siguiente parámetro:
- **BRANCH**: El nombre de la rama a desplegar.

### Ejemplo de Ejecución
1. Ejecuta el pipeline en Jenkins.  
2. Introduce el nombre de la rama (por ejemplo, `main`, `feature-xyz`) en el campo del parámetro `BRANCH`.  
3. Observa el progreso de la construcción y los resultados en la salida de consola de Jenkins.

---

## Manejo de Errores

1. **Validación del Comando SSH**:
   - Asegura que el script de despliegue en el servidor remoto se ejecutó correctamente.
   - Proporciona un mensaje de error si el comando devuelve un código de salida distinto de cero.

2. **Manejo de Excepciones**:
   - Captura excepciones durante la ejecución del pipeline y las reporta con mensajes detallados.

---

## Contribución

Siéntete libre de enviar _issues_ o _pull requests_ para proponer mejoras al pipeline.

---

## Licencia

Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo [LICENSE](LICENSE) para más detalles.
