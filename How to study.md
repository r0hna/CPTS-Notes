# Addressing the Confidence Gap & What to Focus On

The CPTS exam is less about finding "gotchas" and more about demonstrating a solid, repeatable penetration testing methodology across various domains: web, internal network, external, and Active Directory. After a break, the main areas that tend to get rusty are:

* **Methodology Flow:** The seamless transition from enumeration to exploitation, pivoting, and post-exploitation.
* **Tool Recall & Syntax:** Remembering the specific commands, flags, and common tools for various attack vectors.
* **Active Directory Nuances:** AD attacks often involve multiple steps and reliance on specific tools and techniques that can be forgotten.
* **Report Writing Structure:** While not a "technical" skill for the exam itself, the report is crucial for passing, and a break can impact your ability to quickly recall and organize findings.
* **Pivoting and Tunneling:** Setting up reliable tunnels (e.g., `chisel`, `ligolo-ng`, SSH tunneling) and managing network routes is critical and often forgotten without consistent practice.

## Your 10-Day Plan: "Strategic Refresh & Targeted Practice"

Instead of trying to "learn new things" in 10 days, your focus should be on **deep revision, solidifying your methodology, and reinforcing weak areas through targeted practice.**

### Days 1-3: Methodical Review & Note Enhancement

* **Review Your Existing Notes:** This is paramount. Go through *all* your CPTS notes (from Hack The Box Academy, "unofficial CTF", and any personal notes). Don't just read them; actively process them.
* **Methodology Focus:** As you review, pay close attention to the *flow* of a penetration test. For each type of target (Windows host, Linux host, Web Application, Active Directory domain), mentally walk through your steps:
    * Initial Recon & Enumeration (Nmap, Nessus/OpenVAS output interpretation, web enumeration - GoBuster, Dirb, Nikto, etc.)
    * Vulnerability Identification (CVEs, misconfigurations, logic flaws)
    * Exploitation (Public exploits, custom scripts, common attack vectors)
    * Privilege Escalation (Windows & Linux - look for common vectors like kernel exploits, SUID/GUID binaries, misconfigured services, weak permissions, always PEASS, WinPEAS, LinPEAS)
    * Pivoting & Lateral Movement (SSH tunneling, `chisel`, `ligolo-ng`, RDP, SMB, Pass-the-Hash, Pass-the-Ticket)
    * Post-Exploitation (Credential dumping, persistent access, data exfiltration)
    * Active Directory Specifics: This is critical. Review Kerberoasting, AS-REP Roasting, BloodHound/Sharphound, unconstrained delegation, constrained delegation, group policy enumeration, DC Sync, etc.
* **Consolidate and Refine Cheat Sheets:** Based on your review, build concise cheat sheets for:
    * Common Linux/Windows privilege escalation commands.
    * Active Directory enumeration and attack commands (PowerView, Rubeus, Impacket scripts).
    * Web application attack payloads (SQLi, XSS, Command Injection, LFI/RFI).
    * Pivoting and tunneling commands.
    * Reverse shell one-liners.
* **Tool Syntax Drills:** For tools you use frequently (e.g., `nmap`, `gobuster`, `responder`, `impacket` scripts, `crackmapexec`, `metasploit` modules), quickly type out common commands from memory, then check your notes. This reinforces muscle memory.

### Days 4-7: Targeted Practice - Pro Labs & Specific Modules

This is where you move from passive review to active application.

* **Hack The Box Pro Labs:** If you have access, **Dante** and **Offshore** are excellent for CPTS preparation as they simulate enterprise-level networks with multiple machines, pivoting, and Active Directory components.
    * **Prioritize areas you feel weakest in.** If your AD skills are rusty, focus on the AD sections of these labs. If web pivoting is a concern, seek that out.
    * **Approach them as if they were the exam:** No hints, no walkthroughs (unless absolutely stuck after a significant effort). Take detailed notes as you go, practicing your reporting structure.
* **Revisit Specific HTB Academy Modules/Skills Assessments:** Instead of re-doing the entire path, pick out modules from the "Penetration Tester" job role path that cover your weaker areas identified in Days 1-3.
    * **Active Directory Enumeration and Attacks:** This is a huge component of the CPTS. Make sure you're rock solid here.
    * **Windows & Linux Privilege Escalation:** Re-run the exercises, focusing on understanding the *why* behind each technique, not just the *how*.
    * **Web Application Penetration Testing:** Revisit modules on common web vulnerabilities like SQL injection, command injection, LFI/RFI, and deserialization.
    * **Pivoting & Lateral Movement:** Practice setting up various tunnels and moving between subnets.
* **"Hard" Difficulty Academy Machines (if time permits):** If you still have time and feel confident, select a few "Hard" rated machines from the HTB Academy that align with CPTS topics (Windows, Linux, AD, Web). Focus on your methodology.

### Days 8-9: Mock Exam Simulation & Report Outline

* **Mini-Exam or Complex Machine:** If you can afford it, consider purchasing access to a Hack The Box machine (or even a small Pro Lab segment if available) that you haven't done, and treat it as a mini-exam.
    * **Time yourself.**
    * **Take meticulous notes for reporting.**
    * **Practice building your report outline as you go.** This is critical for the actual exam.
* **Report Writing Practice:** Even if you don't do a full mock exam, spend a solid half-day practicing outlining a penetration test report.
    * **Review the CPTS Report Template:** Hack The Box provides a template. Familiarize yourself with its structure, sections, and what kind of information they expect for each finding (description, impact, remediation, evidence, steps to reproduce).
    * **Practice articulating findings:** For a few common vulnerabilities (e.g., unquoted service path, weak file permissions, SQLi), write out a concise vulnerability description, impact, and remediation steps. This will make report writing under pressure much faster.
    * **Screenshot Best Practices:** Ensure your screenshots are clear, highlight the relevant information, and are properly captioned.

### Day 10: Final Light Review & Rest

* **Light Review:** Go over your cheat sheets, methodology outlines, and high-level concepts. Avoid deep dives into new topics.
* **Rest:** Seriously, this is as important as studying. A well-rested mind performs far better under pressure. Get good sleep, eat well, and do something relaxing.

## Crucial Reminders for the CPTS Exam:

* **Methodology is Key:** Don't just jump into random attacks. Follow a systematic methodology for enumeration, vulnerability identification, exploitation, and post-exploitation.
* **Documentation is Paramount:** Take *detailed* notes during the exam. Every command, every finding, every piece of evidence. This will save you immense time during the report writing phase. Use a tool like CherryTree, Obsidian, or even a well-structured text file.
* **Pivoting & Tunnelling:** Be absolutely comfortable with setting up and maintaining network tunnels. This is where many struggle.
* **Active Directory is a Major Focus:** Expect a significant portion of the exam to involve Active Directory.
* **Don't Get Stuck on One Thing:** If you're spinning your wheels on a specific vulnerability for more than an hour or two, take a break from it and move to another target or re-enumerate. You can always come back to it. The network is large, and there are often multiple paths to objectives.
* **Read the Exam Instructions Carefully:** Before you start the timer, read every instruction, the scope, and the objectives thoroughly.
* **Manage Your Time:** 10 days is a generous amount of time, but it can also lead to procrastination if not managed well. Break down the exam into manageable chunks for each day.
* **The Report:** Allocate sufficient time (at least 2-3 full days) for the report writing. It's not an afterthought; it's a critical component of passing.