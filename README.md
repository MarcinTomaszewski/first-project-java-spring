# **Controller - Spring **

## **Opis projektu**
Ten projekt demonstruje podstawowe działanie kontrolera w Spring Framework. `HelloController` obsługuje dwa różne żądania HTTP GET.

---

## **Jak działa kod**

Kod obsługuje dwie ścieżki:
1. `/` – zwraca statyczny tekst jako odpowiedź.
2. `/greeting` – przyjmuje parametr wejściowy `name`, przekazuje go do widoku poprzez obiekt Model i generuje dynamiczną odpowiedź.

---

## **Opis adnotacji @nazwa oraz obiekt Model**

- **`@Controller`**: Adnotacja wskazuje, że klasa jest kontrolerem Spring MVC. Klasa zostaje zarejestrowana jako komponent Spring i jest odpowiedzialna za obsługę żądań HTTP.
- **`@ResponseBody`**: Instruuje Spring, aby zwrócił treść odpowiedzi HTTP bez użycia widoków. Spring domyślnie traktuje zwracane wartości z metod kontrolera jako nazwy szablonów (widoków) w systemie szablonów Thymeleaf.
- **`Model`**: Obiekt umożliwiający przekazywanie danych z kontrolera do widoku.
- **`@GetMapping`**: Adnotacja określająca, że metoda obsługuje żądania HTTP GET dla podanego adresu URL.
- **`@RequestParam`**: Adnotacja używana do pobierania parametrów z zapytania HTTP.

---

```java
@Controller
public class HelloController {}
```
- **`@Controller`**: Oznacza, że ta klasa obsługuje żądania HTTP jako kontroler w aplikacji webowej.
- **`public class HelloController`**: Definiuje publiczną klasę o nazwie `HelloController`.

---

### **Metoda 1: hello()**

```java
@GetMapping(value = "/")
@ResponseBody
public String hello() {
    return "Hello Vistula, in my first Spring controller.";
}
```
1. **`@GetMapping(value = "/")`**:
    - Ta metoda obsługuje żądania HTTP GET pod adresem `/` (główna strona aplikacji).
2. **`@ResponseBody`**:
    - Zapewnia, że odpowiedź HTTP będzie zawierała tekst bez użycia systemu widoków.
3. **`public String hello()`**:
    - Definiuje metodę `hello` zwracającą obiekt typu `String`.
4. **`return "Hello Vistula, in my first Spring controller.";`**:
    - Zwraca statyczny tekst jako odpowiedź HTTP. W tym przypadku nie ma widoku.

---

### **Metoda 2: greeting()**

```java
@GetMapping(value = "/greeting")
public String greeting(@RequestParam(name="name", required = false, defaultValue = "World") String name, Model model) {
    model.addAttribute("name", name);
    return "greeting";
}
```
1. **`@GetMapping(value = "/greeting")`**:
    - Metoda obsługuje żądania HTTP GET pod adresem `/greeting`.
2. **`@RequestParam(name="name", required = false, defaultValue = "World")`**:
    - Pobiera parametr `name` z żądania HTTP.
    - `name`: nazwa parametru w URL.
    - `required = false`: Parametr jest opcjonalny.
    - `defaultValue = "World"`: Jeśli parametr `name` nie zostanie podany, użyta zostanie wartość domyślna "World".
3. **`Model model`**:
    - Obiekt `Model` służy do przekazywania danych z kontrolera do widoku.
4. **`model.addAttribute("name", name);`**:
    - Dodaje atrybut `name` (jego wartość) do modelu, dzięki czemu będzie on dostępny w widoku.
5. **`return "greeting";`**:
    - Zwraca nazwę widoku **`greeting`** (np. `greeting.html`). Widok zostanie wyrenderowany z użyciem danych przekazanych w `Model`.

---

## **Przykładowe użycie**

### **Endpoint 1: `/`**
- **Żądanie**:
  ```bash
  curl http://localhost:8080/
  ```
- **Odpowiedź**:
  ```plaintext
  Hello Vistula, in my first Spring controller.
  ```

---

### **Endpoint 2: `/greeting`**
#### Bez parametru `name`:
- **Żądanie**:
  ```bash
  curl http://localhost:8080/greeting
  ```
- **Odpowiedź (widok greeting.html)**:
  ```html
  Hello, World!
  ```

#### Z parametrem `name`:
- **Żądanie**:
  ```bash
  curl http://localhost:8080/greeting?name=John
  ```
- **Odpowiedź (widok greeting.html)**:
  ```html
  Hello, John!
  ```

---

## **Podsumowanie**
- **Endpoint `/`**:
    - Prosta odpowiedź tekstowa w formie stringa.
- **Endpoint `/greeting`**:
    - Obsługuje dynamiczne dane wejściowe (parametr `name`).
    - Integruje się z widokami za pomocą `Model`.

---
