# CBT721
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. 
Due to amazing work by Alison Zhang and Jake Choi repos are no longer deleted.

```
//***FILE 721 is from Shirley Huhtanen and contains an extremely    *   FILE 721
//*           interesting and potentially useful system to capture  *   FILE 721
//*           change history for members of libraries.  Details of  *   FILE 721
//*           this package follow, below:                           *   FILE 721
//*                                                                 *   FILE 721
//*  ChangeWiz  (c) 2005                                            *   FILE 721
//*                                                                 *   FILE 721
//*  Renaissance Data Systems Inc.                                  *   FILE 721
//*  Shirley Huhtanen                                               *   FILE 721
//*  3325 Lorna Rd 2-325                                            *   FILE 721
//*  Birmingham, AL  35216                                          *   FILE 721
//*  (205) 999-9012                                                 *   FILE 721
//*  email: shirleywho@aol.com                                      *   FILE 721
//*                                                                 *   FILE 721
//*  This library is a self-contained unit and should contain all   *   FILE 721
//*  of the elements needed to create any or all of 3 different     *   FILE 721
//*  Change History capture systems.                                *   FILE 721
//*                                                                 *   FILE 721
//*  Why this system was created.                                   *   FILE 721
//*                                                                 *   FILE 721
//*  Some source management applications only have information      *   FILE 721
//*  about the last change made to a member.  Some can show         *   FILE 721
//*  historical information about all changes to a member, but      *   FILE 721
//*  only for one member at a time.  For members in PDS libraries   *   FILE 721
//*  that are not managed by a source management system, only       *   FILE 721
//*  information about the current version of a member is           *   FILE 721
//*  available.  Also, these systems may not identify the date a    *   FILE 721
//*  member was moved to production.  A member may be edited on     *   FILE 721
//*  one day and moved to production weeks or months later.         *   FILE 721
//*                                                                 *   FILE 721
//*  Here are 3 different systems for Change History depending on   *   FILE 721
//*  the type of source being tracked. A system for Endevor could   *   FILE 721
//*  be created easily using the same kind of methodology.  All of  *   FILE 721
//*  these systems create and maintain a history file that has one  *   FILE 721
//*  record for each time a member is changed, added or deleted.    *   FILE 721
//*                                                                 *   FILE 721
//*  The following information is captured:  element name,          *   FILE 721
//*  library, edit date/time, promote date/time, User id, change    *   FILE 721
//*  code/move request, level, number of lines.                     *   FILE 721
//*                                                                 *   FILE 721
//*  Here are some ways this information can be used.               *   FILE 721
//*                                                                 *   FILE 721
//*     1.  Create a summary report of changes made to all          *   FILE 721
//*           production members within a particular time period.   *   FILE 721
//*     2.  A daily report can be created that shows all members    *   FILE 721
//*           moved to production on that day.                      *   FILE 721
//*     3.  Identify all members changed during any time period.    *   FILE 721
//*     4.  For Sorbanes-Oxley reporting, this system provides an   *   FILE 721
//*           audit trail of changes to all production members      *   FILE 721
//*     5.  Identify members changed frequently.  Systems           *   FILE 721
//*           using these should probably be rewritten or           *   FILE 721
//*           redesigned.                                           *   FILE 721
//*     6.  Create summary reports of the number of                 *   FILE 721
//*           changes made by each programmer during a time         *   FILE 721
//*           period.                                               *   FILE 721
//*                                                                 *   FILE 721
//*   1.  PDS change history                                        *   FILE 721
//*       This system is fully documented in members $$PDS*.        *   FILE 721
//*       Create a change history file for PDS libraries that are   *   FILE 721
//*       not managed by a change management system.                *   FILE 721
//*                                                                 *   FILE 721
//*   2.  SCLM change history                                       *   FILE 721
//*       This system is fully documented in members $$SCLM*.       *   FILE 721
//*       Create a change history file for libraries that are       *   FILE 721
//*       managed by the SCLM change mgmt system.                   *   FILE 721
//*                                                                 *   FILE 721
//*   3.  Panvalet change history                                   *   FILE 721
//*       This system is fully documented in member $$PAN.  Create  *   FILE 721
//*       a change history file for libraries that are managed by   *   FILE 721
//*       the Panvalet source mgmt system.                          *   FILE 721
//*                                                                 *   FILE 721
//*    Naming standards for members in this library.                *   FILE 721
//*                                                                 *   FILE 721
//*    $*****   documentation for these members.                    *   FILE 721
//*    JXCPP*   Cobol copybooks. Procedure div                      *   FILE 721
//*    JXCPR*   Cobol copybooks. Record layouts                     *   FILE 721
//*    JXCPW*   Cobol copybooks. Working storage.                   *   FILE 721
//*    JXC###** where # is numeric.  These are Cobol programs.      *   FILE 721
//*    JXCU###  where # is numeric.  These are Cobol programs.      *   FILE 721
//*    JXD*     JCL for production daily jobs                       *   FILE 721
//*    JXE*     Easytrieve programs                                 *   FILE 721
//*    JXI*     JCL include members (except JXIN*)                  *   FILE 721
//*    JXIN*    Cobol copybooks. Custom changes for each client.    *   FILE 721
//*    JXM*     JCL for production monthly jobs                     *   FILE 721
//*    JXP*     Procs                                               *   FILE 721
//*    JXR*     JCL for production request jobs                     *   FILE 721
//*    JXSD*    Card members. Data cards. May need changes.         *   FILE 721
//*    JXSR*    Card members. Sort cards. No custom changes.        *   FILE 721
//*    JXW*     JCL for production weekly jobs                      *   FILE 721
//*    JZ*      Easytrieve record layouts                           *   FILE 721
//*                                                                 *   FILE 721
//*    All other members are test JCL or request JCL for special    *   FILE 721
//*    reports.                                                     *   FILE 721
//*                                                                 *   FILE 721
//*   This material is provided as-is.  It works on the z/OS        *   FILE 721
//*   system it was developed on, but may not work on all systems.  *   FILE 721
//*   No warranty is made to the accuracy of the programs or        *   FILE 721
//*   related material and no responsibility is assumed for any     *   FILE 721
//*   modifications made to these applications by a third party.    *   FILE 721
//*   The documentation included is intended to aid in setting up   *   FILE 721
//*   the systems.  Validating the results is the responsibility    *   FILE 721
//*   of the party using this material.                             *   FILE 721
//*                                                                 *   FILE 721
//*   These programs are distributed on the CBT Tape with the       *   FILE 721
//*   proviso that they may be freely distributed to any other      *   FILE 721
//*   party on condition that no inducement beyond reasonable       *   FILE 721
//*   handling costs is offered or accepted by either side for      *   FILE 721
//*   such distribution or your normal consulting costs for         *   FILE 721
//*   installation and support.                                     *   FILE 721
//*                                                                 *   FILE 721
//*   The use of any part of these programs or copybooks in         *   FILE 721
//*   another program or application does not make that program or  *   FILE 721
//*   application fall under this license.                          *   FILE 721
//*                                                                 *   FILE 721
//*   Modified versions of these programs and systems should *NOT*  *   FILE 721
//*   be distributed by a third party.  It will be chaos if         *   FILE 721
//*   multiple versions of these programs start floating around.    *   FILE 721
//*                                                                 *   FILE 721
//*   Because these systems interface with other vendor's           *   FILE 721
//*   products, changes to their products could cause these         *   FILE 721
//*   programs and systems to not work any more.  All of the        *   FILE 721
//*   programs have built-in debugging to aid in analysis.  Let me  *   FILE 721
//*   know if you've had to make changes for a specific version of  *   FILE 721
//*   a vendor's software and it can be incorporated here.          *   FILE 721
//*                                                                 *   FILE 721
//*   This documentation has not had a work-out by being used to    *   FILE 721
//*   install the system on another machine.  Please contact me if  *   FILE 721
//*   you have any questions regarding any part of these systems.   *   FILE 721
//*                                                                 *   FILE 721
//*   SCLM and IEHLIST are products of                              *   FILE 721
//*        International Business Machines (IBM)                    *   FILE 721
//*   Panvalet, Endevor and Easytrieve are products of              *   FILE 721
//*        Computer Associates                                      *   FILE 721
//*                                                                 *   FILE 721
```
