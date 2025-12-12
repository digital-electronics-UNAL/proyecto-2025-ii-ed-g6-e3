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

