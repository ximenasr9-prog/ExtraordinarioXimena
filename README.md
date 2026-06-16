# ExtraordinarioXimena
Extraordinario Amerike Ximena Senties Ruiz
## Sistema de Gestión de Finanzas Personales
## 1. Descripción del problema


## 2. Diagrama de flujo 
```mermaid
flowchart TD

A([Inicio]) --> B[Inicializar colección de movimientos]

B --> C[Seleccionar operación]

C --> D{¿Qué desea realizar?}

D -->|Registrar movimiento| E[Solicitar descripción, monto, categoría y tipo]

E --> F[Validar datos del movimiento]

F --> G{¿Datos válidos?}

G -->|Sí| H[Crear movimiento]
H --> I[Agregar movimiento a la colección]
I --> C

G -->|No| J[Mostrar mensaje de error]
J --> C


D -->|Consultar movimientos por categoría| K[Solicitar categoría]

K --> L[Buscar movimientos de la categoría]
L --> M[Mostrar resultados]
M --> C


D -->|Generar reporte| N[Calcular ingresos, gastos y balance]

N --> O[Generar y mostrar reporte]
O --> C


D -->|Salir| P([Fin])
```

## 3. Pseudocódigo

### Módulo de validación
validarMonto()
validarCategoria()
validarTipo()

### Módulo de datos
crearMovimiento()
agregarMovimiento()

### Módulo de cálculo
calcularGastoPorCategoria()
calcularTotalIngresos()
calcularTotalGastos()
calcularBalance()
determinarMayorGasto()

### Módulo de presentación
mostrarMovimientosCategoria()
generarReporte()
mostrarAdvertencia()