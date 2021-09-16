# CDI weld notes

- With very few exceptions, almost every concrete Java class that has a constructor with no
parameters (or a constructor designated with the annotation @Inject) is a bean.

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


## Good resources:
- https://docs.jboss.org/cdi/learn/userguide/CDI-user-guide.pdf
- https://www.youtube.com/watch?v=lyuU24ZFlY4
