     SOC Investigation: Brute Force to Account Compromise


    ## Overview
    This project simulates a real-world SOC (Security Operations Center) analyst workflow — from initial detection of a brute force attack to full incident investigation and reporting. Built using the **Boss of the SOC (BOTS) v1 dataset** in a locally deployed **Splunk Enterprise** environment.

    Unlike a typical "detection-only" walkthrough, this project follows the **complete Incident Response (IR) lifecycle**, including analyst decision-making and false positive analysis — the parts of SOC work that are usually left out of beginner projects.

    ## Objective
    To detect, investigate, and report on a brute force attack scenario the way a real SOC L1 Analyst would — including reasoning through false positives and documenting decisions at each stage.

    ## Tools & Environment
    - **SIEM:** Splunk Enterprise (local install)
    - **Dataset:** Boss of the SOC (BOTS) v1
    - **Language:** Splunk Search Processing Language (SPL)
    - **OS:** Windows

    ## Skills Demonstrated
    - SPL query writing (search, stats, timechart, correlation)
    - Log analysis (authentication logs)
    - Incident Response lifecycle (Detection → Investigation → Reporting → Lessons Learned)
    - False positive identification and reasoning
    - Security documentation / incident reporting

    ## Project Structure

    | Folder | Description |
    |---|---|
    | `01-detection/` | SPL queries used to detect suspicious login activity, with screenshots |
    | `02-investigation/` | Attack timeline, correlation analysis, and analyst decision log |
    | `03-incident-report/` | Formal incident report (severity, impact, root cause, response) |
    | `04-lessons-learned/` | Recommended detection rule improvements based on findings |

    ## Key Findings
    *(To be filled in after investigation is complete)*

    ## Author
    Nitin — Aspiring SOC L1 Analyst | IBM Cybersecurity Certified
