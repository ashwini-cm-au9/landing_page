DELIMITER $$
CREATE EVENT IF NOT EXISTS your_event
ON SCHEDULE EVERY 1 WEEK
STARTS CURRENT_TIMESTAMP
COMMENT 'Insert data on Thursday and Friday'
DO
BEGIN
    IF DAYOFWEEK(NOW()) IN (5, 6) THEN
        INSERT INTO your_table (data_column) VALUES ('Your Data Here');
    END IF;
END;
$$
DELIMITER ;

SET GLOBAL event_scheduler = ON;
DELIMITER $$
CREATE EVENT IF NOT EXISTS insert_timeslots_event
ON SCHEDULE EVERY 1 WEEK
STARTS CURRENT_TIMESTAMP
COMMENT 'Insert timeslots on Thursday and Friday'
DO
BEGIN
    IF DAYOFWEEK(NOW()) = 5 THEN -- Thursday (5)
        INSERT INTO timeslots (timeslot_datetime) VALUES (DATE_ADD(CURRENT_DATE, INTERVAL 10 HOUR));
    END IF;
    
    IF DAYOFWEEK(NOW()) = 6 THEN -- Friday (6)
        INSERT INTO timeslots (timeslot_datetime) VALUES (DATE_ADD(CURRENT_DATE, INTERVAL 14 HOUR));
    END IF;
END;
$$
DELIMITER ;
