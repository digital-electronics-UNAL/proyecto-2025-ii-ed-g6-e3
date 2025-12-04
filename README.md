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
El siguiente diagrama muestra la interconexión entre los módulos principales del sistema de monitoreo ambiental y control de ventilación implementado en la FPGA. Cada bloque representa un componente funcional independiente y las señales que intercambian permiten realizar la lectura del sensor, el control del ventilador y la visualización en la pantalla LCD.


![Diagrama ](conexionsistema.png)

1. Módulo DHT11 Sensor (dht11_sensor.dht11_inst)

Este bloque se encarga de gestionar la comunicación con el sensor DHT11.
Sus principales funciones son:

- Leer la señal digital del sensor (dht11_io).

- Extraer y entregar los valores de temperatura `( temp1 , temp2 )` y humedad `(hum1, hum2)`.

- Proveer señales internas de depuración `(state_debug)`.

- Trabaja sincronizado con el reloj global `(clk)` y se reinicia mediante `rst_n`.

La información generada por este módulo se distribuye hacia los módulos de control del ventilador y de la LCD.

2. Módulo de Control de Ventilador (fsm_fan_control: fan_ctrl)

Este bloque implementa la máquina de estados encargada de activar o desactivar el ventilador según la temperatura medida.
Recibe:

- El valor de temperatura desde el módulo DHT11.

- La señal de reloj y reset.

Como salida genera:

- fan_enable, señal que controla el relé encargado de energizar los ventiladores.

Su funcionamiento sigue la lógica:

- Activa el ventilador si la temperatura es mayor a cierto umbral.

- Lo apaga si la temperatura desciende por debajo del límite inferior.

3. Módulo Controlador de LCD (LCD1602_controller: lcd_ctrl)

Este módulo recibe los valores numéricos de temperatura y humedad provenientes del sensor y se encarga de formatearlos y enviarlos a la pantalla LCD 16x2.

Entradas importantes:

Datos de temperatura y humedad (parte entera y fraccionaria).

Señales de reloj `(clk)`, reset `(reset)` y sincronización `(ready_i)`.

Salidas hacia la LCD:

lcd_data[7:0]: bus de datos hacia la pantalla.

lcd_e, lcd_rs, lcd_rw: señales de control para la correcta escritura en el display.

El módulo asegura que la información se actualice de manera ordenada y comprensible.

4. Señales globales y sistema general

clk: señal de reloj compartida por todos los módulos, garantizando sincronización.

rst_n / reset: permite reiniciar el sistema completo.

ready_i: señal que habilita la actualización de la LCD.

state[2:0]: señal que refleja el estado actual del sistema, útil para depuración.

Resumen general

El sistema completo integra tres módulos principales:

- Lectura del sensor DHT11 → obtiene temperatura y humedad.

- Control del ventilador → decide cuándo activar el relé mediante fan_enable.

- Controlador de LCD → muestra los valores ambientales en pantalla.


## Simulaciones


## Evidencias de implementación

