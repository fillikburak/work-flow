**Table Of Contents**

[TOC]

#CSharp
##Generics
###Generic Structures
- Make a generic structure:

```C#
interface IRepository<T>{
  List<T> GetList();
  T Get(int id);
  void Add(T entity);
  void Update(T entity);
  void Delete(T entity);
}

interface ICustomerDal : IRepository<Customer>{
  void CustomMethod();
}

interface IProductDal : IRepository<Product>
}

class CustomerDal : ICustomerDal{
  //methods
}

class ProductDal : IProductDal{
  //methods
}
```

----
###Generic Methods
- Make a generic method

```C#
List<string> result = BuildList<string>("a","b","c");

public List<T> BuildList<T>(params T[] items){
    return new List<T>(items)
}
```

###Generic Limitations
- where `T` : class means you are must be a reference type
- `new()` means you have to renewable (e.g int is value type, string is reference type)
- `IEntity` means you have to convertible to `IEntity` so you can create `IRepository<Student>` but cannot create `IRepository<IStudentDal>`
- If u want to allow value types u can use `struct` keyword like : where `T` : `struct`


```C#
interface IRepository<T> where T: class, IEntity, new()
{
  List<T> GetList();
  T Get(int id);
  void Add(T entity);
  void Update(T entity);
  void Delete(T entity);
}

interface IEntity{
}

interface IStudentDal : IRepository<Student>{
}

interface ICustomerDal : IRepository<Customer>{
  void CustomMethod();
}

interface IProductDal : IRepository<Product>{  
}

class StudentDal : IStudentDal{
  //methods
}

class CustomerDal : ICustomerDal{
  //methods
}

class ProductDal : IProductDal{
  //methods
}

class Student : IEntity{
  //props
}

class CustomerDal : IEntity{
  //props
}

class ProductDal : IEntity{
  //props
}
```
