# Online-Course-Management-System


## Online Course Management System (UML + JavaScript)

This project models a simple **Online Learning Platform** using **Object-Oriented Programming (OOP)** in JavaScript. It incorporates real-world concepts like users, courses, assignments, and grading.

---

## UML Class Diagram

![WhatsApp Image 2025-07-30 at 11 20 21_27a615a4](https://github.com/user-attachments/assets/9db7c78f-96fd-464e-9f7a-f11bfb34b49b)

### Key Relationships

- `User` superclass → `Student` and `Instructor` subclasses
- `Course` has `Instructor`
- `Student` enrolls in `Course`
- `Assignment` belongs to a `Course`
- `Grade` links `Student` and `Assignment`

---

## OOP Concepts Demonstrated

| Principle      | Implementation |
|----------------|----------------|
| **Abstraction** | User, Course, Assignment abstract real-world roles |
| **Encapsulation** | Private fields with getters/setters |
| **Inheritance** | Student & Instructor inherit from User |
| **Polymorphism** | Overridden `login()` method in subclasses |

---

## JavaScript Implementation (Core Classes)
```
class User {
  constructor(id, name, email, password) {
    this._id = id;
    this._name = name;
    this._email = email;
    this._password = password;
  }

  get id() { return this._id; }
  get name() { return this._name; }
  set name(newName) { this._name = newName; }
  get email() { return this._email; }
  set email(newEmail) { this._email = newEmail; }

  login() {
    console.log(${this._name} logged in as basic user);
  }

  logout() {
    console.log(${this._name} logged out);
  }
}

class Student extends User {
  constructor(id, name, email, password, studentId, gradeLevel) {
    super(id, name, email, password);
    this._studentId = studentId;
    this._gradeLevel = gradeLevel;
  }

  get studentId() { return this._studentId; }
  get gradeLevel() { return this._gradeLevel; }

  login() {
    console.log(${this._name} logged in as student);
  }

  enroll(course) {
    console.log(${this._name} enrolled in ${course.title});
  }

  submitAssignment(assignment) {
    console.log(${this._name} submitted ${assignment.title});
  }
}

class Instructor extends User {
  constructor(id, name, email, password, instructorId, department) {
    super(id, name, email, password);
    this._instructorId = instructorId;
    this._department = department;
  }

  get instructorId() { return this._instructorId; }
  get department() { return this._department; }

  login() {
    console.log(${this._name} logged in as instructor);
  }

  createCourse(title, description) {
    const course = new Course(Date.now().toString(), title, description, this);
    console.log(${this._name} created course: ${title});
    return course;
  }

  gradeAssignment(assignment, student, score, feedback) {
    const grade = new Grade(assignment, student, score, feedback);
    console.log(${this._name} graded ${student.name}'s assignment);
    return grade;
  }
}

class Course {
  constructor(id, title, description, instructor) {
    this._id = id;
    this._title = title;
    this._description = description;
    this._instructor = instructor;
    this._assignments = [];
    this._enrollments = [];
  }

  get id() { return this._id; }
  get title() { return this._title; }
  get instructor() { return this._instructor; }

  createAssignment(title, description, dueDate) {
    const assignment = new Assignment(Date.now().toString(), title, description, dueDate);
    this._assignments.push(assignment);
    return assignment;
  }

  enrollStudent(student) {
    const enrollment = new Enrollment(student, this);
    this._enrollments.push(enrollment);
    return enrollment;
  }
}

class Assignment {
  constructor(id, title, description, dueDate) {
    this._id = id;
    this._title = title;
    this._description = description;
    this._dueDate = dueDate;
  }

  get id() { return this._id; }
  get title() { return this._title; }
  get dueDate() { return this._dueDate; }
}

class Enrollment {
  constructor(student, course) {
    this._student = student;
    this._course = course;
    this._enrollmentDate = new Date();
  }

  get student() { return this._student; }
  get course() { return this._course; }
  get enrollmentDate() { return this._enrollmentDate; }

  drop() {
    console.log(${this._student.name} dropped ${this._course.title});
  }
}

class Grade {
  constructor(assignment, student, score, feedback) {
    this._assignment = assignment;
    this._student = student;
    this._score = score;
    this._feedback = feedback;
  }

  get score() { return this._score; }
  get feedback() { return this._feedback; }

  calculate()
  {
    return this._score;
  }
}

const instructor = new Instructor('1', 'Dr. Smith', 'smith@uni.edu', 'pass123', 'inst101', 'Computer Science');
const student = new Student('2', 'John Doe', 'john@student.edu', 'pass456', 'stu202', 'Junior');

instructor.login(); 
student.login();   

const course = instructor.createCourse('Advanced JavaScript', 'Learn advanced JS concepts');
course.enrollStudent(student);

const assignment = course.createAssignment('OOP Project', 'Design an OOP system', new Date('2023-12-31'));
student.submitAssignment(assignment);

const grade = instructor.gradeAssignment(assignment, student, 95, 'Excellent work!');
```

## SOLID Principles

| Principle | Applied As |
|----------|-------------|
| **S** (Single Responsibility) | Each class handles one responsibility |
| **O** (Open/Closed) | Easy to extend with new user roles |
| **L** (Liskov Substitution) | `Student` & `Instructor` used in place of `User` |
| **I** (Interface Segregation) | Classes expose only needed methods |
| **D** (Dependency Inversion) | Grade interacts with abstract entities |

---

