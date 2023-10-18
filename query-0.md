<!-- 
Dopo aver creato un nuovo database nel vostro phpMyAdmin e aver importato lo schema allegato, eseguite le query del file allegato.
Cosa consegnare?
Dopo aver testato le vostre query con phpMyAdmin, riportatele in un file query.md e caricatelo nella vostra repo.




Terminale Macos
/Applications/MAMP/Library/bin/mysql -u root -p -P 3366

Terminale Window
C:\MAMP\bin\mysql\bin\mysql -u root -p -P 3366
-->

# query-0

1. SELECT * FROM `students` WHERE YEAR(date_of_birth) = 1990;

2. SELECT * FROM `courses` WHERE cfu > 10;

3. SELECT * FROM `students` WHERE TIMESTAMPDIFF(YEAR, date_of_birth, CURRENT_DATE()) > 30;

4. SELECT * FROM `courses` WHERE `period` = 'I semestre' AND `year` = 1;

5. SELECT * FROM `exams` WHERE HOUR(`hour`) >= 14 AND `date` = '2020-06-20';

6. SELECT * FROM `degrees` WHERE `level` = 'magistrale';

7. SELECT * FROM `departments` || SELECT COUNT(*) AS `departments_count` FROM `departments`;

8. SELECT * FROM `teachers` WHERE `phone` IS NULL;

## Selezionare le informazioni sul corso con id = 144, con tutti i relativi appelli d’esame

```sql
SELECT `courses`.`id` AS `course_id`, `courses`.`name`, `courses`.`description`, `courses`.`period`, `courses`.`cfu`, `courses`.`year`, `courses`.`website`, `exams`.`id` AS `exam_id`, `exams`.`date`, `exams`.`hour`, `exams`.`location`, `exams`.`address`
FROM `courses`
JOIN `exams` ON `courses`.`id` = `exams`.`course_id`
WHERE `courses`.`id` = 144;
```

## Selezionare a quale dipartimento appartiene il Corso di Laurea in Diritto dell'Economia (Dipartimento di Scienze politiche, giuridiche e studi internazionali)

```sql
SELECT departments.*
FROM departments
JOIN degrees ON departments.`id` = `degrees`.`department_id`
WHERE `degrees`.`name` = "Corso di Laurea in Diritto dell'Economia";
```

## Selezionare tutti gli appelli d'esame del Corso di Laurea Magistrale in Fisica del primo anno

```sql
SELECT courses.`name`, `courses`.`period`, `courses`.`cfu`, `exams`.`date`, `exams`.`location`, `exams`.`address`
FROM degrees
JOIN courses ON `courses`.`degree_id` = `degrees`.`id`
JOIN exams ON `exams`.`course_id` = `courses`.`id`
WHERE `courses`.`year` = 1 AND `degrees`.`name` = 'Corso di Laurea Magistrale in Fisica';
```

## Selezionare tutti i docenti che insegnano nel Corso di Laurea in Lettere (21)

```sql
SELECT DISTINCT `teachers`.*
FROM `teachers`     
JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Lettere'
ORDER BY `teachers`.`surname` ASC;
```

## Selezionare il libretto universitario di Mirco Messina (matricola n. 620320)

```sql
SELECT students.name, students.surname, students.registration_number, courses.id, courses.name, exams.date, exam_student.vote
FROM exam_student
JOIN exams ON exam_student.exam_id = exams.id
JOIN students ON exam_student.student_id = students.id
JOIN courses ON exams.course_id = courses.id
WHERE students.name = 'Mirco' AND students.surname = 'Messina' AND exam_student.vote >= 18;
```