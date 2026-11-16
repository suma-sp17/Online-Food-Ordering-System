# QuickBite -- Builder Design Pattern

## 1. Project Overview

**QuickBite** is an Online Food Ordering System used to demonstrate the
**Builder Design Pattern** in Python.

The system creates different types of food orders through a step-by-step
construction process. It supports:

-   Delivery orders
-   Takeaway orders
-   Dine-in orders

The main purpose of this project is to show how the Builder Design
Pattern separates the process of constructing an order from the final
`FoodOrder` object.

## 2. Design Pattern Used

**Builder Design Pattern (Creational Design Pattern)**

The Builder Design Pattern separates the construction of a complex
object from its representation. It allows the same construction process
to create different representations.

In QuickBite, the final product is a `FoodOrder`. Different concrete
builders configure that product for delivery, takeaway, or dine-in.

## 3. Why the Builder Pattern Is Used

An online food-ordering system can create different kinds of orders, and
each order type may require different information.

For example:

-   A delivery order requires a delivery address.
-   A takeaway order requires collection details.
-   A dine-in order requires a table number.

The Builder Pattern helps organize these steps into separate classes.
This makes the construction process easier to understand, maintain, and
extend.

## 4. Classes and Their Responsibilities

The implementation contains six main classes.

### 4.1 OrderBuilder -- Builder Interface

`OrderBuilder` is an abstract base class that defines the steps required
to construct an order.

Methods:

-   `addItems()` -- Adds selected food items to the order.
-   `setCustomer()` -- Sets the customer's details.
-   `setAddress()` -- Sets delivery, collection, or table details.
-   `setPayment()` -- Sets the selected payment method.
-   `calculateTotal()` -- Calculates the total order amount.
-   `getResult()` -- Returns the completed `FoodOrder` object.

The concrete builders implement these methods.

### 4.2 OrderDirector -- Director

`OrderDirector` controls the sequence of construction steps.

Methods:

-   `__init__(builder)` -- Receives a concrete builder.
-   `changeBuilder(builder)` -- Changes the builder used by the
    director.
-   `makeOrder()` -- Calls the builder methods in sequence and returns
    the completed order.

The Director does not need to know the internal details of each concrete
builder.

### 4.3 DeliveryOrderBuilder -- Concrete Builder

Creates a delivery order.

It:

-   Adds the selected food items.
-   Sets customer details.
-   Stores the delivery address.
-   Sets the payment method.
-   Calculates the total amount.
-   Returns the completed order.

### 4.4 TakeawayOrderBuilder -- Concrete Builder

Creates a takeaway order.

It performs the common order-building steps and sets the order details
to indicate that the customer will collect the order from the
restaurant.

### 4.5 DineInOrderBuilder -- Concrete Builder

Creates a dine-in order.

It performs the common order-building steps and stores the customer's
table number as the order's location detail.

### 4.6 FoodOrder -- Product

`FoodOrder` is the final product created by the concrete builders.

It stores:

-   `customer` -- Customer name or details.
-   `items` -- Selected food items and their prices.
-   `payment` -- Selected payment method.
-   `totalAmount` -- Calculated order total.
-   `orderType` -- Delivery, Takeaway, or Dine-In.
-   `address` -- Delivery address, collection information, or table
    details.

Method:

-   `displayOrder()` -- Displays the completed order details.

## 5. UML Class Diagram -- Relationships

Use the following relationships in the StarUML class diagram.

  ------------------------------------------------------------------------------
  From                     To                UML relationship  Meaning
  ------------------------ ----------------- ----------------- -----------------
  `DeliveryOrderBuilder`   `OrderBuilder`    Realization       Delivery builder
                                                               implements the
                                                               builder
                                                               interface.

  `TakeawayOrderBuilder`   `OrderBuilder`    Realization       Takeaway builder
                                                               implements the
                                                               builder
                                                               interface.

  `DineInOrderBuilder`     `OrderBuilder`    Realization       Dine-in builder
                                                               implements the
                                                               builder
                                                               interface.

  `OrderDirector`          `OrderBuilder`    Directed          Director holds
                                             association       and uses a
                                                               builder.

  Each concrete builder    `FoodOrder`       Association       Each builder
                                                               creates and
                                                               maintains a
                                                               food-order
                                                               object.

  `OrderBuilder`           `FoodOrder`       Dependency, if    The `getResult()`
                                             shown             return type
                                                               refers to
                                                               `FoodOrder`.
  ------------------------------------------------------------------------------

**UML notation:**

-   Realization: dashed line with a hollow triangle pointing to
    `OrderBuilder`.
-   Directed association: solid line with an open arrowhead pointing to
    the class being used.
-   Dependency: dashed line with an open arrowhead pointing to the
    depended-on class.
-   Association: solid line between the related classes.

## 6. How the System Works

The order construction process follows these steps:

1.  The customer selects an order type.
2.  The application creates the corresponding concrete builder.
3.  The builder is passed to `OrderDirector`.
4.  `OrderDirector.makeOrder()` starts the construction process.
5.  The Director calls `addItems()`.
6.  The Director calls `setCustomer()`.
7.  The Director calls `setAddress()`.
8.  The Director calls `setPayment()`.
9.  The Director calls `calculateTotal()`.
10. The Director calls `getResult()` and receives the completed
    `FoodOrder`.
11. The completed order can be displayed using `displayOrder()`.

## 7. Order Types

  Order type   Concrete builder         Order-specific information
  ------------ ------------------------ ----------------------------
  Delivery     `DeliveryOrderBuilder`   Delivery address
  Takeaway     `TakeawayOrderBuilder`   Collection from restaurant
  Dine-In      `DineInOrderBuilder`     Table number

## 8. Example

Suppose a customer selects:

-   Customer: Alex
-   Food items: Pizza -- ₹250, Burger -- ₹120
-   Order type: Delivery
-   Address: Bengaluru
-   Payment: UPI

The application creates a `DeliveryOrderBuilder` and passes it to
`OrderDirector`.

The Director runs the construction steps. The builder creates a
`FoodOrder` containing the customer details, selected items, delivery
address, payment method, and total amount.

**Total amount: ₹370**

This example demonstrates how the same overall construction process can
produce different types of food orders.

## 9. Technologies Used

-   **Python** -- Implements the Builder Design Pattern.
-   **`abc` module** -- Defines the abstract `OrderBuilder` interface.
-   **StarUML** -- Creates the UML class diagram.

If the project is connected to a web interface, Flask, HTML, and CSS can
be used for the web application. They are not part of the Builder
Pattern itself.

## 10. How to Run the Python Demonstration

1.  Install Python 3.
2.  Save the Python implementation in a file such as `main.py`.
3.  Open a terminal in the project folder.
4.  Run:

``` bash
python main.py
```

The program asks for the customer and order details, constructs the
selected order using the appropriate builder, and displays the completed
order.

## 11. Advantages of the Builder Pattern in QuickBite

-   Separates order construction from the final order object.
-   Supports multiple order types.
-   Keeps the Director independent of concrete builder details.
-   Makes it easier to add another order type with a new concrete
    builder.
-   Organizes the construction steps into clear methods.
-   Improves code readability and maintainability.

## 12. Conclusion

The QuickBite project demonstrates the Builder Design Pattern through an
Online Food Ordering System. The `OrderBuilder` interface defines the
construction steps, the concrete builders create different order types,
the `OrderDirector` controls the sequence, and `FoodOrder` represents
the completed order.

This implementation shows how a creational design pattern can be applied
to a practical software application.

------------------------------------------------------------------------

**Project:** QuickBite -- Online Food Ordering System\
**Design Pattern:** Builder Design Pattern\
**Implementation Language:** Python
