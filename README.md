# ExtraordinarioXimena
Extraordinario Amerike Ximena Senties Ruiz
## Sistema de Gestión de Finanzas Personales
## 1. Descripción del problema
Este sistema sirve para que una persona pueda llevar un control claro de su dinero sin complicarse. La idea es que el usuario pueda registrar cada movimiento que hace, ya sea un ingreso o un gasto, y guardarlo junto con una descripción, un monto y una categoría como Alimentación, Transporte, Entretenimiento, Servicios u Otros.

Antes de guardar cualquier movimiento, el sistema revisa que los datos tengan sentido: que el monto sea mayor a cero, que la categoría exista y que el tipo realmente sea ingreso o gasto. Con toda esta información validada, el sistema va acumulando los movimientos y después puede calcular cosas importantes como el total de ingresos, el total de gastos y el balance actual.

Además, el sistema ayuda a entender en qué se está gastando más, mostrando el total por categoría y permitiendo ver solo los movimientos de una categoría específica. Al final, genera un reporte completo donde se ve el estado general del dinero del usuario, incluyendo una advertencia si los gastos ya superaron a los ingresos.


## 2. Diagrama de flujo 
```mermaid
flowchart TD

A([Inicio]) --> B[Inicializar colección de movimientos]

B --> C[Seleccionar operación]
c
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
#### validarMonto()
```text
FUNCION validarMonto(monto)

    SI monto > 0 ENTONCES
        RETORNAR verdadero
    SI NO
        RETORNAR falso
    FIN SI

FIN FUNCION
```
#### validarCategoria()
```text

FUNCION validarCategoria(categoria)
    categoriasValidas = [
        "Alimentos", "Transporte", "Servicios", "Entretenimiento", "Otros"
        ]

    SI categoria ESTA_EN categoriasValidas ENTONCES 
        RETORNAR verdadero
    SI NO
        RETORNAR falso
    FIN SI

FIN FUNCION
```

#### validarTipo()
```text

FUNCION validarTipo(tipo)
    

    SI tipo == "Ingreso" O tipo == "Gasto"
    ENTONCES
        RETORNAR verdadero
    SI NO
        RETORNAR falso
    FIN SI

FIN FUNCION
```

### Módulo de datos
#### registarMovimiento()
```text

FUNCION registrarMovimiento(descripcion,monto,tipo,categoria)
    movimiento.descripcion = descripcion
    movimiento.monto = monto
    movimiento.tipo = tipo
    movimiento.categoria = categoria
    RETORNAR movimiento

FIN FUNCION
```

#### agregarMovimiento()
```text

FUNCION agregarMovimiento(listaMovimientos,movimiento)
    AGREGAR movimiento A listaMovimientos

FIN FUNCION
```

### Módulo de cálculo
#### calcularGastoPorCategoria() 
```text

FUNCION calcularGastoPorCategoria(listaMovimientos)
    gastoCategoria = DICCIONARIO_VACIO
    PARA CADA movimiento EN listaMovimientos HACER 
        SI movimiento.tipo == "Gasto" ENTONCES 
            gastoCategoria[movimiento.categoria] =  gastoCategoria[movimiento.categoria] + movimiento.monto
        FIN SI
    FIN PARA
    RETONAR gastoCategoria

FIN FUNCION
```

#### calcularTotalIngresos()
```text

FUNCION calcularTotalIngresos(listaMovimientos)
    ingresosTotales = 0
    PARA CADA movimiento EN listaMovimientos HACER 
        SI movimiento.tipo == "Ingreso" ENTONCES 
            ingresosTotales = ingresosTotales  + movimiento.monto
        FIN SI
    FIN PARA
    RETONAR ingresosTotales

FIN FUNCION
```
#### calcularTotalGastos()

```text

FUNCION calcularTotalGastos(listaMovimientos)
    gastosTotales = 0
    PARA CADA movimiento EN listaMovimientos HACER 
        SI movimiento.tipo == "Gasto" ENTONCES 
            gastosTotales = gastosTotales  + movimiento.monto
        FIN SI
    FIN PARA
    RETONAR gastosTotales

FIN FUNCION
``` 
#### calcularBalance()
```text

FUNCION calcularBalance(ingresosTotales,gastosTotales)
    balanceTotal = 0
    balanceTotal = ingresosTotales - gastosTotales
   
    RETONAR balanceTotal

FIN FUNCION
```
#### determinarMayorGasto()
```text

FUNCION determinarMayorGasto(listaMovimientos)
    gastoCategoria = calcularGastoPorCategoria(listaMovimientos)
    mayorGasto = 0
    categoriaMayorGasto = ""
    PARA CADA categoria EN gastoCategoria HACER 
        SI gastoCategoria[categoria] > mayorGasto ENTONCES 
            mayorGasto = gastoCategoria[categoria]
            categoriaMayorGasto = categoria
        FIN SI
    FIN PARA
    RETONAR categoriaMayorGasto

FIN FUNCION
```

### Módulo de presentación
#### mostrarMovimientosCategoria()
```text

FUNCION mostrarMovimientosCategoria()
    gastoCategoria = calcularGastoPorCategoria(listaMovimientos)
    mayorGasto = 0
    categoriaMayorGasto = ""
    PARA CADA categoria EN gastoCategoria HACER 
        SI gastoCategoria[categoria] > mayorGasto ENTONCES 
            mayorGasto = gastoCategoria[categoria]
            categoriaMayorGasto = categoria
        FIN SI
    FIN PARA
    RETONAR categoriaMayorGasto

FIN FUNCION
```

generarReporte()
mostrarAdvertencia()