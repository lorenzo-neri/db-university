<!-- 
Group by:
Contare quanti iscritti ci sono stati ogni anno
Contare gli insegnanti che hanno l'ufficio nello stesso edificio
Calcolare la media dei voti di ogni appello d'esame
Contare quanti corsi di laurea ci sono per ogni dipartimento
Joins:
Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
-->

# query-1

## Group by

### Contare quanti iscritti ci sono stati ogni anno
```sql
SELECT YEAR(`enrolment_date`) AS enrolment_year, COUNT(*) students
FROM students
GROUP BY YEAR(`enrolment_date`);
```

### Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```sql
SELECT office_address, COUNT(*) teachers
FROM teachers 
GROUP BY office_address;
```

### Calcolare la media dei voti di ogni appello d'esame
```sql
SELECT COUNT(`exam_id`), AVG(`vote`) 
FROM `exam_student` 
GROUP BY `exam_id`;
```

### Contare quanti corsi di laurea ci sono per ogni dipartimento
```sql
SELECT COUNT(*), `department_id`
FROM `degrees`
GROUP BY `department_id`;
```

## Joins

### Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```sql
SELECT `students`.`name`, `students`.`surname`, `students`.`registration_number`, `degrees`.`name`
FROM `students`
JOIN `degrees` ON `degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```

### Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
```sql
SELECT `degrees`.`name`, `degrees`.`level`, `departments`.`name` AS `department_name`
FROM `degrees`
JOIN `departments` ON `department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' AND `degrees`.`level` = 'Magistrale';
```

### Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```sql
SELECT `courses`.`name`, `teachers`.`name`, `teachers`.`surname`
FROM `course_teacher`
JOIN `courses` ON `course_id` = `courses`.`id`
JOIN `teachers` ON `teacher_id` = `teachers`.`id`
WHERE `teacher_id` = 44;
```

### Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
```sql
SELECT `students`.`name`, `students`.`surname`, `degrees`.`name`, `degrees`.`level`, `departments`.`name`
FROM `students`
JOIN `degrees` ON `degree_id` = `degrees`.`id`
JOIN `departments` ON `department_id` = `departments`.`id`
ORDER BY `students`.`name`, `students`.`surname` ASC;
```

### Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```sql
SELECT `degrees`.`name`, `courses`.`name`, `teachers`.`name`, `teachers`.`surname`
FROM course_teacher
JOIN courses ON course_id = `courses`.`id`
JOIN teachers ON teacher_id = `teachers`.`id`
JOIN degrees ON degree_id = `degrees`.`id`;
```

