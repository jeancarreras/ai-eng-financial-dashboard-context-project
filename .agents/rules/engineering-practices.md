# Engineering Practices Rules

## 1. Separacion de capas en backend

- Las rutas HTTP no deben concentrar generacion de datos, logica de agregacion y serializacion en el mismo archivo.
- Cada cambio nuevo en backend debe ubicar transporte HTTP, servicios de dominio y proveedores de datos en modulos separados.
- Si una ruta necesita mas de una transformacion relevante, esa logica debe extraerse a una funcion o servicio dedicado y testeable.

## 2. Fuente unica para contratos de dominio

- Los tipos compartidos entre frontend y backend no deben evolucionar en paralelo sin verificacion.
- Cuando un shape de API cambie, el cambio debe reflejarse en ambas capas dentro del mismo trabajo y con pruebas asociadas.
- Priorizar esquemas compartidos, generacion de tipos o una capa de mapeo explicita para reducir drift de contrato.

## 3. UI sin valores duros que contradigan datos reales

- No introducir periodos, labels o estados hardcodeados que puedan contradecir el dataset renderizado.
- Los encabezados y filtros visibles deben derivarse de los datos o de configuracion explicita.
- Mantener consistencia de idioma en toda la interfaz visible al usuario.

## 4. Reproducibilidad de datos mock

- Los datos mock usados para desarrollo o demo deben ser deterministas en el tiempo, no solo por seed.
- Evitar dependencias directas de la fecha actual cuando el objetivo sea comparar pantallas, pruebas o comportamientos entre ejecuciones.
- Si la fecha actual es necesaria, debe inyectarse como dependencia controlable.

## 5. Testing orientado a contrato y casos borde

- Preservar la cobertura actual de happy paths y extenderla con casos borde antes de introducir nuevas rutas o filtros.
- Todo cambio de API debe cubrir al menos un caso nominal, un caso vacio o borde y una asercion de contrato de respuesta.
- En frontend, toda logica de transformacion o formato nueva debe quedar en funciones puras con pruebas unitarias.

## 6. Desarrollo local y tooling del editor

- La documentacion del proyecto debe distinguir entre dependencias del contenedor y dependencias que necesita el editor local.
- Evitar flujos que dejen directorios de trabajo con permisos de root cuando el repo tambien se usa desde VS Code fuera del contenedor de la app.
- Si una configuracion de TypeScript depende de tipos externos, debe existir una instruccion clara para restaurarlos localmente.

## 7. Patrones que conviene preservar

- Mantener modelos de respuesta tipados en backend.
- Mantener utilidades puras y probadas para calculos financieros en frontend.
- Mantener proxy local de Vite para reducir configuracion manual.
- Mantener componentes de dashboard reutilizables con estados de carga consistentes.