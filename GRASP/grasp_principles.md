# Principios de Asignación de responsabilidades generales (GRASP)

[Leer principal](../README.md)

## Tabla de contenido

1. [Definición](#definición)

---

## Definición

los principios de asignacion de responsabilidades generales (GRASP) o en inglés **General Responsability Assignment Software Patterns** son un conjunto de guías que permiten diseñar un sistema con un bajo acoplamiento, una alta cohesión, flexible y extensible. **GRASP** permite asignar responsabilidades a las clases y objetos.

Los principios que contiene son:

- **Creator**: Su responsabilidad es la creación de objetos.
- **Information Expert**: Posee la responsabilidad de conocer toda la información necesaria para llenar una clase.
- **Low Coupling**: Reduce las interconexiones y dependencias entre clases.
- **High Cohesion**: Clases enfocadas en un solo proposito.
- **Controller**: Captura eventos y coordina actividades.
- **Pure Fabrication**: Provee clases nuevas como helpers o conectores.
- **Indirection**: Usa intermediarios o abstracciones para desacoplar.
- **Polymorphisim**: Permite a objetos diferentes ser tratados por igual a través de una interfaz.
