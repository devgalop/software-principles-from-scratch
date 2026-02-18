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

    El principio de Abierto/Cerrado busca que el código desarrollado sea abierto a nuevas extensiones pero que se mantenga cerrado para modificaciones. Esto quiere decir, que es preferible extender nuevos comportamientos al código existente antes que modificarlo.

- **Consecuencias**:

    Aplicando este principio, el código obtiene:

  - El código adquiere **flexibilidad** y **extensibilidad** ya que al no tener que modificar el código existente, se pueden agregar nuevas funcionalidades de forma más fácil.
  - Permite agregar **modificaciones sin impactar** código existente ya que utiliza el polimorfismo y herencia.

- **Ejemplo de uso**:

    Dentro de un sistema de pagos, se tiene la posibilidad de pagar con varios métodos de pago, cada uno de ellos con una pasarela de pagos especifica.

  - **Clases mal diseñadas**: El desarrollador decide crear una clase **PaymentMethod** en la que para cada uno de los medios de pagos crea un método relacionado. Esta implementación implica que si en el futuro ingresa un nuevo medio de pago o si cambia alguno de los existentes, se modifique la clase entera.

  ```csharp
    // Clase para realizar pagos
    public class PaymentMethod
    {
        public async Task<bool> PayWithDebitCard()
        {
            //lógica de pago con tarjeta débito
            Console.WriteLine("Realiza pago con tarjeta débito");
            return true;
        }

        public async Task<bool> PayWithCreditCard()
        {
            //lógica de pago con tarjeta crédito
            Console.WriteLine("Realiza pago con tarjeta crédito");
            return true;
        }

        public async Task<bool> PayWithPSE()
        {
            //lógica de pago a través de plataforma PSE
            Console.WriteLine("Realiza pago con PSE");
            return true;
        }
    }
  ```

  - **Clases bien diseñadas**: Con la ayuda de un patrón de diseño **Factory Method** se aplica el principio **OCP** ya que en vez de tener una sola clase encargada de todos los tipos de pago, se tendrá una clase base con la cual interactua el usuario pero cada implementación especifica está de forma individual. Si en el futuro llegan nuevos métodos de pagos, bastaría con agregar una nueva implementación sin modificar el código existente.

  ```csharp
    //Interfaz de métodos de pago
    public interface IPaymentMethod
    {
        Task<bool> Pay();
    }

    //Implementación especifica de método de pago con tarjeta débito
    public sealed class DebitCardPayment : IPaymentMethod
    {
        public async Task<bool> Pay()
        {
            //lógica de pago con tarjeta débito
            Console.WriteLine("Realiza pago con tarjeta débito");
            return true;
        }
    }

    //Implementación especifica de método de pago con tarjeta crédito
    public sealed class CreditCardPayment : IPaymentMethod
    {
        public async Task<bool> Pay()
        {
            //lógica de pago con tarjeta crédito
            Console.WriteLine("Realiza pago con tarjeta crédito");
            return true;
        }
    }

    //Implementación especifica de método de pago PSE
    public sealed class PSEPayment : IPaymentMethod
    {
        public async Task<bool> Pay()
        {
            //lógica de pago a través de la plataforma PSE
            Console.WriteLine("Realiza pago a través de PSE");
            return true;
        }
    }

    //Fabrica de método de pago
    public abstract class PaymentFactory
    {
        public abstract IPaymentMethod Create();
    }

    //Implementación para crear métodos de pago con tarjeta débito
    public sealed class DebitCardPaymentFactory : PaymentFactory
    {
        public IPaymentMethod Create()
        {
            return new DebitCardPayment();
        }
    }

    //Implementación para crear métodos de pago con tarjeta crédito
    public sealed class CreditCardPaymentFactory : PaymentFactory
    {
        public IPaymentMethod Create()
        {
            return new CreditCardPayment();
        }
    }

    //Implementación para crear métodos de pago por PSE
    public sealed class PSEPaymentFactory : PaymentFactory
    {
        public IPaymentMethod Create()
        {
            return new PSEPayment();
        }
    }

  ```

[Volver al inicio](#tabla-de-contenido)

---

## Liskov Substitution Principle (LSP)

- **Definición**:

    El principio de Sustitución de Liskov, propuesto por Barbara Liskov, establece que las clases derivadas deben ser completamente intercambiables con sus clases base sin alterar el comportamiento esperado del programa. En otras palabras, si una clase *B* hereda de una clase *A*, cualquier instancia de *B* debe poder sustituir a una instancia de *A* sin que el sistema pierda su funcionalidad o genere errores. Este principio se basa en la idea de que las clases derivadas deben cumplir con el contrato definido por la clase base.

- **Consecuencias**:

    Al aplicar el principio de Sustitución de Liskov, el código obtiene los siguientes beneficios:

  - **Mayor flexibilidad y reutilización**: Las clases derivadas pueden ser utilizadas en lugar de sus clases base sin necesidad de realizar modificaciones adicionales, lo que facilita la extensión y el mantenimiento del sistema.
  - **Reducción de errores**: Al garantizar que las clases hijas puedan sustituir a las clases base sin alterar el comportamiento esperado, se minimizan los errores en tiempo de ejecución.
  - **Facilidad para realizar pruebas**: Al cumplir con este principio, se pueden realizar pruebas unitarias de las clases derivadas de manera independiente, ya que se garantiza que respetan el contrato definido por la clase base.
  - **Mejor comprensión del código**: El diseño del sistema se vuelve más claro y predecible, ya que las clases derivadas mantienen el comportamiento esperado de las clases base.
  - **Promueve el uso de polimorfismo**: Facilita la implementación de soluciones polimórficas, permitiendo que el código sea más genérico y adaptable a cambios futuros.

- **Ejemplo de uso**:

    Dentro de un sistema de generacion de reportes, se tiene la posibilidad de cargar el reporte en diferentes tipos de destinos como por ejemplo: SFTP, FTP, Via Email entre otros...

  - **Clases mal diseñadas**: El desarrollador para cumplir con el requerimiento asignado, crea una clase principal *Notifier* sobre la cual crea los diferentes metodos encargados de cada tipo de envío.

    ```csharp
    //Clase encargada de enviar las notificaciones del reporte
    public class Notifier
    {
        public void NotifySFTP(string reportPath)
        {
            //lógica para cargar a SFTP
            Console.WriteLine("Notificación generada para SFTP");
        }

        public void NotifyFTP(string reportPath)
        {
            //lógica para cargar a FTP
            Console.WriteLine("Notificación generada para FTP");
        }

        public void NotifyEmail(string reportPath)
        {
            //lógica para cargar a email
            Console.WriteLine("Notificación generada para Email");
        }
    }
    ```

  - **Clases bien diseñadas**: Aplicando el principio **LSP** podemos refactorizar esta solución de la siguiente manera: La clase *Notifier* establece el contrato que las demás implementaciones usarán. Se debe crear para cada tipo de notificación una implementación diferente.

    ```csharp
        public interface Notifier
        {
            void Notify(string reportPath);
        }

        public sealed class SFTPNotifier : Notifier
        {
            public void Notify(string reportPath)
            {
                //lógica para cargar a SFTP
                Console.WriteLine("Notificación generada para SFTP");
            }
        }

        public sealed class FTPNotifier : Notifier
        {
            public void Notify(string reportPath)
            {
                //lógica para cargar a FTP
                Console.WriteLine("Notificación generada para FTP");
            }
        }

        public sealed class EmailNotifier : Notifier
        {
            public void Notify(string reportPath)
            {
                //lógica para cargar a Email
                Console.WriteLine("Notificación generada para Email");
            }
        }
    ```

[Volver al inicio](#tabla-de-contenido)

---

## Interface Segregation (ISP)

- **Definición**:

    El principio de Segregación de Interfaces establece que las interfaces deben ser específicas y enfocadas en una única responsabilidad, de manera que los clientes (clases que implementan las interfaces) no se vean obligados a depender de métodos que no utilizan. Esto implica dividir interfaces grandes y genéricas en varias interfaces más pequeñas y especializadas, cada una diseñada para satisfacer las necesidades específicas de los clientes que las implementan. Este principio está estrechamente relacionado con el principio de responsabilidad única (SRP), ya que ambos buscan reducir la complejidad y mejorar la mantenibilidad del código.

- **Consecuencias**:

    Al aplicar este principio en el código, conseguimos lo siguiente:
  - **Mayor flexibilidad y mantenibilidad**: Las interfaces pequeñas y específicas facilitan la implementación y el mantenimiento del código, ya que los cambios en una funcionalidad no afectan a otras partes del sistema.
  - **Reducción de dependencias innecesarias**: Los clientes solo implementan los métodos que realmente necesitan, evitando la sobrecarga de código innecesario.
  - **Mejor comprensión del código**: Las interfaces más pequeñas y específicas son más fáciles de entender y utilizar, lo que mejora la claridad del diseño.
  - **Facilita la reutilización del código**: Las interfaces especializadas pueden ser reutilizadas en diferentes contextos sin necesidad de modificar su implementación.
  - **Promueve un diseño modular**: Al dividir las interfaces en partes más pequeñas, se fomenta un diseño más modular y desacoplado.

- **Ejemplo de uso**:

    Dentro de una aplicación de logistica encargada del envío de paquetería, se tiene la posibilidad de realizar las siguientes tareas:
  - Los clientes tienen la posibilidad de realizar un seguimiento al paquete
  - La operación debe crear guia para un paquete al momento de recibirlo
  - Cada proceso logistico debe registrar estado del paquete

  - **Clases mal diseñadas**: Se creó una interfaz llamada *IPackingManager* que contiene todos los métodos permitidos dentro de la gestión de paquetes. Esto obliga a cualquier cliente a tener que implementar todos los métodos aunque no los necesite.

    ```csharp
    //Estado del paquete
    public sealed record TrackState(
        string TrackNumber, 
        string State, 
        DateTime Date
    );

    public interface IPackingManager
    {
        string GenerateTrackNumber();
        List<TrackState> GetStates(string trackNumber);
        void RegisterState(TrackState state);
    }
    ```

  - **Clases bien diseñadas**: Al aplicar el principio **ISP** se logra separar cada responsabilidad dentro de una sola interfaz, permitiendo que cada usuario elija las responsabilidades que necesite.

    ```csharp
    //Estado del paquete
    public sealed record TrackState(
        string TrackNumber, 
        string State, 
        DateTime Date
    );

    // Interfaz encargada de la generacion de guias
    public interface ITrackIdProvider
    {
        string GenerateTrackNumber();
    }

    // Interfaz encargada de consulta de estados
    public interface ITrackingStatesProvider
    {
        List<TrackState> GetStates(string trackNumber);
    }

    // Interfaz encargada de agregar estados
    public interface ITrackStateRegister
    {
        void RegisterState(TrackState state);
    }
    ```

[Volver al inicio](#tabla-de-contenido)

---

## Dependency Inversion Principle (DIP)

- **Definición**:

    l principio de Inversión de Dependencias establece que los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de abstracciones (interfaces). Además, las abstracciones no deben depender de los detalles, sino que los detalles deben depender de las abstracciones. Esto permite que las clases sean más flexibles, reutilizables y fáciles de mantener.

- **Consecuencias**:

    Al aplicar este principio, el código obtiene:
  - **Mayor flexibilidad**: Las clases pueden ser reutilizadas en diferentes contextos.
  - **Mejor mantenibilidad**: El código es más fácil de mantener y modificar.
  - **Reducción de dependencias**: Las clases no dependen de clases concretas, sino de interfaces abstractas.

- **Ejemplo de uso**:

    En una aplicación encargada de la gestión de usuarios, se tiene un proveedor que genera el token de acceso para nuestros dispositivos.

  - **Clases mal diseñadas**: En este diseño, la clase User está directamente acoplada a la implementación concreta de GoogleAuthenticatorTokenProvider. Esto significa que si en el futuro se necesita cambiar el proveedor de tokens o agregar uno nuevo, será necesario modificar la clase User, lo que va en contra del principio de abierto/cerrado (OCP). Además, este acoplamiento dificulta las pruebas unitarias, ya que no es posible sustituir fácilmente el proveedor de tokens por un mock o stub.

    ```csharp
    public class User(string Name, string Id)
    {
        public string GetToken()
        {
            GoogleAuthenticatorTokenProvider tokenProvider = neW();
            return tokenProvider.GenerateToken();
        }
    }

    public class GoogleAuthenticatorTokenProvider
    {
        public string GenerateToken()
        {
            //lógica de generación de token
            Console.WriteLine("Generando token con proveedor Google Authenticator");
            return "TOKEN_GENERADO";
        }
    }
    ```

  - **Clases bien diseñadas**: En este ejemplo, se utiliza la técnica de Inyección de Dependencias (Dependency Injection) para pasar la implementación concreta de ITokenProvider al constructor de la clase TokenProvider. Esto permite cambiar fácilmente el proveedor de tokens sin modificar la clase TokenProvider, lo que hace que el sistema sea más flexible y fácil de mantener

    ```csharp
    //La clase usuario pertenece al dominio y no debe ser alterada por la infraestructura
    public class User(string Name, string Id)
    {}

    //Esta clase es encargada de proveer al cliente de tokens generados sin importar el proveedor
    public class TokenService(ITokenProvider provider)
    {
        public string GetToken()
        {
            return provider.GenerateToken();
        }
    }

    //Contrato para proveer tokens
    public interface ITokenProvider
    {
        string GenerateToken();
    }

    //Proveedor especializado en generación de tokens
    public class GoogleAuthenticatorTokenProvider : ITokenProvider
    {
        public string GenerateToken()
        {
            //lógica de generación de token
            Console.WriteLine("Generando token con proveedor Google Authenticator");
            return "TOKEN_GENERADO";
        }
    }
    ```

[Volver al inicio](#tabla-de-contenido)
