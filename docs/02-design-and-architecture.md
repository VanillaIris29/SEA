# 02 – Design and Architecture

## 1. Тип и структура на приложението

Приложението е **уеб базирана система за онлайн курсове**, разработена с **ASP.NET Core MVC** и **Entity Framework Core**.  
То следва архитектурен модел **MVC (Model–View–Controller)** и използва **ASP.NET Identity** за управление на потребители, роли и автентикация.

Проектът е организиран в следните основни части:

- **Controllers/** – обработват заявки и управляват логиката.
- **Models/** – домейн модели и ентитита.
- **ViewModels/** – модели, използвани за форми и изгледи.
- **Views/** – Razor изгледи за визуализация.
- **Data/** – база данни, EF Core контекст.
- **Areas/Identity/** – стандартни Identity страници.

---

## 2. Модел на данните

Приложението използва релационна база данни (SQL Server) чрез Entity Framework Core.

### Основни ентитита:

#### **Course**
- Id  
- Title  
- ShortDescription  
- Description  
- DurationHours  
- DurationDays  
- Price  
- MaxParticipants  
- CurrentParticipants  
- ImagePath  
- HasCertificate  
- StartDate  
- EndDate  
- CategoryId (FK)
- Category  
- OrganizerId (FK)
- Organizer
- Enrollments (колекция)

#### **Enrollment**
- Id  
- UserId (FK)
- User 
- CourseId (FK)
- Course
- EnrolledOn  

#### **Category**
- Id  
- Name
- Courses

#### **ApplicationUser**
Разширява IdentityUser с:
- FirstName  
- MiddleName  
- LastName  
- City  
- Country  
- Age
- CreatedCourses

---

## 3. Таблици и връзки

### Връзки между таблиците:

- **Course – Category**: много към едно  
- **Course – Enrollment – ApplicationUser**:
  - 1 курс → много записвания  
  - 1 потребител → много записвания  
- **Course – Organizer (ApplicationUser)**: много курсове към един организатор  

### ER диаграма:
- Course — Enrollment — ApplicationUser
- Course — Category
- ## 5. Потребителски поток

### Роли:
- **Anonymous** – вижда списък с курсове и детайли.
- **User** – може да се записва за курсове.
- **Organizer** – създава и управлява свои курсове.
- **Admin** – управлява всички курсове и потребители.

### Основни страници:

- `Course/All` – списък с курсове  
- `Course/Details/{id}` – детайли за курс  
- `Course/Create` – създаване на курс  
- `Course/Edit/{id}` – редакция  
- `Course/Manage` – курсове на организатора  
- `Course/ManageAll` – всички курсове (Admin)  
- `Course/Participants/{id}` – участници в курс  
- `Course/ManageExpired` – изтекли курсове (Organizer)
- `Course/ManageAllExpired` – всички изтекли курсове (Admin)
- `Category/Create` – създаване на категория (Admin)
- `UserCourses/MyCourses` – списък с курсовете в които е записан участник
### Примерен потребителски поток:

1. Потребителят отваря списъка с курсове.  
2. Избира курс и разглежда детайлите.  
3. Влиза в системата.  
4. Записва се за курс.  
5. Вижда своите записани курсове.

## 6. Основни модули / слоеве

### **Presentation Layer**
- Razor Views  
- HTML/CSS/Bootstrap  

### **Application Layer**
- Controllers  
- ViewModels  
- Бизнес логика  

### **Data Layer**
- EF Core  
- ApplicationDbContext  
- Модели и връзки  

## 7. Използвани технологии

- **Език:** C#  
- **Framework:** ASP.NET Core MVC  
- **ORM:** Entity Framework Core  
- **База данни:** SQL Server  
- **UI:** Razor Views, Bootstrap  
- **Автентикация:** ASP.NET Identity  
- **Други:** LINQ, TempData, ViewBag  

## 8. Защо са избрани тези технологии

- **ASP.NET Core MVC** – модерен, бърз и подходящ за уеб приложения.  
- **EF Core** – улеснява работата с база данни чрез ORM.  
- **Identity** – готова и сигурна система за потребители и роли.  
- **SQL Server** – стабилна релационна база, интегрирана с .NET.  
- **Bootstrap** – бърз и лесен начин за responsive дизайн.  
