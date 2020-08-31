# Manager Task

## Project setup

```
yarn install
```

### Compiles and hot-reloads for development

```
yarn serve
```

### Compiles and minifies for production

```
yarn build
```

### Lints and fixes files

```
yarn lint
```

## Assignment

Design:

![design]('./design.PNG')

Features:

1. Base on the mock design, build the website interface
2. Create a new task: Users can enter information and create new tasks in the form on the left side of the screen.
   a. Task title is a required field.
   b. Due date has the default value which is today, do not accept days in the past as
   due date
   c. Priority field has three values: low, normal and high. The default value is
   normal.
3. The created tasks will be sorted by Due date from the near future to far future. Each task
   will be displayed as same as the picture bellow
   c. Users can update task data in this form d. When you click the Remove button, this task will be deleted. 4. Users can search tasks by task title. Each time the user enters text, the task list will be filtered and displayed
   Coding Requirement:

- Implement TodoList app base on your framework (angular/ reactjs/ vuejs) - Complete all the functions - Naming convention, es6 or later. - The code is broken into reasonable components - Store data to LocalStorage is a plus - The code smells​good - Not using libraries for CSS is a plus. - Nice and responsive interface is a plus.
  a. When you tick the checkbox, the screen will display a bulk action box
  The bulk action will execute the action for all tasks that have been checked in the checkbox. Temporarily ignore the Done method. The Remove method removes the tasks
  b. When you click the “detail” button, the task item will display detailed information
