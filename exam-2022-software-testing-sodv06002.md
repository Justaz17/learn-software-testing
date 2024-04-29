
# TECHNOLOGICAL UNIVERSITY OF THE SHANNON: MIDLANDS MIDWEST

**SUMMER** **EXAMINATION 2022**

SODV06002 – Software Testing

**MODULE:  PROGRAMME(S):**

LC\_KGDVM\_KTH

LC\_KSFDM\_KMY LC\_KSFDM\_ITH LC\_KISYM\_JMY

LC\_KISYM\_KMY

LC\_KIDMM\_KMY LC\_KCPTM\_JMY

**YEAR OF STUDY:  EXAMINER(S):**

SODV06001 Software Testing:

- Bsc. (Honours) Games Design and Development
- Bsc. (Honours) Software Development Higher Certificate in Science Software Development
- Bsc. (Honours) Internet Systems Development Bachelor of Science
- Bsc. (Honours) Interactive Digital Media Bachelor of Science Computing

2 

Mr. Brendan Watson  (Internal) Mr. Andrew Shields  (External) 

SODV06002 – Software Testing   Page 4 of 4 Summer Exam 

**TIME ALLOWED:   2 HOURS** 

**INSTRUCTIONS:  Answer any 3 questions. All questions carry equal** 

**marks and marks will be scaled to 100.**  

PLEASE DO NOT TURN OVER THIS PAGE UNTIL YOU ARE INSTRUCTED TO DO SO. The use of programmable or text storing calculators is expressly forbidden. Please note that where a candidate answers more than the required number of questions, the examiner will mark all questions attempted and then select the highest scoring ones.  

There are no additional requirements for this paper. 

**Question 1                (Total 33 Marks)** 

1) Explain your understanding of the goal of software testing and the implications of the goal of software testing. 

**(11 marks)** 

2) Do you think scenarios and use cases can be used for software testing, explain your answer?  

**(11 marks)** 

3) Explain your understanding of the big bang approach to software testing. Do you think you will ever use this approach in the future, explain your answer? 

**(11 marks)** 

**Question 2                  (Total 33 Marks)** 

1. Develop a control flowgraph for the code shown in Figure 1 below and determine the complexity. Suppose software testing has been employed so that TER1 = 1 and TER2 = 1, would you recommend further testing and explain your answer.  **(11 marks)**
2. Develop the branch table for the code shown in Figure 1 below. **(11 marks)**
3. Develop the block table for the code shown in Figure 1 below. **(11 marks)**

```java
public void walkFirstColOfGridEatingPies(Grid aGrid)
{
    initialize();
    for (int i=1; i <= 2; i++)
    {
        turn ("right");
    }

    for (int j=1; j <= 2; j++)
    {
        if(aGrid.pieInSight (this) == true)
        {
        eatPie (aGrid) ;
        }
        else
        {
            walk (aGrid) ;
        }
    }
}
```

> Figure 1

## **Question 3   (Total 33 Marks)**  

An OvertimeHoursProcessor component has a method called processOvertimeHours which contains business logic about processing of overtime hours worked. The code for the processOvertimeHours is shown in Figure 2 below. 

```java
package com.mycompany.overtimehoursprocessor;
import java.util.Calendar;

public class OvertimeHoursProcessor {

    public OvertimeHoursProcessor() {}// Default constructor

    public Boolean processOvertimeHours(String overtimeHoursFile) {
        //First piece of business logic is to check the overtimeHoursFile has
        // valid extension.
        if (overtimeHoursFile.endsWith(".data"))
        {
            //Next piece of business logic is to check that it is a Saturday
            // as hours worked thia day are overtime rate. 
            Calendar cal = Calendar.getInstance();
            if (cal.get(Calendar.DAY_OF_WEEK) == Calendar.SATURDAY))
            {
                readTheOvertimeHoursFile();
                return true;
            }
            else
            {
                return false;
            }
        }
        else
        {
            return false;
        }
    }

    public void readTheOvertimeHoursFile() {
        /* ... */
    }
    /* ... */
}
// This code is under conatruction and is not currently needed
// to unit test the business logic in the processOvertimeMours method.
```

1) Explain what a stub is and why you need to utilize stubs to unit test code.  **(8 Marks)** 

A stub is a piece of code that simulates the behaviour of a component that the system under test depends on.  For example the component may not be available or may have not been implemented yet.  It may not be necessary to use a real implementation of the component such as a database or web service in a unit test to test a system or piece of the system/code a stub would be suitable.

2) Refactor the OvertimeHoursProcessor to make it testable by introducing a layer of indirection to avoid the dependency i.e. write code or pseudocode. You refactoring should include adding an interface which will allow use of a configurable stub in the unit tests.   **(12 Marks)** 

```java
package com.mycompany.overtimehoursprocessor;

/**
 * Interface for the OvertimeHoursFileProcessor
 */
public interface OvertimeHoursFileProcessor {

    public String getOvertimeHoursFile();
    public void setOvertimeHoursFile(String overtimeHoursFile);

    public void readTheOvertimeHoursFile();
}

/**
 * OvertimeHoursFileProcessorStub
 */
import org.apache.commons.logging.Log;

public class OvertimeHoursFileProcessorStub implements OvertimeHoursFileProcessor {

    private static final Log log = LogFactory.getLog(OvertimeHoursFileProcessorStub.class);
    private String overtimeHoursFile;


    public String getOvertimeHoursFile() {
        return "overtimeHoursFile";
    }

    public void setOvertimeHoursFile(String overtimeHoursFile) {
    }

    public void readTheOvertimeHoursFile() {
        log.info("Stub for Reading the overtime hours file");
    }
}

import java.util.Calendar;

/**
 * Refactored OvertimeHoursProcessor
 
 */
public class OvertimeHoursProcessor {

    private final OvertimeHoursFileProcessor overtimeHoursFileProcessor;

    public OvertimeHoursProcessor(OvertimeHoursFileProcessor overtimeHoursFileProcessor) {
        this.overtimeHoursFileProcessor = overtimeHoursFileProcessor;
    }


    public Boolean processOvertimeHours() {
        //First piece of business logic is to check the overtimeHoursFile has
        // valid extension.
        if (overtimeHoursFileProcessor.getOvertimeHoursFile().endsWith(".data"))
        {
            //Next piece of business logic is to check that it is a Saturday
            // as hours worked this day are overtime rate. 
            Calendar cal = Calendar.getInstance();
            if (cal.get(Calendar.DAY_OF_WEEK) == Calendar.SATURDAY))
            {
                overtimeHoursFileProcessor.readTheOvertimeHoursFile();
                return true;
            }
            else
            {
                return false;
            }
        }
        else
        {
            return false;
        }
    }

```java

1) Write code or pseudocode for three unit tests to test the business logic in the processOvertimeHours method. Write code or pseudocode for a configurable stub to be used by your tests utilising constructor injection. 

**(13 Marks)** 

**Question 4    Total 33 Marks**  

1) Explain your understanding of equivalence partitioning.  

**(10 Marks)** 

2) A software system to accept new stock items in a steel yard accepts the item name followed by a list of different lengths the steel comes in. The specification states that the item name is to be alphabetic 5 to 10 characters long. Each length in metres must be in the range of 1 to 7, whole numbers only. The lengths are to be entered in descending order (biggest length first) with a maximum of 3 lengths allowed to be entered for each item and whole numbers only. A comma is to be used to separate the item name from the lengths and a comma will be used to separate each length and the enter key to be pressed after the last length is entered 

   Derive the equivalence classes and determine black box test cases based on these and utilise boundary value analysis.   **(23 Marks)** 
SODV06002 – Software Testing   Page 4 of 4 Summer Exam 
