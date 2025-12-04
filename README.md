[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=21941049&assignment_repo_type=AssignmentRepo)
# Proyecto final - Electrónica Digital 1 - 2025-II

# Integrantes
- Olmer Stiven Ortiz Hernandez
- Daniela Patricia Esquivel Díaz
- Juan Jose Cifuentes Rojas

# Nombre del proyecto
Proyecto Deméter: monitoreo de invernaderos

# Documentación
## Introducción 
Actualmente el control de la temperatura en cultivos e invernaderos representa un desafío constante para los agricultores. Además, la radiación solar, las variaciones climáticas externas y la falta de ventilación adecuada son factores que desestabilizan los rangos óptimos de temperatura de los cultivos. Estas condiciones afectan directamente el crecimiento de las plantas, reducen el rendimiento y, en muchos casos, generan pérdidas económicas por cosechas de baja calidad.

## Descripción de la arquitectura

El proyecto se compone de varios módulos electrónicos que trabajan en conjunto para monitorear el ambiente y controlar la ventilación:

1. FPGA Cyclone IV

Actúa como el núcleo de control.
En ella se implementan las máquinas de estados encargadas de procesar los datos del sensor y gestionar el encendido de los ventiladores, así como el envío de información hacia la pantalla LCD.

2. Sensor DHT11

Dispositivo encargado de medir temperatura y humedad.
Entrega los valores digitales directamente a la FPGA para su procesamiento.

3. Relé de 3.3 V

Recibe una señal lógica proveniente de la FPGA.
Su función es conmutar una alimentación de 12 V para activar el conjunto de ventiladores cuando la temperatura supera el umbral definido.

4. Ventiladores de 12 V

Cuatro unidades conectadas al relé.
Operan simultáneamente y proporcionan flujo de aire para enfriar cuando el sistema lo determina.

5. Pantalla LCD 16x2

Interfaz de visualización.
Muestra en tiempo real la temperatura, humedad y el estado de los ventiladores según lo que envía la FPGA.

6. Fuente de 12 V

Alimenta a los ventiladores y puede incluir una regulación adicional para suministrar voltajes menores a otros módulos si es necesario.

### Lógica de control del sistema

El comportamiento del sistema de ventilación está determinado por las mediciones de temperatura obtenidas del sensor DHT11. La FPGA evalúa continuamente estos valores y aplica las siguientes reglas:

1. Activación de ventilación

Condición: Temperatura mayor a 20 °C

Acción:

- La FPGA activa la señal de control del relé.

- El relé conmuta la fuente de 12 V.

- Los cuatro ventiladores se encienden de manera simultánea.

2. Desactivación de ventilación

Condición: Temperatura menor a 15 °C

Acción:

- La FPGA desactiva la señal del relé.

- El relé abre el circuito de alimentación.

- Los ventiladores se apagan.


## Diagramas de la arquitectura


## Simulaciones


## Evidencias de implementación

