# Dependency Inversion Principle

**"Classes should not depend on each other directly, dependencies should be established through abstractions."**

Let's see this with a very practical example:

- Imagine you run a coffee shop ☕. If you are receiving money from customers, you should make the payment process as easy and convenient as possible, and expand the payment options to create an effortless service experience. So you add more payment options (Cash, Stripe, Paypal, Crypto, Uranium, Dark Matter, ...) to collect money regardless of how is it collected.

- Imagine you are a barista making coffee. You need ground coffee to make brew coffee, regardless of how it is ground, via electric grinder, or hand grinder it doesn't matter as long as you can make coffee.

The Bad code:

```Python
class PaymentMethod:
    def payment_cash(self, amount):
        #some logic
    
    def payment_card(self, infra, amount):
        # paypal process...
        # stripe process...
        # transfer process...

payment_method = PaymentMethod()

PaymentMethod.payment_cash(3)
PaymentMethod.payment_card(paypal, 3)
```

We violate both Dependency Inversion and Open/Closed Principles in this version. We are directly calling `payment_card` method and we have to modify it in order to add a new option. Let's fix this.

The Good code:

```Python
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):
    @abstractmethod
    def process_payment(self, amount):
        pass


class PaymentStripe(PaymentProcessor):
    def process_payment(self, amount):
        # some logic
        print(f"{amount} amount of payment received with Stripe.")


class PaymentUranium(PaymentProcessor):
    def process_payment(self, amount):
        # some logic
        print(f"☢️ {amount} grams of radioactive payment received. Handle with caution.")


class CoffeeShop:
    def __init__(self, payment_method: PaymentProcessor):
        self.payment_method = payment_method

    def make_sale(self, order, amount):
        print("Order is being prepared...")
        self.payment_method.process_payment(amount)
        print("Order has been completed ☕")

uranium_wallet = PaymentUranium()
my_shop = CoffeeShop(uranium_wallet)

my_shop.make_sale(Affogato, 4)
```

With this way, we are independant from any payment method's specific processes. We built a modular, easy to grasp system.

![alt text](images/dip.png) 