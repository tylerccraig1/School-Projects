DROP TABLE employees;
DROP TABLE equipment;
DROP TABLE locations;
DROP TABLE manufacturers;
DROP TABLE position_codes;
DROP TABLE task_category;
DROP TABLE tasks;

/*##################################################CREATE MANUFACTURERS TABLE##############################################################*/
CREATE TABLE manufacturers
(   mfg_code NUMBER (4),
    mfg VARCHAR2 (30) NOT NULL,
    address VARCHAR2 (30),
    city VARCHAR2 (15),
    country VARCHAR2 (15),
    website VARCHAR2 (30) NOT NULL,
    
        CONSTRAINT manufacturers_mfgCode_pk PRIMARY KEY (mfg_code),
        CONSTRAINT manufacturers_mfg_uq UNIQUE (mfg));
        
INSERT INTO manufacturers
    VALUES (1000, 'Weyland-Yutani', '1131 Kings Street', 'London', 'United Kingdom', 'weylandyutani.com');

INSERT INTO manufacturers
    VALUES (1001, 'Cyberdyne Systems', '2341 Infinity Way', 'Houston', 'United States', 'skynet.net');
    
INSERT INTO manufacturers
    VALUES (1003, 'Wayne Industries', '267 Washington Ave', 'Gotham', 'United States', 'wayneenterprises.com');

INSERT INTO manufacturers
    VALUES (1004, 'Aperture Laboratories', '4545 Memorial Way', 'Ooahu', 'United States', 'aperturescience.com');

INSERT INTO manufacturers
    VALUES (1005, 'CBT Company', '130 Advanced Drive', 'Sprinboro', 'United States', 'cbtcompany.com');
    
INSERT INTO manufacturers
    VALUES (1006, 'Allen-Bradley', '124 Industrial Rd', 'Milwaukee', 'United States', 'allenbradley.com');

INSERT INTO manufacturers
    VALUES (1007, 'Scott Propulsion', '4849 Enterprise Blvd', 'Glasgow', 'Scotland', 'scottprop.net');

INSERT INTO manufacturers
    VALUES (1008, 'Ishimura Mining', '1890 Yamaha Rd', 'Kyoto', 'Japan', 'ishimuamine.com');

INSERT INTO manufacturers
    VALUES (1009, 'Stark Industries', '985 Malibu Way', 'Malibu', 'United States', 'starkindustries.com');

INSERT INTO manufacturers
    VALUES (1010, 'Union Aerospace', '333 Armstrong Ave', 'Houston', 'United States', 'unionaerospace.net');
    
INSERT INTO manufacturers
    VALUES (1011, 'IFM Efector', '1671 Essen Way', 'Essen', 'Germany', 'ifm.com');

INSERT INTO manufacturers
    VALUES (1012, 'Rolls Royce', '1221 Thames Blvd', 'London', 'United Kingdom', 'rollsroyce.com');
    
    
    
/*##################################################CREATE LOCATIONS TABLE###################################################################*/
CREATE TABLE locations
(   location_code CHARACTER (5),
    facility VARCHAR2 (10) NOT NULL,
    department VARCHAR2 (50),
    floor NUMBER (3) NOT NULL,
    room NUMBER (5) NOT NULL,
    description VARCHAR2 (50),
    
        CONSTRAINT locations_CodeFacility_pk PRIMARY KEY (location_code, facility));

INSERT INTO locations
    VALUES ('EN000', 'Site A', 'Engineering', 000, 00002, 'Eng Lab 2');

INSERT INTO locations
    VALUES ('AI005', 'Site A', 'AI Development', 005, 00510, 'AI Dev Lab 10');

INSERT INTO locations
    VALUES ('PT001', 'Site C', 'Propulsion Testing', 001, 00102, 'Prop Testing Area 2');

INSERT INTO locations
    VALUES ('CC001', 'Site A', 'Central Control', 001, 00101, 'Site A Central Control');
    
INSERT INTO locations (location_code, facility, floor, room)
    VALUES ('MB001', 'Site A', '000', '00001');
    
    
    
/*##################################################CREATE POSITION_CODES TABLE###################################################################*/
CREATE TABLE position_codes
(   position_code CHAR (4),
    position VARCHAR2 (20) NOT NULL,
        
        CONSTRAINT positionCodes_positionCode_pk PRIMARY KEY (position_code),
        CONSTRAINT positionCodes_position_uq UNIQUE (position));

INSERT INTO position_codes
    VALUES ('EE01', 'ElectricalEngineer');
    
INSERT INTO position_codes
    VALUES ('ME01', 'MechanicalEngineer');

INSERT INTO position_codes
    VALUES ('CE01', 'ControlsEngineer');

INSERT INTO position_codes
    VALUES ('ME02', 'MiningEngineer');

INSERT INTO position_codes
    VALUES ('OP01', 'Operator');

INSERT INTO position_codes
    VALUES ('EC02', 'Electrician');

INSERT INTO position_codes
    VALUES ('MC02', 'Mechanic');

INSERT INTO position_codes
    VALUES ('TC02', 'Technician');

INSERT INTO position_codes
    VALUES ('SD01', 'COBOLDeveloper');

INSERT INTO position_codes
    VALUES ('SD02', 'JavaDeveloper');

INSERT INTO position_codes
    VALUES ('QI01', 'Quality Inspector');

INSERT INTO position_codes
    VALUES ('SE01', 'SafetyEngineer');



/*##################################################CREATE EMPLOYEES TABLE###################################################################*/
CREATE TABLE employees
(   employeeID NUMBER (5),
    position_code CHAR (4),
    firstName VARCHAR2 (20) NOT NULL,
    lastName VARCHAR2 (20) NOT NULL,
    startDate DATE DEFAULT SYSDATE, 
    phoneNumber CHARACTER (14),
    email VARCHAR2 (30) NOT NULL,
    
        CONSTRAINT employees_employeeID_pk PRIMARY KEY (employeeID),
        CONSTRAINT employees_positionCode_fk FOREIGN KEY (position_code)
            REFERENCES position_codes (position_code),
        CONSTRAINT employees_phoneNumber_uq UNIQUE (phoneNumber),
        CONSTRAINT employees_email_uq UNIQUE (email));
        
INSERT INTO employees
    VALUES (12345, 'ME01', 'Amanda', 'Ripley', '02-JAN-10', '(123)456-7890', 'aripley@bluepropulsion.com');

INSERT INTO employees
    VALUES (23456, 'EE01', 'Issac', 'Clarke', '02-JAN-10', '(234)561-2389', 'iclarke@bluepropulsion.com');

INSERT INTO employees
    VALUES (00992, 'CE01', 'Damon', 'Baird', '03-FEB-12', '(123)412-3145', 'dbaird@bluepropulsion.com');

INSERT INTO employees
    VALUES (00012, 'ME02', 'Carter', 'Matthews', '04-FEB-12', '(324)123-4567', 'cmatthews@bluepropulsion.com');

INSERT INTO employees
    VALUES (00013, 'SE01', 'Frank', 'Jacobs', '08-APR-12', '(222)111-3333', 'fjacobs@bluepropulsion.com');
    
INSERT INTO employees
    VALUES (10699, 'CE01', 'Yuki', 'Hamara', '08-APR-12', '(456)123-6734', 'yhamara@bluepropulsion.com');

INSERT INTO employees
    VALUES (10698, 'QI01', 'Samir', 'Nadir', '09-MAY-12', '(333)245-5647', 'snadir@bluepropulsion.com');
    
INSERT INTO employees
    VALUES (70912, 'SD01', 'Hal', 'Kyles', '05-JUN-12', '(555)666-7878', 'hkyles@bluepropulsion.com');

INSERT INTO employees
    VALUES (10234, 'SD02', 'Jimmy', 'Buffett', '09-JUN-12', '(555)555-5555', 'jbuffett@bluepropulsion.com');

INSERT INTO employees
    VALUES (00233, 'TC02', 'Wess', 'Brookes', '10-JUN-12', '(999)888-7777', 'wbrookes@bluepropulsion.com');

INSERT INTO employees
    VALUES (00232, 'ME01', 'Homer', 'Hickam', '11-JUN-12', '(332)555-6767', 'hhickam@bluepropulsion.com');





/*##################################################CREATE EQUIPMENT TABLE###################################################################*/
CREATE TABLE equipment
(   equipmentID VARCHAR2 (5),
    description VARCHAR2 (30),
    status VARCHAR2 (6) DEFAULT 'Active',
    serialNo VARCHAR2 (30) NOT NULL,
    productNo VARCHAR2 (30) NOT NULL,
    mfg_code NUMBER (4),
    purchase_price NUMBER (7),
    install_date DATE DEFAULT SYSDATE,
    location_code CHARACTER (5) NOT NULL,
    
        CONSTRAINT equipment_equipmentID_pk PRIMARY KEY (equipmentID),
        CONSTRAINT equipment_status_ck CHECK (status IN ('Active', 'Down')),
        CONSTRAINT equipment_serialNo_uq UNIQUE (serialNo),
        CONSTRAINT equipment_mfgCode_fk FOREIGN KEY (mfg_code)
            REFERENCES manufacturers (mfg_code));

INSERT INTO equipment
    VALUES ('WY102', 'WY Warp Drive 01', 'Active', 'WY102-123-16', 'WYWD134', 1000, 1234567, '08-OCT-19', 'PT001');

INSERT INTO equipment
    VALUES ('WY103', 'WY Warp Drive 02', 'Active', 'WY102-123-17', 'WYWD134', 1000, 1234567, '08-OCT-19', 'PT001');

INSERT INTO equipment
    VALUES ('CS002', 'Skynet Defense Sensor', 'Active', 'CS-SKY-01241', 'SNET1322', 1001, 14562, '03-Feb-20', 'AI005');

INSERT INTO equipment
    VALUES ('UA001', 'UnionAerospace Impact Driver', 'Active', 'UAC0112-1223-43', 'UAC1221ID', 1010, 1122233, '10-OCT-19', 'EN000'); 

INSERT INTO equipment
    VALUES ('WE001', 'WayneEnterprises Tumbler 01', 'Active', '11-00022-02453', 'WE0011234', 1003, 1234561, '31-OCT-19', 'PT001');

INSERT INTO equipment
    VALUES ('SP223', 'Scott Prop Slip Drive 1', 'Active', '44-12442-6578', 'SP200', 1007, 9876543, '12-DEC-11', 'PT001');

INSERT INTO equipment
    VALUES ('AB001', 'Allen-Bradley VFD 750-01', 'Active', 'PW-750-00123', 'AB-PF750-VFD-480', 1006, 3000, '05-APR-15', 'EN001');
    
/*Fixed record with proper equipment ID, re-insert in Equipment table*/
INSERT INTO equipment (equipmentID, description, serialNo, productNo, location_code)
    VALUES ('IM002', 'Ishimua Rotary Drill', 'ISH297-312', 'ISH-RD-002', 'EN000');

/*UPDATE Equipment with proper mfg_code*/ 
UPDATE equipment
    SET mfg_code = 1008 
    WHERE equipmentID = 'IM002';

COMMIT;

/*DELETE Equipment record where EquipmentID = IM002*/
DELETE equipment 
    WHERE equipmentID = 'IM002';

/*Recover deleted record*/  

ROLLBACK;



/*##################################################CREATE TASK_CATEGORY TABLE###########################################################*/
CREATE TABLE task_category
(   category_code VARCHAR2 (5),
    category VARCHAR2 (30) NOT NULL,
    
        CONSTRAINT taskCategory_categoryCode_pk PRIMARY KEY (category_code),
        CONSTRAINT taskCategory_category_uq UNIQUE (category));

INSERT INTO task_category
    VALUES ('RE001', 'REPLACEMENT - Part');

INSERT INTO task_category
    VALUES ('RE002', 'REPLACEMENT - Equipment');

INSERT INTO task_category
    VALUES ('IN001', 'INSTALL - Small Part');

INSERT INTO task_category
    VALUES ('IN002', 'INSTALL - Large Part');
    
INSERT INTO task_category
    VALUES ('CC001', 'CONFIG-CHANGE - Config Change');

INSERT INTO task_category
    VALUES ('CN001', 'CLEAN - General Cleaning');
    
    
    
/*##################################################CREATE TASKS TABLE###################################################################*/
CREATE TABLE tasks
(   taskID NUMBER (5),
    equipmentID VARCHAR2 (5),
    category_code VARCHAR2 (5),
    createdBy NUMBER (5),
    assignedTo NUMBER (5),
    assignmentDate DATE DEFAULT SYSDATE NOT NULL,
    finishedDate DATE,
    totalHrs NUMBER (3),
    cost NUMBER (8,2), 
    comments VARCHAR2 (50),
        
        CONSTRAINT tasks_taskID_pk PRIMARY KEY (taskID),
        CONSTRAINT tasks_categoryCode_fk FOREIGN KEY (category_code)
            REFERENCES task_category (category_code),
        CONSTRAINT tasks_equipmentID_fk FOREIGN KEY (equipmentID)
            REFERENCES equipment (equipmentID),
        CONSTRAINT tasks_createdBy_fk FOREIGN KEY (createdBy)
            REFERENCES employees (employeeID),
        CONSTRAINT tasks_assignedTo_fk FOREIGN KEY (createdBy)
            REFERENCES employees (employeeID));

INSERT INTO tasks
    VALUES (00006, 'WE001', 'CC001', 13, 23456, '04-Jan-18', '04-JAN-18', 10, 1000.81, 'Tumbler Computer needs to be reconfigured');

INSERT INTO tasks
    VALUES (00007, 'WE001', 'IN001', 13, 10699, '05-JAN-18', '07-JAN-18', 20, 2000.20, 'Fire System needs to be replaced'); 

INSERT INTO tasks
    VALUES (00008, 'SP223', 'IN002', 10698, 13, '02-FEB-18', '10-FEB-18', 20, 1000, 'Railings need to be placed around slip drive');

INSERT INTO tasks
    VALUES (00009, 'AB001', 'RE001', 13, 992, '15-APR-20', '15-APR-20', 5, 30.56, 'VFD had overcurrent fault, bad bearings on spindle');  

INSERT INTO tasks
    VALUES (00010, 'WY102', 'CN001', 12345, 23456, '09-JUL-20', '10-JUL-20', 10, 46.72, 'Cold Intake to drive blocked');
    
INSERT INTO tasks (taskID, equipmentID, category_code, createdBy)
    VALUES (00011, 'CS002', 'RE001', 23456);
    
INSERT INTO tasks (taskID, equipmentID, comments)
    VALUES (00012, 'UA001', 'Pressure Sensor on Driver HIGH Fault');

INSERT INTO tasks (taskID, equipmentID, category_code)
    VALUES (00013, 'IM002', 'RE002');

INSERT INTO tasks
    VALUES (00014, 'WY103', 'RE001', 12345, 10699, '07-SEP-20', '08-SEP-20', 100, 1000.89, 'Drive Needs New Fusion Manifold');

INSERT INTO tasks
    VALUES (00015, 'WE001', 'RE001', 12345, 00012, '09-SEP-20', '10-SEP-20', 100, 10000.56, 'Tumbler Needs New Drive Axle');

INSERT INTO tasks
    VALUES (00016, 'AB001', 'RE002', 12345, 992, '10-OCT-20', '11-OCT-20', 20, 3000, 'Gasket on Box Failed, water got into box');
    


/*##################################################ITEM 4: QUERIES TO SELECT INFORMATION FROM MULTIPLE TABLES######################################################*/
/*ITEM 4a: USING COLUMN ALIAS*/
SELECT equipmentID, description AS Equipment_Name, mfg_code, mfg AS manufacturer 
FROM manufacturers JOIN equipment USING (mfg_code);

/*ITEM 4b: PERFORMING BASIC ARITHMETIC*/
SELECT equipmentID, description, SUM(cost) AS Total_Costs, purchase_price, (purchase_price - SUM(cost)) AS Cost_to_Replace 
FROM tasks JOIN equipment USING (equipmentID)
GROUP BY equipmentID, description, purchase_price;

/*ITEM 4c: REMOVING DUPLICATES*/
SELECT DISTINCT city, country FROM manufacturers;
SELECT DISTINCT mfg_code FROM equipment;

SELECT DISTINCT productNo, mfg_code, mfg, website 
FROM equipment JOIN manufacturers USING (mfg_code);

/*ITEM 4d: USING CONCATENATION*/
SELECT firstname || lastname, position_code, position 
FROM employees JOIN position_codes USING (position_code);

SELECT description || serialNo FROM equipment;

SELECT equipmentID, description, serialNo, productNo || mfg
FROM equipment JOIN manufacturers USING (mfg_code);



/*#############################################ITEM 5: QUERIES TO RESTRICT ROWS USING CRITERIA AND COMPOUND CRITERIA#################################################*/
/*ITEM 5a: RANGE CRITERIA (between)*/
SELECT * FROM tasks
    WHERE cost BETWEEN 0 AND 1000;

/*ITEM 5b: USING IN OPERATOR*/
SELECT * FROM tasks
    WHERE category_code IN ('RE001', 'RE002');

/*ITEM 5c: USING LIKE OPERATOR WITH WILDCARDS*/
SELECT * FROM equipment
    WHERE description LIKE 'WY%';

/*ITEM 5d: Ordering of Output*/
SELECT * FROM tasks
    WHERE cost < 1000
    ORDER BY taskID DESC;
   
SELECT taskID, assignedTo, totalHrs, cost, comments FROM tasks
    WHERE assignedTo = 23456
    ORDER BY totalHrs;



/*#############################################ITEM 6: JOINS#################################################*/
/*ITEM 6a: QUERY THAT JOINS 3 TABLES AND LIMITS OUTPUT*/
SELECT taskId, comments, equipmentID, description, mfg, assignedTo
FROM tasks JOIN equipment USING (equipmentID)
            JOIN manufacturers USING (mfg_code)
WHERE equipmentID = 'WE001';
    
/*ITEM 6b: QUERY WITH AN OUTER JOIN*/
SELECT taskID, comments, equipmentID, description, mfg_code, mfg 
FROM tasks LEFT OUTER JOIN equipment USING (equipmentID)
            JOIN manufacturers USING (mfg_code)
ORDER BY taskID;

/*ITEM 6c: QUERY WITH A NON-EQUALITY JOIN*/
SELECT t.taskID, t.comments, t.cost, e.equipmentID, e.description, e.purchase_price
FROM tasks t, equipment e
WHERE t.cost < e.purchase_price


/*ITEM 6d: QUERY USING A SET OPERATION*/
SELECT taskID, category_code, comments, equipmentID, description
FROM tasks JOIN equipment USING (equipmentID)
WHERE category_code = 'RE001'
UNION
SELECT taskID, category_code, comments, equipmentID, description
FROM tasks JOIN equipment USING (equipmentID)
WHERE category_code = 'RE002'
ORDER BY category_code;


/*#############################################ITEM 7: SINGLE ROW FUNCTIONS#################################################*/
/*ITEM 7a: INITCAP*/
SELECT INITCAP(firstname), INITCAP(lastname) FROM employees;

/*ITEM 7b: SUBSTRINGS*/
SELECT DISTINCT SUBSTR(equipmentID,1,2), description FROM equipment
ORDER BY SUBSTR(equipmentID,1,2);

/*ITEM 7c: ROUND*/
SELECT taskID, equipmentID, comments, cost, ROUND(cost, 0) FROM tasks; 

/*ITEM 7d: TOCHAR - USE WITH DATES*/
SELECT equipmentID, description, TO_CHAR(install_date, 'MM-DD-YYYY') AS INSTALL_DATE 
FROM equipment;

/*ITEM 7e: NVL*/
SELECT taskID, equipmentID, NVL(comments, 'Further Investigation Required'), NVL(totalhrs,1), cost
FROM tasks
WHERE NVL(comments, 'Further Investigation Required') = 'Further Investigation Required';

/*ITEM 7f: CASES*/
SELECT equipmentID, SUM(cost) AS MAINTENANCE_COST, purchase_price,
    CASE 
        WHEN (SUM(cost) > purchase_price) THEN 'REPLACE'
        WHEN (SUM(cost) < purchase_price) THEN 'ACTIVE'
        ELSE 'CANNOT DETERMINE'
    END "Equip Life"
FROM tasks JOIN equipment USING(equipmentID)
GROUP BY equipmentID, purchase_price;



/*#############################################ITEM 8: GROUP BY FUNCTIONS#################################################*/
/*ITEM 8a: SUM AND AVERAGE*/
SELECT equipmentID, equipment.description, SUM(cost) AS TOTAL_MAINTENANCE_COST, ROUND(AVG(cost),2) AS AVG_MAINTENANCE_COST, purchase_price
FROM tasks JOIN equipment USING (equipmentID)
GROUP BY equipmentID, equipment.description, purchase_price;

/*ITEM 8b: COUNT*/
SELECT equipmentID, equipment.description, COUNT(equipmentID) AS MAINTENANCE_TASKS
FROM tasks JOIN equipment USING (equipmentID)
GROUP BY equipmentID, equipment.description;

/*ITEM 8c: MIN AND MAX FUNCTIONS*/
SELECT equipmentID, equipment.description, MIN(cost), MAX(cost), purchase_price
FROM tasks JOIN equipment USING (equipmentID)
GROUP BY equipmentID, equipment.description, equipment.purchase_price;

/*ITEM 8d: GROUP WITH A SINGLE TABLE*/
SELECT COUNT(taskID) AS MAINTENANCE_COUNT, assignedTo, lastname
FROM tasks JOIN employees
    ON tasks.assignedTo = employees.employeeID
GROUP BY  assignedTo, lastname;

/*ITEM 8e: GROUP BY SET OR CUBE*/
SELECT COUNT(taskID), category_code, category, ROUND(AVG(cost),2) AS CAT_AVG_COST
FROM tasks JOIN task_category USING (category_code)
GROUP BY GROUPING SETS (category_code, category, (category_code, category));



/*#############################################ITEM 9: SUBQUERIES AND MERGE STATEMENTS#################################################*/
/*ITEM 9a: SINGLE-ROW SUBQUERY WITH A HAVING CLAUSE*/
SELECT employeeID, lastname, AVG(totalhrs)
FROM tasks JOIN employees
    ON tasks.assignedTo = employees.employeeID
HAVING SUM (totalhrs) > (SELECT AVG (totalhrs) FROM tasks)
GROUP BY employeeID, lastname;

/*ITEM 9b: MULTI-ROW SUBQUERY WITH HAVING CLAUSE*/
SELECT equipmentID, SUM(cost / totalhrs) AS Total_Maintenance
FROM tasks
HAVING SUM(cost / totalhrs) < ANY (SELECT SUM(purchase_price / totalhrs)
                                    FROM tasks JOIN equipment USING (equipmentID)
                                    GROUP BY equipmentID)
GROUP BY equipmentID;                                  

/*ITEM 9c: MULTI-COLUMN SUBQUERY WITH A WHERE CLAUSE*/
SELECT category_code, category, taskID, cost AS HIGHEST_CAT_COST
FROM tasks JOIN task_category USING (category_code)
WHERE (category_code, cost) IN (SELECT category_code, MAX(cost)
                                    FROM tasks
                                    GROUP BY category_code)
ORDER BY category_code;

/*TEM 9d: USE A SUBQUERY WITH ALL OPERATOR*/
SELECT taskID, comments, category_code, equipmentID, cost
FROM tasks
WHERE cost > ALL (SELECT cost
                            FROM tasks
                            WHERE category_code = 'CN001');
                            
COMMIT;

/*ITEM 9e: USE A SUBQUERY IN A DML ACTION*/
UPDATE tasks
SET assignedTo = (SELECT MAX(assignedTo)
                    FROM tasks)    
WHERE assignedTo IS NULL;

SELECT * FROM tasks
ROLLBACK;

/*#############################################ITEM 11: VIEWS#################################################*/
/*ITEM 11a: CREATE A SIMPLE VIEW*/
CREATE OR REPLACE VIEW OPEN_TASKS
AS SELECT taskID, comments, equipmentID, equipment.description AS Equipment, 
locations.description AS Location, createdBy, assignedTo, totalhrs, cost
FROM tasks JOIN equipment USING (equipmentID)
            JOIN locations USING (location_code)
WHERE finishedDate IS NULL;
SELECT * FROM OPEN_TASKS

/*ITEM 11b: CREATE A VIEW WITH A CHECK OPTION*/
CREATE OR REPLACE VIEW CLOSED_TASKS AS
SELECT taskID, comments, equipmentID, description, finishedDate, totalhrs, cost, lastname AS CompletedBy
FROM tasks JOIN equipment USING (equipmentID)
           JOIN employees
ON tasks.assignedTo = employees.employeeID
WHERE finishedDate IS NOT NULL
WITH CHECK OPTION;

CREATE OR REPLACE VIEW EQUIPMENT_IDENTIFICATION AS
SELECT equipmentID, description, mfg_code, mfg, serialNo, productNo
FROM equipment JOIN manufacturers USING (mfg_code);

/*ITEM 11c: UPDATE A RECORD IN A SIMPLE VIEW*/
UPDATE EQUIPMENT_IDENTIFICATION
    SET description = 'AB VFD PowerFlex 750'
    WHERE description = 'Allen-Bradley VFD 750-01';
    
/*ITEM 11d: TOP-N ANALYSIS*/
SELECT equipmentID, description, purchase_price
FROM (SELECT equipmentID, description, purchase_price
        FROM equipment
        WHERE purchase_price IS NOT NULL
        ORDER BY purchase_price DESC)
WHERE ROWNUM <=5;



/*#############################################ITEM 12: SEQUENCES AND INDEXES#################################################*/
/*ITEM 12a: CREATE A SEQUENCE*/
CREATE SEQUENCE task_taskID_seq
INCREMENT BY 1
START WITH 00017
NOCYCLE;

INSERT INTO tasks(taskID, equipmentID, category_code, comments)
VALUES (task_taskID_seq.NEXTVAL, 'IM002', 'RE001', 'Drill-Head Needs Replacement');

SELECT * FROM tasks;

/*ITEM 12b: LIST ALL SEQUENCES USING A QUERY*/
SELECT * FROM user_sequences;

/*ITEM 12c: CREATE AN INDEX (OTHER THAN UNIQUE OR PRIMARY KEY*/
CREATE INDEX manufacturer_mfgCode_idx
ON manufacturers (mfg_code, mfg);

SELECT table_name, index_name, index_type
FROM user_indexes WHERE table_name = 'MANUFACTURERS';

/*ITEM 12d: LIST ALL INDEXES USING A QUERY*/
SELECT table_name, index_name, index_type
FROM user_indexes;

/*ITEM 12e: IDENTIFY A COLUMN FOR BITMAP INDEX*/
/*CREATE BITMAP INDEX tasks_taskCategory_idx
ON tasks (category_code)*/