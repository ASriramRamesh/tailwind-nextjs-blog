---
title: Java Records
date: '2024-11-3'
tags: [PDF, reader, project, iOS, localization, RTL, CJK]
type: Blog
license: CC BY-SA 4.0
---

# Understanding Java Records

Java 17 introduced records, a special kind of class designed to simplify the creation of immutable data carriers. Records reduce boilerplate code and provide a more concise way to define classes that primarily serve as data holders.

## What are Records?

Records are intended for situations where a class is created solely to hold data. They automatically generate several key methods, including:
- Constructor: A constructor that initializes the fields
- Accessors: Getter methods for each field
- `equals()` and `hashCode()`: Implementations that compare records based on their field values
- `toString()`: A method that returns a string representation of the record's fields

## Basic Record Example

```java
record Book(String author, String title, double price) {
}

public class TestBook {
    public static void main(String[] args) {
        Book book = new Book("Morgan Housel ", "The Psychology of Money", 313);
        System.out.println("Details of the book : " + book);
        System.out.println(book.author());
        System.out.println(book.title());
        System.out.println(book.price());
        System.out.println("Hash code of Book" + book.hashCode());
    }
}
```

### Output:
```
Details of the bookBook[author=Morgan Housel , title=The Psychology of Money, price=313.0]
Morgan Housel
The Psychology of Money
313.0
Hash code of Book:1015016633
```

## Key Features of Records

- All fields in records are final, they cannot be modified
- Since values are immutable, there are no setter methods
- Records are final, they cannot be subclassed
- Records cannot extend from other classes as all records are implicitly inheriting from `java.lang.Record` and Java does not support multiple inheritance
- You can add instance methods to a record

## Adding Custom Methods to Records

```java
record Book(String author, String title, double price) {
    // Instance method to format book details in a specific way
    public String formattedDetails() {
        return String.format("'%s' by %s (Price: Rs.%.2f)", title, author, price);
    }
}

public class TestBook {
    public static void main(String[] args) {
        Book book = new Book("Morgan Housel", "The Psychology of Money", 313);
        
        // Using the formattedDetails() method
        System.out.println("Formatted Book Details: " + book.formattedDetails());
    }
}
```

### Output:
```
Formatted Book Details: 'The Psychology of Money' by Morgan Housel (Price: Rs.313.00)
```

## Benefits Over Traditional DTOs

Records significantly reduce boilerplate code associated with DTOs. Traditional DTOs require explicit constructors, getter methods, and implementations for `equals()`, `hashCode()`, and `toString()`. In contrast, records automatically generate these methods, making them more concise and easier to read. A record can replace a typical DTO class with just a single line of code.
