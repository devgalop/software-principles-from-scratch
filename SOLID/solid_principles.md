# Principios SOLID

[Leer principal](../README.md)

## Tabla de contenido

1. [Definición](#definición)
2. [Single Responsability](#single-responsability-principle-srp)
3. [Open/Closed](#openclosed-principle-ocp)
4. [Liskov Substitution](#liskov-substitution-principle-lsp)
5. [Interface Segregation](#interface-segregation-isp)
6. [Dependency Inversion](#dependency-inversion-principle-dip)

---

## Definición

Los principio de diseño orientado a objetos **SOLID** son conceptos claves dentro del desarrollo de software bajo el paradigma orientado a objetos. Estos cinco conceptos promueven un desarrollo ágil, robusto y escalable.

El acrónimo SOLID deriva de los siguientes principios:

- [Single Responsability Principle (SRP)](#single-responsability-principle-srp)
- [Open/Closed Principle (OCP)](#openclosed-principle-ocp)
- [Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
- [Interface Segregation Principle (ISP)](#interface-segregation-isp)
- [Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)

Estos principios fueron expuestos por [Robert C. Martin](https://es.wikipedia.org/wiki/Robert_C._Martin)

[Volver al inicio](#tabla-de-contenido)

---

## Single Responsability Principle (SRP)

- **Definición**:

    El principio de responsabilidad única establece que una clase debe tener una única responsabilidad bien definida, lo que significa que debe haber una única razón para que la clase cambie. En otras palabras, cada clase debe estar enfocada en cumplir un único propósito o tarea específica dentro del sistema.

- **Consecuencias**:

    Al aplicar este principio, se obtienen:
  - un **código más modular** y fácil de entender, ya que cada clase tiene un propósito claro y definido.
  - Facilita la **mantenibilidad del código**, ya que los cambios en una funcionalidad específica solo afectan a la clase responsable de esa tarea, reduciendo el riesgo de introducir errores en otras partes del sistema.
  - Permite un **manejo de errores más eficiente**, ya que las responsabilidades están aisladas y los problemas pueden identificarse y solucionarse más fácilmente.
  - Fomenta la **reutilización del código**, ya que las clases con responsabilidades únicas pueden ser utilizadas en diferentes contextos sin depender de otras funcionalidades no relacionadas.
  - Promueve el **desarrollo colaborativo**, ya que diferentes desarrolladores pueden trabajar en distintas partes del sistema sin interferir entre sí.

- **Ejemplo de uso**:

    Dentro de una aplicación existe un requerimiento para implementar un módulo de recuperación de contraseña cuando un usuario no recuerde su clave de ingreso. El requerimiento especifica que el usuario ingresa a través de un front su correo electronico registrado y si este existe en la base de datos, se genera un token el cual es notificado a través de un correo.

  - **Clase mal diseñada**: El primer escenario del código vemos que el desarrollador construyó una clase **RecoveryPassword** la cual tiene varias responsabilidades: *Validar Usuario*, *Generar Token*, *Notificar Usuario*

  ```csharp
    //Captura petición enviada por el usuario desde el front
    public sealed record RecoveryPasswordRequest(string Email);

    //Clase para requerimiento de recuperación de contraseña
    public class RecoveryPassword
    {

        public async Task<bool> IsUserRegistered(string email)
        {
            bool isRegistered = false;
            //Lógica para validar usuario en la base de datos
            Console.WriteLine($"Validando en base de datos la existencia de '[{email}]'");
            return isRegistered;
        }

        public string GenerateToken()
        {
            //lógica para generar el token
            Console.WriteLine("Generando Token de usuario");
            return "TOKEN_GENERATED";
        }

        public async Task<bool> SendNotification(string email, string body)
        {
            //lógica para el envío de la notificación por correo
            Console.WriteLine($"Enviando correo a la direccion '[{email}]'");
            return true;
        }
    }
    ```

  - **Clases bien diseñadas**: Si se aplica el principio **SRP** la clase **RecoveryPassword** podría dividirse en tres clases independientes: **UserValidatorService** encargada de la validación del usuario, **TokenProvider** encargada de generar tokens, **NoficationService** encargada de envio de notificaciones

  ```csharp
    //Captura petición enviada por el usuario desde el front
    public sealed record RecoveryPasswordRequest(string Email);

    //Clase encargada de la validacion del usuario en base de datos
    public sealed class UserValidatorService
    {
        public async Task<bool> IsUserRegistered(string email)
        {
            bool isRegistered = false;
            //Lógica para validar usuario en la base de datos
            Console.WriteLine($"Validando en base de datos la existencia de '[{email}]'");
            return isRegistered;
        }
    }

    //Clase encargada de la generacion de tokens
    public sealed class TokenProvider
    {
        public string GenerateToken()
        {
            //lógica para generar el token
            Console.WriteLine("Generando Token de usuario");
            return "TOKEN_GENERATED";
        }
    }

    //Clase encargada de enviar notificaciones por correo electronico
    public sealed class NotificationService
    {
        public async Task<bool> SendAsync(string email, string body)
        {
            //lógica para el envío de la notificación por correo
            Console.WriteLine($"Enviando correo a la direccion '[{email}]'");
            return true;
        }
    }
  ```

[Volver al inicio](#tabla-de-contenido)

---

## Open/Closed Principle (OCP)

- **Definición**:
- **Consecuencias**:
- **Ejemplo de uso**:

[Volver al inicio](#tabla-de-contenido)

---

## Liskov Substitution Principle (LSP)

- **Definición**:
- **Consecuencias**:
- **Ejemplo de uso**:

[Volver al inicio](#tabla-de-contenido)

---

## Interface Segregation (ISP)

- **Definición**:
- **Consecuencias**:
- **Ejemplo de uso**:

[Volver al inicio](#tabla-de-contenido)

---

## Dependency Inversion Principle (DIP)

- **Definición**:
- **Consecuencias**:
- **Ejemplo de uso**:

[Volver al inicio](#tabla-de-contenido)
