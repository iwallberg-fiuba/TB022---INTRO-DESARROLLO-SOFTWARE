

Pending.

### Niveles de Testing

```txt
Unit Testing
├─ Component Testing
├─ API Testing
├─ Schema Testing
└─ Data Validation Testing

Integration Testing
├─ Frontend ↔ Backend
├─ Backend ↔ DB
└─ Servicio ↔ Servicio

End-to-End Testing (E2E)

User Acceptance Testing (UAT)
```

| Nivel                             | Qué prueba                                                                              |
| --------------------------------- | --------------------------------------------------------------------------------------- |
| **Unit Testing**                  | La unidad más pequeña de código de forma aislada (función, método, clase o componente). |
| **Integration Testing**           | La comunicación e interacción entre múltiples módulos, servicios o capas.               |
| **End-to-End (E2E) Testing**      | Flujos reales de usuario atravesando todas las capas del sistema.                       |
| **User Acceptance Testing (UAT)** | Que el sistema cumpla los requisitos funcionales y expectativas del usuario o cliente.  |

Nota: System Testing (que viene después de Integration Testing) no es necesario en este caso porque con E2E Testing es suficiente.



Testings según capa

El testing se realiza de forma progresiva, pero no siempre completamente secuencial: algunas pruebas pueden solaparse entre capas a medida que el sistema crece.

```txt
Frontend
├─ Component Testing
├─ UI Testing
└─ E2E Testing

Backend
├─ Unit Testing
├─ API Testing
└─ Integration Testing

Base de Datos
├─ Schema Testing
├─ Data Validation Testing
└─ Migration Testing

Sistema Completo
├─ E2E Testing
└─ UAT
```

| Tipo                        | Capa          | Nivel al que suele pertenecer | Qué prueba                                                        |
| --------------------------- | ------------- | ----------------------------- | ----------------------------------------------------------------- |
| **Component Testing**       | Frontend      | Unit Testing                  | Un componente de interfaz de forma aislada.                       |
| **API Testing**             | Backend       | Unit / Integration Testing    | Endpoints, requests, responses, validaciones y códigos de estado. |
| **Schema Testing**          | Base de Datos | Unit Testing                  | Tablas, columnas, relaciones, índices y estructura general.       |
| **Data Validation Testing** | Base de Datos | Unit Testing                  | Constraints, claves, tipos de datos y reglas de integridad.       |
| **UI Testing**              | Frontend      | Unit / System Testing         | Elementos visuales, navegación e interacción de la interfaz.      |
| **Migration Testing**       | Base de Datos | Unit / Integration Testing    | Scripts de creación, actualización y migración de esquemas.       |


Los tests de unidad se hacen durante todo el desarrollo.  
Los tests de integración aparecen cuando dos o más partes empiezan a comunicarse.  
Los tests E2E y UAT se hacen cuando el sistema ya tiene flujos completos funcionando.


## Frontend

En el frontend, los tests se enfocan en validar componentes, pantallas e interacciones del usuario.

1. **Unit Testing**  
   Verifica funciones o lógica aislada del frontend.

2. **Component Testing**  
   Valida que cada componente se renderice y funcione correctamente.

3. **UI Testing**  
   Revisa comportamiento visual e interacción básica de la interfaz.

4. **E2E Testing**  
   Simula flujos completos de usuario conectando frontend, backend y base de datos.

5. **UAT**  
   Verifica que la interfaz y los flujos cumplan con lo esperado por el usuario final.

## Backend

En el backend, los tests se enfocan en validar lógica, rutas, servicios, controladores y conexión con la base de datos.

1. **Unit Testing**  
   Verifica funciones, métodos, servicios o módulos de forma aislada.

2. **Integration Testing**  
   Valida la interacción entre módulos, rutas, servicios y base de datos.

3. **API Testing**  
   Comprueba que los endpoints respondan correctamente.

4. **System Testing**  
   Evalúa el comportamiento del backend dentro del sistema completo.

5. **E2E Testing**  
   Simula flujos completos desde el frontend hasta la base de datos.

6. **UAT**  
   Confirma que el sistema cumple los requisitos funcionales definidos.

## Base de Datos

En la base de datos, los tests se enfocan en validar estructura, relaciones, restricciones y persistencia de datos.

1. **Schema Testing**  
   Verifica que las tablas, columnas, tipos de datos y relaciones estén correctamente definidas.

2. **Data Validation Testing**  
   Comprueba constraints, claves primarias, claves foráneas, `NOT NULL`, `UNIQUE`, etc.

3. **Integration Testing**  
   Valida que el backend pueda leer, insertar, actualizar y eliminar datos correctamente.

4. **Migration / Seed Testing**  
   Comprueba que los scripts de creación e inserción inicial funcionen bien.


## Orden Recomendado

1. Unit Testing (Frontend y Backend)
2. Schema / Data Validation / Migration Testing (DB)
3. Integration Testing (Backend ↔ DB)
4. API Testing
5. Integration Testing (Frontend ↔ Backend)
6. End-to-End Testing (E2E)
7. User Acceptance Testing (UAT)




