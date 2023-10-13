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


// Create a legend
var legend = new am4maps.Legend();

// Connect the legend to the FlightMap series
legend.parent = chart;
legend.data = series;


// Create a checkbox for the legend item
legend.itemContainers.template.createChild(am4core.CheckBox);


// Configure the checkbox behavior
legend.itemContainers.template.children.getIndex(0).checkbox.events.on("checked", function (event) {
    series.mapImages.each(function (mapImage) {
        mapImage.show = event.target.isActive;
    });
});

// By default, the series should be visible, so set the checkbox to checked
legend.itemContainers.template.children.getIndex(0).checkbox.setState("checked");


// Add your flight data to the series
series.data = yourFlightData;

// Call this method to update the chart's appearance
chart.validateData();
