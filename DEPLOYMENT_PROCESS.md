# PROCESO DE DESPLIEGUE DE PRUEBAS UNITARIAS

## 1. Introducción y Propósito

El propósito de este documento es detallar el proceso estandarizado para la verificación, construcción y despliegue de las pruebas unitarias asociadas a nuestro código fuente. El objetivo es asegurar que todos los cambios que lleguen a la rama principal (`main`) hayan sido probados de manera automatizada y pasen todos los estándares de calidad definidos.

## 2. Prerrequisitos Técnicos

Antes de iniciar el proceso de despliegue o contribución, asegúrate de tener instaladas y configuradas las siguientes herramientas:

1.  **Git:** Sistema de control de versiones.
2.  **Node.js / Python / [Tu Lenguaje]:** Entorno de ejecución y gestor de paquetes (ej. npm, pip, etc.).
3.  **Herramienta de Pruebas Unitarias:** (Ej. Jest, JUnit, pytest, etc.).
    * *Detalle aquí la herramienta y su versión recomendada.*
4.  **Acceso al Repositorio de GitHub:** Debes tener permisos de clonación y contribución (Push).

## 3. Estrategia de Ramificación (Branching Strategy)

Para mantener la integridad y estabilidad de la base de código, seguimos una estrategia de ramas basada en características:

| Rama | Propósito | Reglas de Fusión |
| :--- | :--- | :--- |
| **`main`** | Código estable, listo para producción. | **Solo se permite la fusión (merge) a través de Pull Requests (PR) aprobados.** |
| **`develop`** | Rama base para la integración de nuevas funcionalidades. | Se fusionan las ramas de característica (`feature/*`). |
| **`feature/<nombre>`** | Se crean para desarrollar una característica o corrección específica. | Se fusionan a `develop` una vez completadas y probadas localmente. |

## 4. Proceso de Desarrollo y Contribución Paso a Paso

### 4.1. Configuración Inicial

1.  **Clonar el Repositorio:**
    ```bash
    git clone [https://github.com/hiroyuki130312/Unit-Test-Deployment.git](https://github.com/hiroyuki130312/Unit-Test-Deployment.git)
    ```
2.  **Instalar Dependencias:**
    ```bash
    # Ejemplo para Node.js
    npm install 
    # Ejemplo para Python
    pip install -r requirements.txt
    ```

### 4.2. Flujo de Trabajo Local (Creación de Cambios)

1.  **Crear una nueva rama de característica:**
    ```bash
    git checkout develop
    git pull origin develop
    git checkout -b feature/mi-nueva-caracteristica
    ```
2.  **Implementar el Código y las Pruebas Unitarias:**
    * Escribe el código de la nueva funcionalidad.
    * **Importante:** Escribe las pruebas unitarias correspondientes.
3.  **Ejecutar las Pruebas Unitarias Localmente:**
    ```bash
    # Comando de ejemplo para ejecutar pruebas
    npm run test 
    # o bien
    python -m pytest
    ```
    * *Solo se procede si todas las pruebas pasan exitosamente.*

4.  **Confirmar (Commit) los Cambios:**
    ```bash
    git add .
    git commit -m "feat: [Descripción clara de la nueva característica]"
    ```
5.  **Subir (Push) los cambios a GitHub:**
    ```bash
    git push origin feature/mi-nueva-caracteristica
    ```

### 4.3. Proceso de Despliegue e Integración (Pull Request)

1.  **Abrir un Pull Request (PR):** Desde GitHub, crea un PR para fusionar la rama `feature/mi-nueva-caracteristica` en la rama **`develop`**.
2.  **Revisión y Aprobación (Merge Rules):**
    * El PR debe ser revisado por un compañero o mentor.
    * **Se requiere al menos 1 aprobación (Approval) antes de que la fusión sea posible.**
    * La revisión incluye verificar: 1) La funcionalidad, 2) La calidad del código, y 3) La cobertura de las pruebas unitarias.
3.  **Fusión (Merge):** Una vez aprobado, el PR se puede fusionar a `develop`.
4.  **Integración a `main`:** La fusión a la rama `main` se realiza únicamente en hitos de lanzamiento estables, a través de un PR final desde `develop` a `main`, siguiendo las mismas reglas de revisión y aprobación.

## 5. Solución de Problemas Comunes (Troubleshooting)

| Problema | Causa más Común | Solución |
| :--- | :--- | :--- |
| **Fusión Bloqueada** | No hay suficientes revisiones de aprobación en el PR. | Pide una revisión adicional a un miembro del equipo. |
| **Pruebas Fallan (Localmente)** | Errores en la lógica del código o en las pruebas recién escritas. | Revisa el *stack trace* del error y depura el código o corrige la prueba. |
| **Conflicto de Fusión (Merge Conflict)** | Dos ramas modificaron las mismas líneas de código. | Resuelve el conflicto manualmente en tu rama local, realiza un nuevo *commit* y sube los cambios. |