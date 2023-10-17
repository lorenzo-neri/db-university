<!-- 
Dopo aver creato un nuovo database nel vostro phpMyAdmin e aver importato lo schema allegato, eseguite le query del file allegato.
Cosa consegnare?
Dopo aver testato le vostre query con phpMyAdmin, riportatele in un file query.md e caricatelo nella vostra repo.
-->

1. SELECT * FROM `students` WHERE YEAR(date_of_birth) = 1990;

2. SELECT * FROM `courses` WHERE cfu > 10;

3. SELECT * FROM `students` WHERE TIMESTAMPDIFF(YEAR, date_of_birth, CURRENT_DATE()) > 30;

4. SELECT * FROM `courses` WHERE `period` = 'I semestre' AND `year` = 1;

5. SELECT * FROM `exams` WHERE HOUR(`hour`) >= 14 AND `date` = '2020-06-20';

6. SELECT * FROM `degrees` WHERE `level` = 'magistrale';

7. SELECT * FROM `departments`
7. SELECT COUNT(*) AS `departments_count` FROM `departments`;

8.SELECT * FROM `teachers` WHERE `phone` IS NULL;

