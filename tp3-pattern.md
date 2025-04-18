# tp3 design patterns

## 1. La pizzeria O’Reilly

### 1.1 Ce qui varie dans le code

Ce qui change :
- Le *type de pizza* : "fromage", "grecque", "poivrons", etc.
- La *logique d’instanciation* dans commanderPizza() : ajout/suppression d’un type de pizza → modification du code source !

> 🧠 Principe de conception : identifier ce qui varie, et l’isoler !

---

### 1.2 Extraire dans une classe SimpleFabriqueDePizzas

java
public class SimpleFabriqueDePizzas {
    public Pizza creerPizza(String type) {
        if (type.equals("fromage")) {
            return new PizzaFromage();
        } else if (type.equals("grecque")) {
            return new PizzaGrecque();
        } else {
            return new PizzaPoivrons();
        }
    }
}

### 1.3 nouveau format du Pizzeria

java
public class Pizzeria {
    SimpleFabriqueDePizzas fabrique;

    public Pizzeria(SimpleFabriqueDePizzas fabrique) {
        this.fabrique = fabrique;
    }

    public Pizza commanderPizza(String type) {
        Pizza pizza = fabrique.creerPizza(type);
        pizza.preparer();
        pizza.cuire();
        pizza.couper();
        pizza.emballer();
        return pizza;
    }
}


Pizzeria --> SimpleFabriqueDePizzas --> Pizza
                     ↘
[PizzaFromage, PizzaGrecque, PizzaPoivrons]

### 1.4 avantage
- On respecte le principe ouvert/fermé : on peut ajouter de nouveaux types de pizza sans modifier Pizzeria.

- Oui, on transfère le problème… mais dans une classe dédiée, centrant les responsabilités.