
## Exercise 2.2

The principle of data protection involved with serving the two different roles described (customer and staff) is **encapsulation**. In a broader sense, the underlying principle is Role-Based Access Control (RBAC).

1. Library Customer View:

A customer should be able to search and read information on books without any ability to alter the book data. Therefore it would be sensible to implement a read-only version of **book** class with getters but no setters:

```Java
// @.classInvariant title != null && publicationYear > 0 && publisher != null
public class ImmutableBook {
    private final String title;
    private final int publicationYear;
    private final String publisher;

    // @.pre book != null
    // @.post this.title == book.getTitle() ...
    public ImmutableBook(Book book) {
        this.title = book.getTitle();
        this.publicationYear = book.getPublicationYear();
        this.publisher = book.getPublisher();
    }

    // Getter methods only
    // @.pre true
    // @.post RESULT == this.title
    public String getTitle() {
        return title;
    }

    // Other getters here...
}
```
- ImmutableBook class only has getters and no setters. Fields are made **final** to make sure they are immutable.
- Class invariant: After created, the state of **ImmutableBook** object can't be changed.
- For usage, customers queries return **ImmutableBook** instead of **Book**.
<br>
<br>
<br>
2. Library Staff View:

The **book** class for staff is mutable. Staff can permanently edit the information of a spesific book.

The code is similar to above, but with following differences:

- Both getter and setter methods; modification of state is possible.
- Fields are not **final**.
- Class invariant: Book needs to maintain own invariants, staff edits must meet certain conditions; fields cannot be null, etc.
- For usage, when staff want to edit a book, they interact directly with **book** class.

Example:

```Java
public class Book {
    // @.classInvariant title != null && publicationYear > 0 && publisher != null
    private String title;
    private int publicationYear;
    private String publisher;
    
    
    // @.pre title != null && publicationYear > 0 && publisher != null
    // @.post this.title == title ...
    public Book(String title, int publicationYear, String publisher) {
        this.title = title;
        this.publicationYear = publicationYear;
        this.publisher = publisher;
    }

    // @.pre true
    // @.post RESULT == this.title
    public String getTitle() {
        return title;
    }

    // @.pre title != null
    // @.post this.title == title
    public void setTitle(String title) {
        this.title = title;
    }

    // Other getters and setters here...
}
```
---