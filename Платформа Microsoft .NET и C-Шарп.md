C# --> си - подобный , ООП' ый, кросс-платформенный ЯП 

Область применения:
	-Геймдев (Unity)
	-Веб-приложения
	-Моб. разработка.
	-Enterprise-разработка

![[Pasted image 20250422121737.png]]

Generict --> Обобщения. Помогают создавать классы и методы без привязки к каким-либо типам данных.

LINQ --> Нужен для упрощенной работы с БД. То есть ну надо связываться через запросы SQL с БД, т.к. в c# уже есть встроенные методы, помогающие обращаться к БД. 

async / await --> Поддержка асинхронного программирования. 

Nullable --> Переменные могут быть равны NULL

![[Pasted image 20250422122759.png]]

![[Pasted image 20250422123633.png]]

JIT - компиляция --> Занижает скорость программы 

![[Pasted image 20250422124014.png]]

![[Pasted image 20250422124804.png]]

CLR /CIL --> CLR (Common Language Runtime) и CIL (Common Intermediate Language) — компоненты концепции Common Language Infrastructure (CLI), которая лежит в основе платформы .NET. 


![[Pasted image 20250422125103.png]]

SilverLight --> Первая попытка войти в кроссплатформенности

.Net Core --> Полностью кроссплатформенная.

![[Pasted image 20250422125436.png]]


BCL --> Базовая библиотека классов.

CLR --> Общая языковая среда выполнения. Управление памятью, многопоточность, компиляция и т.д.

CIL -->  Промежуточный язык.  

JIT - компиляция --> Just in time. Сначала программа переводит на язык CIL,а уже потом на машинный код.
 (Более развурнуто:
 На первом этапе исходный код преобразуется в CIL — промежуточный язык, который не содержит команд, зависящих от языка, операционной системы и типа компьютера. В результате компиляции создаётся сборка — файл с расширением exe или dll, который содержит код на языке CIL и метаданные. 
 На втором этапе происходит JIT-компиляция, во время которой код CIL переводится в машинный код, но не сразу, а только по мере необходимости во время выполнения программы.
  )

![[Pasted image 20250422130341.png]]

##### LINQ

LINQ --> инструмент, который упрощает работу с коллекциями и данными, предоставляя SQL-подобный синтаксис для запросов к объектам.

Есть синтаксис методов и запросов

Лямда-выражение --> представляет собой подобие функцию (параметр, который передаётся в функцию) и выражение (методы, которые делаются там)
**Например**: 
	a => a > 5;
	a => a*2;

```
// Синтаксис методов
int[] nums = { 1, 2, 3, 4, 5 ,10,5}; 
// Какой-то массив данных
var evenNums = nums.Where(n => n % 2 == 0); 
// evenNums --> Новый массив, n --> лямбда 
```

```
// Синтаксис запросов
var evenNums2 = from n in nums
                where n % 2 == 0
                select n;
// Вывод через любой цикл (for, while, foreach)
```

```
// OrderBy --> сортирует элементы по возрастанию
// OrderByDescending --> сортирует элементы по убыванию
// ThenBy --> применяется после OrderBy для дополнительной сортировки по возрастанию
 // ThenByDescending --> аналогично ThenBy, но сортирует по убыванию
```

```
string[] names = { "Aba", "adwa", "hnasd", "dawbhe" };

var sortedNames = names.OrderBy(n => n.Length); 
// OrderBy --> Сортировка имён по длине имени
var sored_Names2 = names.OrderByDescending(n => n.Length); 
// OrderByDescending --> Сортировка имёт по длине имени + убывание
```

```
// Через синтаксиса запроса
var sortedNames3 = from n in names orderby n.Length select n;
```

```
select --> используется для преобразования (проекции) элементов коллекции
...
var sq = nums.Select(n => n*n);
```

```
Count() --> Вернёт кол-во элементов в массиве
Sum() --> Вернут сумму элементов в массиве
Min() --> Вернёт минимальный элемент в массиве
Max() --> Вернёт максимальное элемент в массиве
Average() --> Вернёт среднее значение в массиве
// Пример

int count = nums.Count();

var res = nums.Where(n => n % 2 == 1)
              .OrderByDescending(n => n)
              .Select(n=> n * n);
```

```
GroupBy --> Группирует элементы коллекции по заданному ключу
// Пример
    var people = new List<Person>
    {
        new Person ("Tom", 30),
        new Person("Lol", 30),
        new Person("Alice", 42),
        new Person("Bob", 26),
        new Person("gAbe", 14)
	};
    var groupedPeople = people.GroupBy(n => n.Age);
// Перебор 
foreach (var group in groupedPeople){
	Console.WhriteLine($"Возраст {group.Key}");
	foreach (var person in group){
		Console.WhiteLine(person.Name)
	}
}
```
```
Join --> слиение / объединение
//**Пример**
var departments = new List<Department>
{
    new Department(1,"Hr"),
    new Department(2,"It")
};

var employees = new List<Employee>
{
    new Employee("Alice", 1),
    new Employee("Bob", 1),
    new Employee("jonh", 1)

};

var employeeDepartments = departments.Join(
    employees,
    d => d.Id,
    e => e.DepartamentId,
    (d, e) => new { DepartmentName = d.Name, EmployeeName = e.Name });
```

```
Concat --> объединение без удаление дубликатов
// **Пример**
int[] nums3 = { 1, 2, 4, 5, 7, 8 };
int[] nums5 = { 5, 2, 5, 7, 98 };

var nums56 = nums3.Concat(nums5);
```

```
Distinct --> Удаление дубликатов
// **Пример**
var nums57 = nums3.Distinct();
```

```
Union --> объединение с удалением дубликатов
// **Пример**
var nums58 = nums3.Union(nums5);
```

```
Intersect --> Пересечение коллекций (Элементы, которые встречаются во всех коллекциях (в двух))
// **Пример**
var nums77 = nums3.Intersect(nums5);
```

```
Except --> разность коллекций (то есть где есть в первой, но нету во второй)
// **Пример**
var num101 = nums3.Except(nums5);
var num102 = nums5.Except(nums3);
```

```
Skip, Take --> Нужны для разбивания данных (достать из коллекции какую-либо часть). Skip --> Какое кол-во данных надо пропустить, Take --> Какое кол-во данных надо взять.
// **Пример**
int[] nums = {1,3,4,5,76,8};
var n1 = nums.Take(2);
var n2 = nums.Skip(2);
```

```
SkipWhile, TakeWhile --> Тоже самое, только можно указывать условия, пока оно действует, то будет работать.
// **Пример**
int [] nums = {1,2,4,5,6,7};
var n4 = num3.TakeWhile(n => n < 3) // 1,2
var n5 = num3.SkipWhile(n => n < 3) // 4,5,6,7
```







