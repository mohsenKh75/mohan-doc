- encapsulation: means making the data access safer with not allowing user to access it directly. user only can access to the data via methods that use that data:
```
type BankAccount struct {
    balance int // private data
}

func (a *BankAccount) Deposit(amount int) {
    if amount > 0 {
        a.balance += amount
    }
}

func (a *BankAccount) Balance() int {
    return a.balance
}
//we only have access to balance with the related methods of Bankaccount
```
- Abstraction: means make usage easy with not engaging the user with the logic and just simply use the logic:
```
type Car struct{}

func (c Car) Start() {
    fmt.Println("Car started")
}

//other file:
car := Car{}
car.Start()

//we just call the Start method without needing to know how it works
```

- inheritence: it is what makes classes reusable. we use other classes in one class to inherit their attribiutes. we have a product class, we use this class inside our CartItem class. the CartItem will contain Product attrs with new things of it self. 

- polymorphism: different types could use a same interface and each one use the interface with its own characteristic/attr:
```
type Animal interface {
    Speak()
}

type Dog struct{}

func (d Dog) Speak() {
    fmt.Println("Woof!")
}

type Cat struct{}

func (c Cat) Speak() {
    fmt.Println("Meow!")
}

// in other file:
animals := []Animal{Dog{}, Cat{}}

for _, animal := range animals {
    animal.Speak()
}

//both Cat and Dog are using same interface but each one use it in its own way.
```