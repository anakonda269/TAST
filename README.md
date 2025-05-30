
class Machine
{
    public List<Drinks> DrinkList = new List<Drinks>();
    public string Name;
    private string SerialNumber;

    public Machine(string name)
    {
        Name = name;
        SerialNumber = "SN-1235467890";
    }
}

class Drinks
{
    public string Name { get; }
    public int Amount { get; set; }
    public double Price { get; }

    public Drinks(string name, int amount, double price)
    {
        Name = name;
        Amount = amount;
        Price = price;
    }

    public void Order()
    {
        if (Amount > 0)
        {
            Amount--;
            Console.WriteLine($"Zamówiono {Name} za {Price} zł. Pozostało {Amount} sztuk.\n");
        }
        else
        {
            Console.WriteLine($"Brak dostępnych {Name}.\n");
        }
    }
}

class TestClass
{
    public static void Run()
    {
        var machine = new Machine("NapojoInator6000");
        machine.DrinkList.Add(new Drinks("Kawa", 5, 6.5));
        machine.DrinkList.Add(new Drinks("Herbata", 3, 5.0));
        machine.DrinkList.Add(new Drinks("Czekolada", 2, 7.0));
        Console.WriteLine($"Witamy w {machine.Name}");

        while (true)
        {
            DisplayMenu(machine);
        }
    }

    static void DisplayMenu(Machine machine)
    {
        Console.WriteLine("Dostępne napoje:");

        for (int item = 0; item < machine.DrinkList.Count; item++)
        {
            var drink = machine.DrinkList[item];
            Console.WriteLine($"{item + 1}. {drink.Name} ({drink.Price} zł) (Dostępność: {drink.Amount})");
        }
        Console.Write("Wybierz numer napoju: ");

        string? wpis = Console.ReadLine();
        int wybor;
        if (int.TryParse(wpis, out wybor))
        {
            if (wybor > 0 && wybor <= machine.DrinkList.Count)
            {
                machine.DrinkList[wybor - 1].Order();
            }
            else
            {
                Console.WriteLine("Nieprawidłowy wybór.\n");
            }
        }
        else
        {
            Console.WriteLine("To nie jest liczba.\n");
        }
    }
}

class Napoj
{
    public string Nazwa { get; }
    public int Ilosc { get; private set; }
    public double Cena { get; }

    public Napoj(string nazwa, int ilosc, double cena)
    {
        Nazwa = nazwa;
        Ilosc = ilosc;
        Cena = cena;
    }

    public void Zamow()
    {
        if (Ilosc > 0)
        {
            Ilosc--;
            Console.WriteLine($"Zamówiono {Nazwa} za {Cena} zł. Pozostało {Ilosc} sztuk.\n");
        }
        else
        {
            Console.WriteLine($"Brak dostępnych {Nazwa}.\n");
        }
    }
}

class Automat
{
    public string Nazwa { get; }
    public List<Napoj> Napoje { get; } = new();

    public Automat(string nazwa)
    {
        Nazwa = nazwa;
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Możesz uruchomić TestClass.Run() lub poniższy kod
        var automat = new Automat("NapojoInator6000");
        automat.Napoje.Add(new Napoj("Kawa", 5, 6.5));
        automat.Napoje.Add(new Napoj("Herbata", 3, 5.0));
        automat.Napoje.Add(new Napoj("Czekolada", 2, 7.0));
        Console.WriteLine($"Witamy w {automat.Nazwa}");

        while (true)
        {
            WyswietlMenu(automat);
        }
        // Lub odkomentuj poniższą linię, aby uruchomić wersję z Machine/Drinks
        // TestClass.Run();
    }

    static void WyswietlMenu(Automat automat)
    {
        Console.WriteLine("Dostępne napoje:");
        for (int i = 0; i < automat.Napoje.Count; i++)
        {
            var napoj = automat.Napoje[i];
            Console.WriteLine($"{i + 1}. {napoj.Nazwa} ({napoj.Cena} zł) (Dostępność: {napoj.Ilosc})");
        }
        Console.Write("Wybierz numer napoju: ");
        string? wpis = Console.ReadLine();
        if (int.TryParse(wpis, out int wybor) && wybor > 0 && wybor <= automat.Napoje.Count)
        {
            automat.Napoje[wybor - 1].Zamow();
        }
        else
        {
            Console.WriteLine("Nieprawidłowy wybór lub wpis.\n");
        }
    }
}
