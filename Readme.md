## Cómo usamos Entity Framework Core

En este ejemplo usaremos SQLite para persistir la información. Lo instalaremos a través **NuGet Package Manager** buscando el tipo **Microsoft.EntityFrameworkCore.Sqlite**

El ejemplo consiste en realizar un CRUD sobre la entidad **Person**

~~~

        public IActionResult Index()
        {
            //return View();
            return View(_context.People.ToList());
        }

        public IActionResult Edit(int id)
        {
            var person = _context.People.SingleOrDefault(m => m.PersonId == id);
            person.FirstName = "Brandon";
            _context.Update(person);
            _context.SaveChanges();
            return RedirectToAction(nameof(Index));
        }

        public IActionResult Create()
        {
            _context.Add(new Person() { FirstName = "Robert", LastName = "Berends", City = "Birmingham", Address = "2632 Petunia Way" });
            _context.SaveChanges();
            return RedirectToAction(nameof(Index));
        }

        public IActionResult Delete(int id)
        {
            var person = _context.People.SingleOrDefault(m => m.PersonId == id);
            _context.People.Remove(person);
            _context.SaveChanges();
            return RedirectToAction(nameof(Index));
        }
        
~~~
