# Registro de Asistencia Estudiantil – Oracle APEX

Prueba técnica para el rol de Desarrollador Junior Oracle APEX.  
La aplicación permite gestionar estudiantes y registrar/consultar su asistencia diaria.

## Estructura del proyecto

- `sql/asistencia.sql`: creación de tablas `ASISTENCIA` con sus restricciones.
- `sql/estudiante.sql`: creación de tablas `ESTUDIANTE` con sus restricciones.
- `sql/data.sql`: inserción de estudiantes y asistencias de prueba.
- `sql/apex.sql`: export de la aplicación APEX en formato SQL.
- `doc/documentación.pdf`: documento con descripción funcional, validaciones y capturas.

## Modelo de datos

### Tabla ESTUDIANTE

- `ID_EST` (NUMBER, PK)
- `NOMBRE` (VARCHAR2(100), NOT NULL)
- `CORREO` (VARCHAR2(120), NOT NULL, UNIQUE)
- `ACTIVO` (CHAR(1), NOT NULL, valores `'S'` / `'N'`)

### Tabla ASISTENCIA

- `ID_ASIST` (NUMBER, PK)
- `ID_EST` (NUMBER, FK → ESTUDIANTE.ID_EST, NOT NULL)
- `FECHA_ASIST` (DATE, NOT NULL)
- `ESTADO` (VARCHAR2(10), NOT NULL, valores `PRESENTE` / `AUSENTE` / `TARDE`)
- `OBSERVACION` (VARCHAR2(200), opcional)

Restricción lógica:
- Única combinación (`ID_EST`, `FECHA_ASIST`) → no se puede registrar más de una asistencia por estudiante y día.

## Páginas de la aplicación

1. **Gestión de Estudiantes**  
   - Interactive Report sobre `ESTUDIANTE`.  
   - Formulario para crear/editar/eliminar estudiantes.  

2. **Reporte de Asistencias**  
   - Interactive Report sobre el join `ASISTENCIA` + `ESTUDIANTE`.  
   - Filtros por rango de fechas y estado (PRESENTE/AUSENTE/TARDE).  
   - Botón **"Nueva Asistencia"** que abre el formulario de registro.

3. **Registro de Asistencia**  
   - Formulario basado en la tabla `ASISTENCIA`.  
   - Estudiante: LOV de `ESTUDIANTE` donde `ACTIVO = 'S'`.  
   - Fecha: `TRUNC(SYSDATE)` por defecto.  
   - Validación para evitar:
     - Fechas futuras.
     - Duplicar asistencia (mismo estudiante + fecha).

## URL de la aplicación

> URL: https://oracleapex.com/ords/r/prueba_tecnica_dti/gesti%C3%B3n-de-estudiantes/home?session=12276321995241

## Autor

- Nombre del candidato: Andrés Felipe García Sosa
