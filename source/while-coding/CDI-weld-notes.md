# CDI weld notes

- With very few exceptions, almost every concrete Java class that has a constructor with no
parameters (or a constructor designated with the annotation @Inject) is a bean.

A managed bean is a Java class. You can explicitly declare a managed bean by annotating the
bean class @ManagedBean, but in CDI you don’t need to. According to the specification, the CDI
container treats any class that satisfies the following conditions as a managed bean:

- It is not a non-static inner class.
- It is a concrete class, or is annotated @Decorator.
- It is not annotated with an EJB component-defining annotation or declared as an EJB bean class
in ejb-jar.xml.
- It does not implement javax.enterprise.inject.spi.Extension.
- It has an appropriate constructor—either:
 - the class has a constructor with no parameters, or
 - the class declares a constructor annotated @Inject.

Bean types for a managed bean contains the bean class, every superclass
and all interfaces it implements directly or indirectly.

If a managed bean has a public field, it must have the default scope @Dependent

- @Inject may be applied to a constructor or method of a bean, and tells the container to call that constructor
or method when instantiating the bean. The container will inject other beans into the parameters of
the constructor or method.

- Notice the controller bean is request-scoped and named (`@Named @RequestScoped`). Since this combination is
so common in web applications, there’s a built-in annotation for it in CDI that we
could have used as a shorthand. When the (stereotype) annotation `@Model` is
declared on a class, it creates a request-scoped and named bean.
Alternatively, we may obtain an instance of TextTranslator programmatically from an injected
instance of Instance, parameterized with the bean type:
`@Inject Instance<TextTranslator> textTranslatorInstance;`

- it isn’t necessary to create a getter or setter method to inject one bean into another. CDI
can access an injected field directly (even if it’s private!), which sometimes helps eliminate some
wasteful code. The name of the field is arbitrary. It’s the field’s type that determines what is
injected.

- At system initialization time, the container must validate that exactly one bean exists which
satisfies each injection point. In our example, if no implementation of Translator is available—if the
SentenceTranslator EJB was not deployed—the container would inform us of an *unsatisfied
dependency*. If more than one implementation of Translator were available, the container would
inform us of the *ambiguous dependency*.

#### creating an user defined `@Qualifier` annotation:

Define:

```
@Qualifier
@Target({TYPE, METHOD, PARAMETER, FIELD})
@Retention(RUNTIME)
public @interface CreditCard {}

```

Qualify bean:

```
@CreditCard
public class CreditCardPaymentProcessor
  implements PaymentProcessor { ... }

```

Use it during injection:

```
@Inject @CreditCard PaymentProcessor paymentProcessor

```

#### Scopes

Each scope is represented by an annotation type.
 
Keep in mind that once a bean is bound to a context, it remains in that context
until the context is destroyed. There is no way to manually remove a bean from a
context. If you don’t want the bean to sit in the session indefinitely, consider
using another scope with a shorted lifespan, such as the request or conversation
scope.

If a scope is not explicitly specified, then the bean belongs to a special scope called the dependent
pseudo-scope. Beans with this scope live to serve the object into which they were injected, which
means their lifecycle is bound to the lifecycle of that object.


#### EL name

If you want to reference a bean in non-Java code that supports Unified EL expressions, for example,
in a JSP or JSF page, you must assign the bean an EL name.
The EL name is specified using the `@Named` annotation

```
public @SessionScoped @Named("cart")
class ShoppingCart implements Serializable { ... }
```

Now we can easily use the bean in any JSF or JSP page:

```
<h:dataTable value="#{cart.lineItems}" var="item">
  ...
</h:dataTable>

```
We can let CDI choose a name for us by leaving off the value of the @Named annotation. The name defaults to the unqualified class name, decapitalized; in this case, `shoppingCart`.

#### Denoting implementation alternatives:

sometimes we have an interface (or other bean type) whose
implementation varies depending upon the deployment environment. For example, we may want
to use a mock implementation in a testing environment. An alternative may be declared by
annotating the bean class with the `@Alternative` annotation.

```
public @Alternative
class MockPaymentProcessor extends PaymentProcessorImpl { ... }
```

We can choose between alternatives at
deployment time by selecting an alternative in the CDI deployment descriptor META-INF/beans.xml of
the jar or Java EE module that uses it. Different modules can specify that they use different
alternatives.

#### producer methods:

Not everything that needs to be injected can be boiled down to a bean class instantiated by the
container using new. There are plenty of cases where we need additional control. What if we need to
decide at runtime which implementation of a type to instantiate and inject? What if we need to
inject an object that is obtained by querying a service or transactional resource, for example by
executing a JPA query?

A producer method is a method that acts as a source of bean instances. The method declaration
itself describes the bean and the container invokes the method to obtain an instance of the bean
when no instance exists in the specified context. A producer method lets the application take full
control of the bean instantiation process.

A producer method is declared by annotating a method of a bean class with the @Produces
annotation.

```
import javax.enterprise.inject.Produces;
@ApplicationScoped
public class RandomNumberGenerator {
  private java.util.Random random = new java.util.Random(System.currentTimeMillis());
  @Produces @Named @Random int getRandomNumber() {
     return random.nextInt(100);
 }
}

```

We can’t write a bean class that is itself a random number. But we can certainly write a method
that returns a random number. By making the method a producer method, we allow the return
value of the method—in this case an `Integer`—to be injected. We can even specify a qualifier—in
this case @Random, a scope—which in this case defaults to @Dependent, and an EL name—which in this
case defaults to randomNumber according to the JavaBeans property name convention. Now we can
get a random number anywhere:

```
@Inject @Random int randomNumber;
```
Notice the name of the member above. It is not the name of the bean class, but it is EL name of the `@Produces` variable.

#### Producer fields

A producer field is a simpler alternative to a producer method. A producer field is declared by
annotating a field of a bean class with the @Produces annotation—the same annotation used for
producer methods.

```
import javax.enterprise.inject.Produces;
public class Shop {
  @Produces PaymentProcessor paymentProcessor = ....;
  @Produces @Catalog List<Product> products = ....;
}
```
### Injection points

Injection can occur via three different mechanisms.

- Bean constructor parameter injection
  ```
  public class Checkout {
   private final ShoppingCart cart;
   @Inject
   public Checkout(ShoppingCart cart) {
     this.cart = cart;
   }
  }
 
  ```
- Initializer method parameter injection

 ```
 public class Checkout {
  private ShoppingCart cart;
  @Inject
  void setShoppingCart(ShoppingCart cart) {
    this.cart = cart;
  }
 }
 ```
 
- direct field injection

 ```
 public class Checkout {
  private @Inject ShoppingCart cart;
 }
 
 ```
  Getter and setter methods are not required for field injection to work


## Good resources:
- https://docs.jboss.org/cdi/learn/userguide/CDI-user-guide.pdf
- https://www.youtube.com/watch?v=lyuU24ZFlY4
