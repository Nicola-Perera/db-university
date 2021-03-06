# Queries

## Query con Group by
1. Contare quanti iscritti ci sono stati ogni anno
{SELECT COUNT(id) AS `numero iscritti`, YEAR(`enrolment_date`) AS `anno` FROM `students` GROUP BY YEAR(`enrolment_date`)}

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
{SELECT COUNT(id) AS `numero insegnanti`, `office_address` AS `ufficio` FROM `teachers` GROUP BY `office_address`}

3. Calcolare la media dei voti di ogni appello d'esame
{SELECT AVG(`vote`) AS `media voti`, `exam_id` FROM `exam_student` GROUP BY `exam_id`}

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
{SELECT COUNT(id) AS `numero di corsi di laurea`, `department_id` FROM `degrees` GROUP BY `department_id`}

## Query con Join
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
{SELECT *, `degrees`.`name` FROM `students` INNER JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id` WHERE `degrees`.`name` = 'Corso di Laurea in Economia'}

2. Selezionare tutti i Corsi di Laurea del Dipartimento di Neuroscienze
{SELECT *, `departments`.`name` FROM `degrees` INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id` WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'}

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
{SELECT *, `course_teacher`.`teacher_id`, `teachers`.`id` FROM `teachers` INNER JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id` INNER JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id` WHERE `teachers`.`id` = 44}

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
{SELECT *, `course_teacher`.`teacher_id`, `teachers`.`id`, `degrees`.`id`, `departments`.`id` FROM `teachers` INNER JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id` INNER JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id` INNER JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id` INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` WHERE `departments`.`id` = 54}

## BONUS: 
1. Selezionare per ogni studente quanti tentativi d???esame ha sostenuto per superare ciascuno dei suoi esami