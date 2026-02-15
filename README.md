# Principios de diseño de Software

## Tabla de contenido

1. [Definicion](#definicion)

    1.1 [Modularidad](#modularidad)

    1.2 [Encapsulamiento](#encapsulamiento)

    1.3 [Abstracción](#abstracción)

    1.4 [Separación de conceptos](#separación-de-conceptos)

2. [SOLID](#solid)
3. [DRY](#dry)
4. [KISS](#kiss)
5. [YAGNI](#yagni)
6. [CoC](#coc)
7. [Composition over Inheritance](#composition-over-inheritance)
8. [LoD](#lod)
9. [Lecturas recomendadas](#lecturas-recomendadas)

---

## Definicion

Los **principios de diseño de software** son guías fundamentales que facilitan el proceso de creación de sistemas de software bien diseñado y mantenibles.

Para incrementar y facilitar la *legivilidad del código*, la *escalabilidad* y la *reutilización del código*, estos principios sostienen conceptos como: *modularidad*, *encapsulamiento*, *abstracción* y *separación de conceptos*.

El gran objetivo de estos son: crear equipos que trabajen de manera eficiente, reducir el número de errores y crear un software robusto pero adaptable y extensible al mismo tiempo.

### Modularidad

Es la práctica dividir un sistema complejo en partes más pequeñas, llamados modulos o componentes. Cada uno de estos modulos es responsable de una tarea y se comunica con otros modulos a través de interfaces definidas.

La modularidad promueve la reutilización de código, facilita la mantenibilidad y el desarrollo de pruebas unitarias.

### Encapsulamiento

Esta es la práctica de agrupar atributos y métodos de que modifican estos atributosdatos en una clase, asegurando que el estado interno de un objeto es solo accesible a través de métodos bien definidos.

El encapsulamiento promueve la integridad de los datos y previene modificaciones no planeadas.

### Abstracción

Se encarga de esconder la complejidad de los detalles de la implementación de un módulo, exponiendo solo la información necesaria para los usuarios. Simplifica las interacciones entre modulos y permite realizar cambios sin afectar el resto del sistema.

### Separación de conceptos

Se trata de dividir el sistema en diferentes secciones, cada una de estas es responsable de un concepto principal. Esto permite que las modificaciones afecten solo a los conceptos relacionados y no al sistema entero.

[Volver al inicio](#tabla-de-contenido)

---

## SOLID

**SOLID** es un acrónimo que define cinco principios del diseño orientado a objetos. Su objetivo principal es evitar en el desarrollo de software *Code Smells*. Además permiten agilidad y adaptabilidad del software. [Seguir aprendiendo](./SOLID/solid_principles.md)

[Volver al inicio](#tabla-de-contenido)

---

## DRY

[Volver al inicio](#tabla-de-contenido)

---

## KISS

[Volver al inicio](#tabla-de-contenido)

---

## YAGNI

[Volver al inicio](#tabla-de-contenido)

---

## CoC

[Volver al inicio](#tabla-de-contenido)

---

## Composition over Inheritance

[Volver al inicio](#tabla-de-contenido)

---

## LoD

[Volver al inicio](#tabla-de-contenido)

---

## Lecturas Recomendadas

- [Software Design Principles](https://www.scaler.com/topics/software-design-principles/)
- [Principles of Software Development: SOLID, DRY, KISS, and more](https://scalastic.io/en/solid-dry-kiss/)
- [SOLID Design Principles Explained: Building Better Software Architecture](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)
- [Principles of Software Design](https://www.geeksforgeeks.org/system-design/principles-of-software-design/)

[Volver al inicio](#tabla-de-contenido)
