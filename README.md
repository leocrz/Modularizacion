# -Modularizacion
```csharp
class Program
{
    // Variables globales para la calculadora
    static double num1, num2, resultado;
    static bool operacionValida;

    static void Main()
    {
        while (true)
        {
            // Solicita al usuario que elija una opción
            Console.WriteLine("\nElija una opción:");
            Console.WriteLine("1. Calculadora básica");
            Console.WriteLine("2. Validación de contraseña");
            Console.WriteLine("3. Números primos");
            Console.WriteLine("4. Suma de números pares");
            Console.WriteLine("5. Conversión de temperatura");
            Console.WriteLine("6. Contador de vocales");
            Console.WriteLine("7. Cálculo de factorial");
            Console.WriteLine("8. Juego de Adivinanza");
            Console.WriteLine("9. Intercambio de números (paso por referencia)");
            Console.WriteLine("10. Tabla de multiplicar");
            Console.WriteLine("11. Salir");
            string opcion = Console.ReadLine();

            // Selecciona la opción a realizar según la elección del usuario
            switch (opcion)
            {
                case "1":
                    CalculadoraBasica();
                    break;
                case "2":
                    ValidacionContrasena();
                    break;
                case "3":
                    NumerosPrimos();
                    break;
                case "4":
                    SumaNumerosPares();
                    break;
                case "5":
                    ConversionTemperatura();
                    break;
                case "6":
                    ContadorVocales();
                    break;
                case "7":
                    CalculoFactorial();
                    break;
                case "8":
                    JuegoAdivinanza();
                    break;
                case "9":
                    IntercambioNumeros();
                    break;
                case "10":
                    TablaMultiplicar();
                    break;
                case "11":
                    Console.WriteLine("Saliendo del programa...");
                    return;
                default:
                    Console.WriteLine("Opción no válida. Inténtelo de nuevo.");
                    break;
            }
        }
    }

    static void CalculadoraBasica()
    {
        // Inicialización de variables globales
        operacionValida = true;

        // Solicita al usuario que ingrese el primer número
        Console.WriteLine("Ingrese el primer número:");
        num1 = LeerNumero();

        // Solicita al usuario que ingrese el segundo número
        Console.WriteLine("Ingrese el segundo número:");
        num2 = LeerNumero();

        // Solicita al usuario que elija una operación
        Console.WriteLine("Elija una operación:");
        Console.WriteLine("1. Suma");
        Console.WriteLine("2. Resta");
        Console.WriteLine("3. Multiplicación");
        Console.WriteLine("4. División");
        string operacion = Console.ReadLine();

        // Selecciona la operación a realizar según la elección del usuario
        switch (operacion)
        {
            case "1":
                Sumar();
                break;
            case "2":
                Restar();
                break;
            case "3":
                Multiplicar();
                break;
            case "4":
                if (num2 != 0)
                {
                    Dividir();
                }
                else
                {
                    Console.WriteLine("Error: No se puede dividir por cero.");
                    operacionValida = false;
                }
                break;
            default:
                Console.WriteLine("Operación no válida.");
                operacionValida = false;
                break;
        }

        // Si la operación es válida, muestra el resultado
        if (operacionValida)
        {
            Console.WriteLine($"El resultado de la operación es: {resultado}");
        }
    }

    static void ValidacionContrasena()
    {
        string password;

        // Ciclo do-while para pedir la contraseña hasta que sea correcta
        do
        {
            Console.WriteLine("Ingrese la contraseña:");
            password = Console.ReadLine();

            if (password != "1234")
            {
                Console.WriteLine("Contraseña incorrecta. Inténtelo de nuevo.");
            }
        } while (password != "1234");

        Console.WriteLine("Acceso concedido.");
    }

    static void NumerosPrimos()
    {
        Console.WriteLine("Ingrese un número:");
        int num = int.Parse(Console.ReadLine());
        bool esPrimo = true;

        if (num <= 1)
        {
            esPrimo = false;
        }
        else
        {
            for (int i = 2; i <= Math.Sqrt(num); i++)
            {
                if (num % i == 0)
                {
                    esPrimo = false;
                    break;
                }
            }
        }

        if (esPrimo)
        {
            Console.WriteLine($"{num} es un número primo.");
        }
        else
        {
            Console.WriteLine($"{num} no es un número primo.");
        }
    }

    static void SumaNumerosPares()
    {
        int suma = 0, num;

        Console.WriteLine("Ingrese números enteros (ingrese 0 para confimar su resultado):");

        while (true)
        {
            num = int.Parse(Console.ReadLine());

            if (num == 0)
                break;

            if (num % 2 == 0)
                suma += num; // Solo suma los números pares
        }

        Console.WriteLine($"La suma total de los números pares ingresados es: {suma}");
    }

    static void ConversionTemperatura()
    {
        Console.WriteLine("Ingrese la temperatura en grados Celsius:");
        double celsius = double.Parse(Console.ReadLine());
        double fahrenheit = (celsius * 9 / 5) + 32;
        Console.WriteLine($"{celsius} grados Celsius equivalen a {fahrenheit} grados Fahrenheit.");
    }

    static void ContadorVocales()
    {
        Console.WriteLine("Ingrese una cadena de texto:");
        string texto = Console.ReadLine();
        int contador = 0;

        foreach (char c in texto.ToLower())
        {
            if ("aeiou".Contains(c))
            {
                contador++;
            }
        }

        Console.WriteLine($"El texto ingresado contiene {contador} vocales.");
    }

    static void CalculoFactorial()
    {
        Console.WriteLine("Ingrese un número:");
        int num = int.Parse(Console.ReadLine());
        long factorial = 1;

        for (int i = 2; i <= num; i++)
        {
            factorial *= i;
        }

        Console.WriteLine($"El factorial de {num} es: {factorial}");
    }

    static void JuegoAdivinanza()
    {
        Random random = new Random();
        int numeroSecreto = random.Next(1, 101);
        int intento;
        int intentos = 0;

        Console.WriteLine("Adivina el número (entre 1 y 100):");

        do
        {
            intento = int.Parse(Console.ReadLine());
            intentos++;

            if (intento < numeroSecreto)
            {
                Console.WriteLine("Demasiado bajo. Inténtalo de nuevo.");
            }
            else if (intento > numeroSecreto)
            {
                Console.WriteLine("Demasiado alto. Inténtalo de nuevo.");
            }
        } while (intento != numeroSecreto);

        Console.WriteLine($"¡Felicidades! Adivinaste el número en {intentos} intentos.");
    }

    static void IntercambioNumeros()
    {
        // Solicita al usuario que ingrese dos números
        Console.WriteLine("Ingrese el primer número:");
        double num1 = LeerNumero();
        Console.WriteLine("Ingrese el segundo número:");
        double num2 = LeerNumero();

        // Muestra los valores originales
        Console.WriteLine($"Valores originales: num1 = {num1}, num2 = {num2}");

        // Llama a la función para intercambiar los valores
        Intercambiar(ref num1, ref num2);

        // Muestra los valores intercambiados
        Console.WriteLine($"Valores intercambiados: num1 = {num1}, num2 = {num2}");
    }

    // Función para intercambiar dos números por referencia
    static void Intercambiar(ref double a, ref double b)
    {
        double temp = a;
        a = b;
        b = temp;
    }

    static void TablaMultiplicar()
    {
        Console.WriteLine("Ingrese el número para la tabla de multiplicar:");
        int num = int.Parse(Console.ReadLine());

        for (int i = 1; i <= 10; i++)
        {
            Console.WriteLine($"{num} x {i} = {num * i}");
        }
    }

    // Método para leer un número asegurando que sea válido
    static double LeerNumero()
    {
        double num;
        while (!double.TryParse(Console.ReadLine(), out num))
        {
            Console.WriteLine("Por favor ingrese un número válido:");
        }
        return num;
    }

    // Método para sumar dos números
    static void Sumar()
    {
        resultado = num1 + num2;
    }

    // Método para restar dos números
    static void Restar()
    {
        resultado = num1 - num2;
    }

    // Método para multiplicar dos números
    static void Multiplicar()
    {
        resultado = num1 * num2;
    }

    // Método para dividir dos números
    static void Dividir()
    {
        resultado = num1 / num2;
    }
}
```
