## Ekspres do kawy
Systemy czasu rzeczywistego, semestr letni 2025.
### Autor
* Mróz Michał 
* email: mmroz@student.agh.edu.pl

## Opis ogólny:
Model przedstawia opis ekspresu do kawy. Urządzenie pozwala na wybieranie napoju, oraz przeglądanie aktualnego stanu urządzenia (między innym ilości dostępnej kawy czy wody i mleka, jak również ich temperatury). 
Urządzenie powinno posiadać układ przetwarzający wybraną przez użytkownika operację, a następnie przedstawić proces działania wymagany do jego realizacji.
Urządzenie powinno składać się z interfejsu umożliwiającego użytkownikowi sterowanie nim, pamięci trwałej, procesora, oraz odpowiednich czujników i kontrolerów używanych do tworzenia napojów.

## Opis dla użytkownika:
Cała interakcja użytkownika z systemem prowadzona będzie przez udostępniony interfejs dający dostęp do różnych funkcjonalności. Zaliczają się do nich:
* Wybór napoju spośród listy przechowywanej w pamięci urządzenia.
* Kontrola zasobów (na przykład sprawdzenie dostępnej ilości kawy) i stanu technicznego (stan filtra wody) przez wyświetlenie wartości odczytanych z odpowiednich czujników.
* Zapisywanie do pamięci preferencji użytkownika.

## Spis komponentów
### Typy danych

|Nazwa|Opis|
|-|-|
|`MilkOrder`| Typ zawierający informacje na temat mleka. Przechowuje dane typu Float `milk_amount` i typu Integer `froth_level` |
|`HeaterOrder`|Typ zawierający informacje o grzałce. Zawiera w sobie dane typu Float: `water_amount`, `heater_temp`, `brewing_time`|
|`CoffeOrder`|Typ zawierający informacje na temat przygotowywanego napoju. Przechowuje pola takie jak `CoffeAmount` typu float, pole `add_milk` typu Boolean oraz pola typu `HeaterOrder` i `MilkOrder`.|

### Urządzenia
|Nazwa|Opis|
|-|-|
|`Grinder`|Odpowiada urządzeniu młynka. Przyjmuje dane typu Float odpowiadające ilości kawy i zwraca informację typu Boolean o zakończeniu działania.|
|`Heater`|Odpowiada urządzniu grzałki. Przyjmuje dane typu `HeaterOrder` i zwraca informację typu Boolean o zakończeniu działania.|
|`Frother`|Spieniacz do mleka przyjmujący informację typu `MilkOrder` i zwracający informację typu Boolean o zakończeniu działania.|
|`Controller`|Odpowiada interfejsowi użytkownika.|
|`ItemSensor`|Czujnik sprawdzający stan danego elementu. Pomiar wykonywany jest na żądanie. Implementacyjnie rozdzielony jest na `ItemSensor.WaterSensor`, `ItemSensor.CoffeSensor`, `ItemSensor.MilkSensor`.|

### Wątki

|Nazwa|Opis|
|-|-|
|`ReadItemSensors`|Wątek odpowiada za odczytanie obecnych stanów zasobów przy wykorzystaniu urządzeń `ItemSensor`.
|`HandleInput`|Wątek odpowiadający za zbieranie danych wejściowych z urządzenia `Controller`.|
|`MakeCoffee`|Wątek odpowiadający za proces przygotowywania napoju.|

### Procesy
|Nazwa|Opis|
|-|-|
|`CoffeMachineController`|Proces kontrolujący działanie urządzenia.|

### Urządzenia dodatkowe
System wyposażony jest w procesor `Processor` kontrolujący działanie systemu, magistralę danych `Bus`. Oprócz tego dołączona jest pamięć `Ram` przechowująca stan urządzenia, oraz pamięć `Memory` przechowującą domyślne ustawienia.
