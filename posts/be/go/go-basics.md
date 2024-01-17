---
title: "Go Basics"
subtitle: "Go Syntax"
date: "2024-01-17"
category: "go"
author: "gork"
---

// Basic Types: int, float64, string, bool
// Composite Types: array, slice, map, struct
// Pointer Types: *&

## Go Variable Types

**var**
**const**

var age int
var height float64
var firstName string
var isEmployed bool

age = 29
height = 177.88
firstName = "gork"
isEmployed = true

değişken değerini zaten biliyorsak, aşağıdaki şekilde de tanımlayabiliriz.

age := 29
height := 177.88
firstName := "gork"
isEmployed := true

```bash
fmt.Println(age, height, firstName, isEmployed)
```

// Format
```bash
fmt.Printf("Age: %d", age)
fmt.Printf("Height: %f", height)
fmt.Printf("FirstName: %s", firstName)
fmt.Printf("Employed?: %t", isEmployed)
```

## Go Array

var colors [3]string
colors[0] = "red"
...
players := [3]string{"ab","cd","qw"}
players[2] = "qw to kg"

## Go Slice

var todos []string
- eğer dizi uzunluğunu bilmiyorsak slice kullanabiliriz.

```bash
todos = append(todos, "uyan", "uyu")
```
**[][]**
```bash
courses := [3][2]string{
  {"Go", "NodeJs"},
  {"AWS", "GCP"}
}
```


## Go Map

wishList := make(map[string]string)
wishList["first"] = "MacPro"
wishList["second"] = "900 Billion Dolar"
wishList["third"] = "a beautiful car"

key:value

delete(wishList, "third") // third key i silinir.

firstWishList := wishList["first"]

benzersiz değer atamak istersek kullanılabilir. productName productDetail price...


## Go Struct

```bash
  type Product struct{
    Name string
    Price float64
  }

  var product Product or product := Product {Name: "M..."}
  product = Product{
    Name: "MacPro",
    Price: 9000,
  }

```

client tarafına `json:""` ile istediğimiz değeri gönderebiliriz.
```bash
  type Product struct{
    Name string `json:"name"`
    Price float64 `json:"productPrice"`
  }
```


## Go Functions

```bash
  func sayHello(){
    fmt.Println("hello.")
  }

  func getUserName() string {
    return "Neo"
  }

  func getUserById (id int) (string, int){
    println(id)
    return "Neo", 32
  }

  name, age := getUserById(4)
  fmt.Printf("Name: %v, age: %v", name, age)
  --
  func getUserById (id, ageInput int) (name string, age int){
    println(id, ageInput)
    return "Neo", 32
  }

  parametre uzunluğunu bilmiyorsak
  func calculateTotal(products...float64) float64 {
      totalAmount := 0.0

      for index, price := range products {
        totalAmount += price
      }

      **eğer index i kullanmayacaksak bize kızacak. onun yerine for _, price...**

      return totalAmount
  }

  **Receiver Functions**

  type Product struct {
    Name string
    Price float64
    Stock int
  }

  Alıcı-FonksiyonAdı-GeriyeNeDönecek
  func (p Product) Calculate(qty int) float64 {
    return p.Price * float64(qty)
  }
  --
  p := Product{
    Name: "MacPro",
    Price: 9000,
    Stock:1
  }
  p.Calculate(2)

  func (p *Product) ReduceStock(qty int) {
    if p.Stock >= qty {
      p.Stock -= qty
    }
  }

  p.ReduceStock(1)

```



