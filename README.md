# SOLID-PRINCIPLES
Activity 33: SOLID PRINCIPLES DOCUMENTATION

What does the SOLID principles actually means? Well, it’s just an acronym of the five principles listed as below.

S - Single Responsibility Principle (known as SRP)

O - Open/Closed Principle

L - Liskov’s Substitution Principle

I - Interface Segregation Principle

D - Dependency Inversion Principle

Let’s try to understand what all these principles means, one by one with examples.

S — Single Responsibility Principle (known as SRP)

The name itself suggest that the “class should be having one and only one responsibility”. What does it mean? Well let’s take the class A which does the following operations.

Open a database connection

Fetch data from database

Write the data in an external file

The issue with this class is that it handles lot of operations. Suppose any of the following change happens in future.

New database

Adopt ORM to manage queries on database

Change in the output structure

So in all the cases the above class would be changed. Which might affect the implementation of the other two operations as well. So ideally according to SRP there should be three classes each having the single responsibility.

O — Open/Closed Principle

This principle suggests that “classes should be open for extension but closed for modification”. What is means is that if the class A is written by the developer AA, and if the developer BB wants some modification on that then developer BB should be easily do that by extending class A, but not by modifying class A.

The easy example would be the RecyclerView.Adapter class. Developers can easily extend this class and create their own custom adapter with custom behaviour without modifying the existing RecyclerView.Adapter class.

L — Liskov’s Substitution Principle

This principle suggests that “parent classes should be easily substituted with their child classes without blowing up the application”. Let’s take following example to understand this.

Let’s consider an Animal parent class.

public class Animal {
    public void makeNoise() {
        System.out.println("I am making noise");
    }
}

Now let’s consider the Cat and Dog classes which extends Animal.

public class Dog extends Animal {
    @Override
    public void makeNoise() {
        System.out.println("bow wow");
    }
}

public class Cat extends Animal {
    @Override
    public void makeNoise() {
        System.out.println("meow meow");
    }
}

Now, wherever in our code we were using Animal class object we must be able to replace it with the Dog or Cat without exploding our code. What do we mean here is the child class should not implement code such that if it is replaced by the parent class then the application will stop running. For ex. if the following class is replace by Animal then our app will crash.

class DumbDog extends Animal {
    @Override
    public void makeNoise() {
        throw new RuntimeException("I can't make noise");
    }
}

If we take Android example then we should write the custom RecyclerView adapter class in such a way that it still works with RecyclerView. We should not write something which will lead the RecyclerView to misbehave.

I — Interface Segregation Principle

This principle suggests that “many client specific interfaces are better than one general interface”. This is the first principle which is applied on interface, all the above three principles applies on classes. Let’s take following example to understand this principle.

In android we have multiple click listeners like OnClickListener as well as OnLongClickListener.

/**
 * Interface definition for a callback to be invoked when a view is clicked.
 */
public interface OnClickListener {
    /**
     * Called when a view has been clicked.
     *
     * @param v The view that was clicked.
     */
    void onClick(View v);
}/**
 * Interface definition for a callback to be invoked when a view has been clicked and held.
 */
public interface OnLongClickListener {
    /**
     * Called when a view has been clicked and held.
     *
     * @param v The view that was clicked and held.
     *
     * @return true if the callback consumed the long click, false otherwise.
     */
    boolean onLongClick(View v);
}

Why do we need two interfaces just for same action with one single tap and another with long press. Why can’t we have following interface.

public interface MyOnClickListener {
    void onClick(View v);
    boolean onLongClick(View v);
}

If we have this interface then it will force clients to implement onLongClick even if they don’t even care about long press. Which will lead to overhead of unused methods. So having two separate interfaces helps in removing the unused methods. If any client want both behaviours then they can implement both interfaces.

D — Dependency Inversion Principle

This principle suggest that “classes should depend on abstraction but not on concretion”. What does it mean that we should be having object of interface which helps us to communicate with the concrete classes. What do we gain from this is, we hide the actual implementation of class A from the class B. So if class A changes the class B doesn’t need to care or know about the changes.

In android if we are following MVP pattern then we need to keep reference of Presenter in our View. Now if we keep the Presenter concrete class object in View then it leads to tight coupling. So what we do is we create a interface which abstracts the implementation of presenter and our view class keeps the reference of the PresenterInterface.


Link to my GitHub Repository (Documentation)

https://github.com/MonetForProgrammingPurposes/SOLID-PRINCIPLES


References

https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design

https://www.freecodecamp.org/news/solid-principles-explained-in-plain-english/

https://www.baeldung.com/solid-principles
