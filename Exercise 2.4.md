
## Exercise 2.4

Design for public transit system using principles of OOP.
<br>

Class diagram for the program would look as follows:

## Card
\- balance: double
<br>
\- expireTime: long

---
+loadMoney(double amount): void
<br>
+getBalance(): double
<br>
+buyTicket(TicketType type): boolean
<br>
+isValid(): boolean
<br>
+getExpireTime(): long
<br>

---
<br>

Explanation:
<br>

Member variables
<br>

- balance: Current balance on card
- expireTime: Expiration time of current valid ticket
<br>

Methods:
<br>

- loadMoney: Add money to card
- getBalance: Return current balance on card
- buyTicket: Makes attempt to buy ticket; Return **true** if successful, **false** if not
- isValid: Checks if current ticket is still valid
- getExpireTime: Return expiration time of current ticket
<br>
<br>

## TicketType  

\+ SINGLE: TicketType
<br>
\+ DAY: TicketType
<br>
\+ MONTH: TicketType

---

\- price: double
<br>
\- duration: long

---
+getPrice(): double
<br>
+getDuration(): long
<br>

---
<br>

Explanation:
<br>

Member variables
<br>

- price: Price of ticket
- duration: Ticket validity duration in milliseconds
<br>

Methods:
<br>

- getPrice(): Return price of ticket
- getDuration(): Return duration of ticket validity
<br>

Enumerations for TicketType:
<br>

- SINGLE: One ticket
- DAY: Day ticket
- MONTH: Monthly ticket
<br>
<br>

## PaymentTerminal
<br>

---
+inquireBalance(Card card): double
<br>
+loadCard(Card card, double amount): void
<br>
+purchaseTicket(Card card, TicketType type): boolean
<br>

---
<br>

Explanation:
<br>

Methods:
<br>

- inquireBalance: Return current balance on card.
- loadCard: Load given amount of money on card
- purchaseTicket: Attempt to purchase ticket of given type; return **true** if successful, **false** if not.
<br>

## Program examples
Class **Card:**
```Java
/**
 * Represents public transportation payment card.
 * @classInvariant balance >= 0
 * @classInvariant expiryTime >= 0
 */
public class Card {
    private double balance;
    private long expiryTime;

    /**
     * Load money onto card.
     * @param amount The amount of money to load.
     * @pre amount > 0
     * @post balance == balance@pre + amount
     */
    public void loadMoney(double amount) {
        assert amount > 0 : "Amount to load must be greater than zero";
        this.balance += amount;
    }

    /**
     * Return current balance on card.
     * @return The current balance.
     * @post result >= 0
     */
    public double getBalance() {
        return this.balance;
    }

    // Other methods ...
}
```
Class **TicketType:**
```Java
/**
 * Represents type of tickets available for purchase.
 */
public class TicketType {
    public static final TicketType SINGLE = new TicketType(3.0, 2 * 60 * 60 * 1000);
    public static final TicketType DAY = new TicketType(8.0, 24 * 60 * 60 * 1000);
    public static final TicketType MONTH = new TicketType(55.0, 30 * 24 * 60 * 60 * 1000);

    private final double price;
    private final long duration;

    /**
     * Constructs a TicketType with the specified price and duration.
     * @param price The price of the ticket.
     * @param duration The duration of the ticket validity in milliseconds.
     * @pre price > 0
     * @pre duration > 0
     */
    private TicketType(double price, long duration) {
        assert price > 0 : "Ticket price must be greater than zero";
        assert duration > 0 : "Ticket duration must be greater than zero";
        this.price = price;
        this.duration = duration;
    }

    // Other methods ...
}
```
Class **PaymentTerminal:**
```Java
/**
 * Represents device that interacts with the card for loading money, check balance, and purchase tickets.
 */
public class PaymentTerminal {
    /**
     * Returns current balance on card.
     * @param card The card to inquire balance from.
     * @pre card != null
     * @return The current balance.
     */
    public double inquireBalance(Card card) {
        assert card != null : "Card must not be null";
        return card.getBalance();
    }

    /**
     * Loads spesified amount of money onto card.
     * @param card The card to load money onto.
     * @param amount The amount of money to load.
     * @pre card != null
     * @pre amount > 0
     */
    public void loadCard(Card card, double amount) {
        assert card != null : "Card must not be null";
        assert amount > 0 : "Amount to load must be greater than zero";
        card.loadMoney(amount);
    }

    /**
     * Try to purhase ticket of given type using card.
     * @param card Card for purchasing the ticket.
     * @param type Type of ticket to purchase.
     * @pre card != null
     * @pre type != null
     * @return True if ticket was successfully purchased, false if not
     */
    public boolean purchaseTicket(Card card, TicketType type) {
        assert card != null : "Card can not be null";
        assert type != null : "Ticket type can not be null";
        return card.buyTicket(type);
    }
}
```
___