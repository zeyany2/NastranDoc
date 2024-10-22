**NASA SP-222(08)** 

**VOLUME II** 

**NASTRAN@ USER’S MANUAL JUNE 1986** 

**runm**

**NASA SP-222(08)** 

**Volume 11** 

**NASTRAN USER’S MANUAL** 

**June 1986**  
**Computer Services Annex, University of Georgia, Athens, Georgia 30602 ‘** ●**For sale from Computer Software Management and Information Center (COSMIC)**   
`COSMIC`   
`The University of Georgia`   
`Computer Services Annex`   
`Athens, GA 30602`   
`(404) 542-3265` 

`NASTWN USER MANUAL UPDATE NOTE` 

`The NASTRAN User Manual is scheduled for review each year to determine whether updates are required. To add your name to the database to receive notification when updates are available, you will need to complete this form and return to COSMIC . This will be the only mailing list for keeping users informed about the manual updates.` 

`Your Name:` 

`Company:` 

`Mailing Address:` 

`City:` 

**State: Zip:** 

`June, 1986` 

`Fold, staple, and`   
`return this form`   
`as a self-mailer.`

II 

BUSINESS REPLY MAIL 

**1 FIRSTCLASS PERMIT NO, 559 ATHENS, CiEORGIA I** 

**F’OSTAGE WILL BE PAID BY ADDRESSES** 

**COSMIC**   
`The University of Georgia`   
`Computer Services Annex`   
`Athens, GA 30602`   
**NO POSTAGE NECESSARY**   
**IFMAILED**   
**IN THE**   
**UNITED STATES**

**INTRODUCTION** 

**The User’s Manual is one of four manuals that constitute the documentation for NASTRAN, the other three being the Theoretical Manual, the Programmer’s Manual and the Demonstration Problem Manual. Although the User’s Manual contains all of the information that is directly associated with the solution of problems with NASTRAN, the user will find it desirable to refer to the other manuals for assistance in the solution of specific user problems.** 

**The Theoretical Manual gives an excellent introduction to NASTRAN and presents developments of the analytical and numerical procedures that underlie the program. The User’s Manual is instructive and encyclopedic in nature, but is restricted to those items related to the use of NASTRAN that are generally independent of the computing system being used. Computer-dependent topics and information that is required for the maintenance and modification of the program are treated in the Programmer’s Manual. The Programmer’s Manual also provides a complete description of the program, including the mathematical equations implemented in the code. The Demonstration Problem Manual presents a discussion of the sample problems delivered w\!th NASTRAN, thereby illustrating the formulation of the different types of prob’\!emsthat can b\~ solved with NASH?PN.** 

**In addition to the four manual\~ described above, there is also a NASTRAN User’s Guide that serves as a handbook for users. It describes all of the NASTRAN features and options and illustrates them by examples. Other excellent sources for NASTRAN-related topics are the proceedings of the NASTRAN Users’ Colloquia (held normally every year) which provide a large body of information based on user experiences with NASTRAN.** 

**The User’s Manual has recently been completely revised and updated. With a view to facilitate easier updating of the manual in the future to keep up with newer releases of NASTRAN, it has now been divided into two volumes.** 

**Volume I consists of seven sections dIldcontains all of the material that was in the old single volume, except Section 3\. This section has been re-arranged into four sections and forms Volume II. In order to avoid confusion, Section 3 of Volume I does not contain anything other than a reference to the new Volume II. Also, it should be noted here that, unless explicitly indicated ——.. otherwise, —. all —-—..references — ....—.--...to....sections ..——.. in each volume refer only to sections in that volume, —.——.—--- —— ..——. .**   
**NASTRAN uses the finite element approach to structural modeling, wherein the distributed physical properties of a structure are represented by a finite number of structural elements which are interconnected at a finite number of grid points, to which loads are applied and for which displacements are’calculated. The procedures for defining and loading a structural model are** 

**i (05/30/86)**

**described in Volume I, Section 1\. This section contains a functional reference for every card that is used for structural modeling.** 

**The NASTRAN Data Deck, including the details for each of the data cards, is described in Volume I, Section 2\. This section also discusses the NASTRAN control cards that are associated with the use of the program.** 

**As mentioned earlier, Volume I, Section 3 does not contain anything other than a reference to Volume II.** 

**The procedures for using the NASTRAN plotting capability are described in Volume I, Section 4\. Both deformed and undeformed plots of the structural model are available. Response curves are also available for static, transient response, frequency response, modal flutter and modal aeroelastic response analyses.** 

**NASTRAN contains problem solution sequences, called rigid formats, Each of these rigid formats is associated with the solution of problems for a particular type of static or dynamic** 

**analysis. in addition to the rigid format procedures, the user may choose to write his own Direct Abstraction Program (DMAP), This procedure permits the user to execute a series of matrix operations of his choice along with any utility modules or executive operations that he may need. The rules governing the creation of DMAP programs are described in Volume I, Section 5\.** 

**The NASTRAN diagnostic messages are documented and explained in Volume I, Section 6\. The NASTRAN Dictionary, in Volume I, Section 7, contains descriptions of mnemonics, acronyms, phrases, and other commonly used NASTRAN terms.** 

**Volume II, Section 1 contains a general description of rigid format procedures. Specific instructions and information for the use of each rigid format are given in Volume II, Sections 2, 3 and 4, which deal with the rigid formats associated with the DISPLACEMENT, HEAT and AERO approaches, respectively.** 

**There is a limited number of sample problems included in the User’s Manual. However, a more comprehensive set of demonstration problems, at least one for each of the rigid formats, is described in the NASTRAN Demonstration Problem Manual, The data decks are available on tape for each of the computer systems on which NASTRAN has been implemented. Samples of the printer output and of structure plots and response plots can be obtained by executing these demonstration problems. The printer output for these problems is also available on microfiche.** 

**ii (05/30/86)**   
**Matrix** 

@ 

**I**  
**TABLE OF CONTENTS** 

**Section Page No. 1\. RIGID FORMATS** 

**1.1 GENERAL DESCRIPTION OF RIGID FORMATS ........................................ 1.1-1 1.1.1 Input File Processor ................................................ 1.1-2 1.1,2 Functional Modules and Supporting DMAP Operations ................... 1.1-4 1.1.3 Checkpoint/Restart Procedures ....................................... 1.1-5 1.1.4 Types of Restarts ................................................... 1.1-7** 

**1.1.4.1 Unmodified Restart ......................................... 1.1-8 1.1.4.2 Modified Restart ........................................... 1.1-8 1.1.4,3 Modified Restart with Rigid Format Switch .................. 1.1-10** 

**1.1.5 Use of DMAPALTERs in Restarts ...................................... 1.1-10 1.1.6 Rigid Format Output ................................................. 1.1-11 1.1.7 Rigid Format Data Base .............................................. 1.1-13** 

**1.1.7.1 Design of the Data Base .................................... 1.1-13 1.1.7.2 Implementation of the Data Base .......,.’.................. 1.1-17 1.1.7,3 Usage of the Data Base ..................................... 1.1-17 1.1.7.4 Development of User Rigid Formats .......................... 1.1-18 1.1.7.5 Usage of User-Developed Rigid Formats ...................... 1.1-20** 

**2\. DISPLACEMENT RIGID FORMATS** 

**2.1 STATIC ANALYSIS ..............0............,................................. 2.1-1** 

**2.1.1** 

**2.1.2** 

**2.1.3** 

**2.1.4** 

**2.1,5** 

**2.1.6** 

**2.1.7** 

**2.2 STATIC 2.2.1** 

**2.2.2** 

**2.2.3** 

**2.2.4**   
**DMAP Sequence for Static Analysis ................................... 2.1-1 Description of Important DMAP Operations for Static Analysis ........ 2.1-9 Output for Static Analysis .......................................... 2.1-16 Case Control Deck for Static Analysis ............................... 2.1-16 Parameters for Static Analysis .................4.................... 2.1-16 Automatic AI.TERsfor Automated Multi-stage Substructuring ........... 2.1-19 Rigid Format Error Messages from Static Analysis .................... 2.1-19** 

**ANALYSIS WITH INERTIA RELIEF .......................0....0............ 2.2-1 DMAP Sequence for Static Analysis with Inertia Relief ............... 2.2-1** 

**Description of Important DMAP Operations for Static Analysis with Inertia Relief ...............,....,,.,......................... 2.2-6** 

**Output for Static Analysis with Inertia Relief ...................... 2.2-11 Case Control Deck for Static Analysis with Inertia Relief ........... 2.2-11 iii (05/30/86)**  
**TABLE OF CONTENTS (Continued)** 

**Section Page No. 2.2.5 Parameters for Static Analysis with Inertia Relief ......,........... 2.2-11 2.2.6 Automatic ALTERs for Automated Multi-stage Substructuring ........... 2.2-13** 

**2.2.7 Rigid Format Error Messages from Static Analysis**   
**with Inertia Relief .........................................,....... 2.2-13 2.3 NORMAL MODES ANALYSIS ....................................................... 2.3-1** 

**2.3.1 2.3.2 2.3.3 2.3.4 2.3.5 2,3.6 2.3.7 2.3.8 2.3.9**   
**DMAP Sequence for Normal Modes Analysis ............................. 2.3-1 Description of Important DMAP Operations for Normal Modes Analysis .. 2.3-6 Output for Normal Modes Analysis ............,......................O 2.3-11 Case Control Deck for Normal Modes Analysis ......,.................. 2.3-13 Parameters for Normal Modes Analysis ................,.........,...,, 2.3-14 Optional Diagnostic Output for FEER .......,,.....,.................. 2.3-15 The APPEND Feature ............................................,..... 2,3-17 Automatic ALTERs for Automated Multi-stage Substructuring ........... 2.3-18 Rigid Format Error Ples$agesfrom Normal Modes Analysis .............. 2.3-18** 

**2.4 STATIC ANALYSIS WITFIDIFFERENTIAL STIFFNESS .0...........,................... 2.4-1 2.4.1 DMAP Sequence for Static Analysis with**   
**Differential Stiffness ...................................** 

**2.4.2 Description of Important DMAP Operations for Static Analys with Differential Stiffness ............0..,.,............** 

**2.4.3 Output for Static Analysis with Differential Stiffness ... 2.4.4 Case Control Deck for Static Analysis with Differential St” 2.4.5 Parameters for Static Analysis with Differential Stiffness 2.4.6 Rigid Format Error Messaaes from Static Analysis with**   
. . . . . . . . . . **2.4-1** 

**s**   
**.......... 2.4-9 ..,....... 2.4-17 ffness.... 2.4-18 .......... 2.4-18** 

**Differential Stiffness .-............................................. 2.4-19 2.5 BUCKLING ANALYSIS .,.........,...................,........................... 2.5-1 2.5.1 DMAP Sequence for Buckling Analysis ................................. 2.5-1 2.5.2 Description of Important DMAP Operations for Buckling Analysis ...... 2.5-7 2.5.3 Output for Buckling Analysis ................,....0...............,.. 2.5-13 2.5.4 Case Control Deck for Buckling Analysis ............................. 2.5-13 2.5.5 Parameters for Buckling Analysis ......................0............, 2.5-14 2.5.6 Optional Diagnostic Output for FEER ........................,...,..,. 2.5-14 2.5.7 Rigid Format Error Messages from Buckling Analysis .........,........ 2.5-15 2.6 PIECEWISE LINEAR STATIC ANALYSIS ...........,................................ 2.6-1 2.6.1 DMAP Sequence for Piecewise Linear Static Analysis .................. 2.6-1 iv (05/30/86)**

●   
**TABLE OF CONTENTS (Continued** 

**Section** 

**2.6.2 Description of Important DMAP Operations for Piecewise Linear**   
**Page No.** 

**Static Analysis ,.............,...0.........,.....0....,............. 2.6-7 2.6.3 Output for Piecewise Linear Static Analysis ......................... 2.6-13 ?.6.4 Case Control Deck for Piecewise Linear Static Analysis .............. 2.6-13 2.6.5 Parameters for Piecewise Linear Static Analysis ..................... 2.6-13 2.6.6 Rigid Format Error Messages from Piecewise Linear Static Analysis ... 2.6-14 DIRECT COMPLEX EIGENVALUE ANALYSIS .,........................................ 2.7-1 2.7** 

**2.7.: DMAP Sequence for Direct Complex Eigenv.1**   
**reanalysis ................ 2.7-I** 

**?,7.2 Description of Important DMAP Operations Eigenvalue Analysis ....,....,..........** 

**2.7.3 output for Direct Complex Eigenvalue** ha’   
**for Direct Complex**   
**............................ 2.7-7 ysis ,.,.,..,..........,., .. 2.7-13** 

**2,7.4 Case Contro”lDeck for Direct Complex Eigenvalue Analysis ............ 2.7-15 2.7.5 Parameters for Direct Complex Eigenvalu: Al:alysis................... ?.7-1.6 2.7.6 Rigid Format Error Messages frpm \!\~irectComplex EigenYalue Analysis . ?.7-17 DIRECT FREQUENCY AND RANDOM RESp\~NSE ......................... ...\!.......... 2.8-1 2.8** 

**2.8.1 DMAP Sequence for Direct Frequency and Random Response .............. ?.G-l** 

**2.8.2 Description of Important DMAP Operations for Direct Frequency and Random Response ..........,....................-....... ............. 2.8-9** 

**2.8.3 Output for Direct,Frequency and Random Response ..................... 2.8-16 2.8.4 Case Contro”lDeck,for Direct Frequency and Random Response .......... 2.8-16 2.8.5 Parameters for Direct Frequency and Random Response ................. 2.8-17 2.8.6 Automatic ALTERs for Automated Multi-stage Substructuring ........... 2.8-18** 

**2.8.7 Rigid Format Error Messages from Direct Frequency**   
**and Random Response ..............................0.............,.... 2.8-18 DIRECT TRANSIENT RESPONSE .......,........................................... 2.9-1 2.9** 

**2.9.1 2.9.2** 

**2.9.3 2.9.4 2.9.5 2.9.6 2.9.7**   
**DMAP Sequence for Direct Transient Response ......................... 2.9-1** 

**Description of Important DMAP Operations for Direct**   
**Transient Response .............................**.o....\*o.......\*.””. 2“9-8 **Output for Direct Transient Response ................................ 2,9-15 Case Control Deck for Direct Transient Response ...................“. 2.9-:.5 Parameters for Direct Transient Response ............................ 2.9-16 The CONTINUE Feature ........0..,.....,.........,.................... 2.9-17 Automatic ALTERs for Automated Multi-staSe Substructuring ........... 2.9-18** 

**2.9,8**   
**Rigid Format Error Messages from Direct V (05/30/86)**   
**Transient Response .......... 2.9-18**

**TABLE OF CONTENTS (Continued)** 

. .   
**\>ecrlon\~ 2.10 MODAL COMPLEX EIGENVALUE ANALYSIS ........................................... 2.10-1** 

**2.10.1 2.10.2** 

**2.10.3 2.10.4 2.10.5 2.10.6 2.10.7 2.10.8**   
**DMAP Sequence for Modal Complex Eigenvalue Analysis ................. 2.10-1** 

**Description of Important DMAP Operations for Modal Complex Eigenvalue Analysis ...........,............................,........ 2.10-7** 

**Output for Modal Complex Eigenvalue Analysis ...............,........ 2.10-13 Case Control Deck for Modal Complex Eigenvalue Analysis .........,... 2.10-13 Parameters for Modal Complex Eigenvalue Analysis .................... 2,10-13 Optional Diagnostic Output for FEER ......,........,..,.,............ 2.10-14 The APPEND Feature .................0..................,............, 2.10-15 Rigid Format Error Messages from Modal Complex Eigenvalue Analysis ,. 2.10-15** 

**2.11 MODAL FREQUENCY AND RANDOM RESPONSE ...................,“.e....,..........,.. 2.11-1** 

**2.11.1 2.11.2** 

**2.11.3 2.11.4 2.11.5 2.11.6 2.11.7 2.11.8**   
**DMAP Sequence for Modal Frequency and Random Response ............... 2.11-1 Description of Important DMAP Operations for Modal Frequency and**   
I  
**Random Response .....,,............,.,.................,.,,.......,.. 2.11-9 Output for Modal Frequency and Random Response ...........,.......... 2.11-17 Case Control Deck for Modal Frequency and Random Response ........... 2.11-17 Parameters for Modal Frequency and Random Response ........,....,.... 2,11-17 Optional Diagnostic Output for FEER ..........,.,....,....,.......... 2,11-18 The APPEND Feature .........................,.......,.......,,.....,. 2.11-19** 

**Rigid Format Error Messages from Modal Frequency**   
**and Random Response ...,.,,.............,.....................,....., 2.11-19** 

**2.12 MODAL TRANSIENT RESPONSE .....................0..,.......,.,...,.,,..,,....,. 2,12-1** 

**2.12.1 2.12,2** 

**2.12.3 2.12.4 2.12.5 2.12.6 2.12.7 2.12.8 2.12.9**   
**DMAP Sequence for Modal Transient Response ............,.....,.,..,.. 2.12-1** 

**Description of Important DMAP Operations for Modal**   
**Transient Response ...................,....,...,.....,............... 2.12-8 Output for Modal Transient Response ...........,,...,......,.,.....,, 2.12-15 Case Control Deck for Modal Transient Response ......,......,......,. 2.12-15 Parameters for Modal Transient Response .....,.............,.....,... 2,12-15 Optional Diagnostic Output for FEER ......,....,,..,...,,...,........ 2,12’-17 The APPEND Feature ..,................,.......,.....,.....,.......... 2.12-17 The CONTINUE Feature ....,......................,......,..,......,,.. 2,12-17 Rigid Format Error Messages from Modal Transient Response ........... ?\!.12-1.7** 

**2.13 NORMAL MODES WITH DIFFERENTIAL STIFFNESS ., 2.13.1 DMAP Sequence for Normal Modes with vi (05/30/86)**   
**?,\~\~-1 .....................,. ,,, ......\> Differential Stiffue$s ..,, ..,. “\~,13-\!** 

**TABLE OF CONTENTS (Continued)** 

**Section**   
**Page No.** 

**2.13.2** 

**2,13.3 2.13.4 2.13.5 2.13.6 2.13.7 2.1.3**   
**Description of Important DMAP Operations for Normal Modes with Differential Stiffness ............,.............0................... 2.13-8** 

**Output for Normal Modes with Differential Stiffness ................. 2.13-16 Case Control Deck for Normal Modes with Differential Stiffness ...... 2.13-16 Parameters for Normal Modes with Differential Stiffness ............. 2.13-17 Optional Diagnostic Output for FEER ................................. 2.13-18 The APPEND Feature ......................,..........................c 2.13-18** 

**Rigid Format Error Messages from Normal Modes with**   
**Differential Stiffness .............................................. 2.13-18** 

**2.14 STAT 2.14**   
**ANALYSIS USING CYCLIC SYMMETRY ..............,........................ 2.14-1 c** 

`1`   
**DMAP Sequence for Static Analysis Using Cyclic Symmetry ............. 2.14-1** 

**2.14.2** 

**2.14.3 2.14.4 2.14,5 2.14.6**   
**Description of Important DMAP Operations for Static Analysis Using Cyclic Symmetry ,.......0...................,........................ 2.14-7** 

**Output for Static Analysis Using Cyclic Symmetry ......,............. 2.14-12 Case Control Deck for Static Analysis Using Cyclic’Symmetry .........2.14-12 Parameters for Static Analysis Using Cyclic Symmetry ................ 2.14-12** 

**Rigid Format Error Messages from Static Analysis Using**   
**CyiilicSymmetry ..........................................+.......... 2.14-14** 

**2.15 NORMAL MODES ANALYSIS USING CYCLIC SYMMETRY ................................. 2.15-1** 

**2.15.1 2.15.2** 

**2.15.3 2.15.4 2.15.5 2.15.6 2.15.7 2.15.8**   
**DMAP Sequence for Normal Modes Analysis Using Cyclic Symmetry ....... 2.15-1** 

**Description of Important DMAP Operations for Normal Modes Analysis Using Cyclic Symmetry ...............,............................... 2.15-6** 

**Output for Normal Modes Analysis Using Cyclic Symmetry .............. 2.15-10 Case Control Deck for Normal Modes Analysis Using Cyclic Symnetry ... 2.15-10 Parameters for Normal Modes Analysis Using Cyclic Symmetry .......... 2.15-10 Optional Diagnostic Output for FEER ................................. 2.15-12 The APPEND Feature .....0..........0................................. 2.15-12** 

**Rigid Format Error Messages from Normal Modes Analysis Using \--- .- Cyclic Symmetry .,.................0.........0....................... Z.15-lZ** 

**?.1.6 (STATIC AEROTHERMOELASTIC DESIGN/ANALYSIS OF AXIAL-FLOW COMPRESSORS .......... 2.16-1** 

**‘2.16.1 ?,16.2 2.16.3**   
**DMAP Sequence for Static Aerothermoelastic Design/Analysis of Axial-Flow Compressors o............................................. 2.16-1** 

**Description of Important DMAP Operations for Static**   
**Aerothermoelastic Design/Analysis of Axial-Flow Compressors ......... 2.16-10** 

**Output for Static Aerothermoelastic Design/Analysis of Axial-Flow Compressors .........................................................2.16-19** 

**vii (05/30/86)**  
**TABLE OF CONTENTS (Continued)** 

**Section**   
**Page No,** 

**2.16.4 2.16.5 2.16.6**   
**Case Control Deck for Static Aerothem,\~elastic Design/Analysis of Axial-Flow Compressors .............................................. 2.16-20** 

**Parameters for Static Aerothermoelastic Design/Analysis of Axial Flow Compressors ......,..................\#.......................... 2.16-20** 

**Rigid Format Error Messages from Static Aerothermoelastic Design/ Analysis of Axial-Flow Compressors ...,.............................. 2.16-22** 

**3\. HEAT RIGID FORMATS** 

**3.1 STATIC HEAT TRANSFER ANALYSIS ...,..,...................,.................... 3.1-1** 

**3.1,1 3.1.2** 

**3.1.3**   
**DMAP Sequence for Static Heat Transfer Analysis ..................... 3.I-1** 

**Description of Important DMAP Operations for Static Heat**   
**Transfer Analysis ...................................,............... 3.1-6 Output for Static Heat Transfer Analysis ......................,...,. 3.1-11** 

**3.1.4 3.1.5**   
**Case Control Deck for Static Heat Transfer Analysis ..... Parameters for Static Heat Transfer Analysis ,.....,0....**   
**........... 3.1-11 ........... 3.1-11** 

**3.1.6**   
**Rigid Format Error Messages from Static Heat Transfer Aria’ ysis ...... 3.1-12** 

**3,2 NONLINEAR STATIC HEAT TRANSFER ANALYSIS ....,.,.....,.............**   
. . . . . . . . . . . **3.2-1** 

**3.2.1 DMAP Sequence for Nonlinear Static Heat Transfer Analysis ........... 3.2-1** 

**3.2.2 Description of Important DMAP Operations for Nonlinear Static Heat Transfer Analysis ...........,............,.......................... 3.2-5** 

**3.2.3 Output for Nonlinear Static Heat Transfer Analysis .................. 3.2-8 3.2.4 Case Control Deck for Nonlinear Static Heat Transfer Analysis ....... 3.2-8 3.2.5 Parameters for Nonlinear Static Hiat Transfer Analysis .............. 3.2-8** 

**3.2.6 Rigid Format Error Messages from Nonlinear Static Heat**   
**Transfer Analysis ............................,..,................,.. 3.2-9 3.3 TRANSIENT HEAT TRANSFER ANALYSIS ............................................ 3,3-1 3.3.1 DMAP Sequence for Transient Heat Transfer Analysis .................. 3.3-1** 

**3.3.2 Description of Important DMAP Operations for Transient Heat Transfer Analysis .........,...............,...................,........,,..,. 3.3-7** 

**3,3.3 Output for Transient Heat Transfer Analysis ......................... 3.3-13 3.3.4 Case Control Deck for Transient Heat Transfer Analysis .............. 3.3-13** 

**3.3.5 Parameters for Transient Heat Transfer 3.3.6 Rigid Format Error Messages from Trans 4\. AERO RIGID FORMATS** 

**4,1 BLADE CYCLIC MODAL FLUTTER ANALYSIS ..........**   
**Analysis ..................... 3.3-14 ent Heat Transfer Analysis ... 3,3-14** 

. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . **4.1-1** 

**4.1.1 DMAP Sequence for Blade Cyclic Modal Flutter Analysis ............... 4.1-1 viii (05/30/86)**

**Section** 

**4.1.2** 

**4.1.3** 

**4.1.4** 

**4.1.5** 

**4.1.6** 

**4.1.7** 

**4.1.8**   
**TABLE OF CONTENTS (Continued)** 

**Page No.** 

**Description of Important DMAP Operations for Blade Cyclic Modal Flutter Analysis .................................................... 4.1-9** 

**Output for Blade Cyclic Modal Flutter Analysis ...................... 4.1-17 Case Control Deck for Blade Cyclic Modal Flutter Analysis ........... 4.1-17 Parameters for Blade Cyclic Modal Flutter Analysis .................. 4.1-18 Optional Diagnostic Output for FEER ................................. 4.1-20 The APPEND Feature .............,.................................... 4.1-20** 

**Rigid Format Error Messages from Blade Cyclic Modal Flutter \---- Analysis ................0........................................... 4.1-ZU** 

**4.2 MODAL FLUTTER ANALYSIS ...................................................... 4.2-1** 

**4.2.1 4.2.2 4.2.3 4.2.4 4.2.5 4.2.6 4.2.7**   
**DMAP Sequence for Modal Flutter Analysis ............................ 4.2-1 Description of Important DMAP Operations for Modal Flutter Analysis . 4.2-8 Output for Modal Flutter Analysis ................................... 4.2-16 Case Control Deck for Modal Flutter Analysis ........................ 4.2-17 Parameters for Modal Flutter Analysis ............................... 4.2-17 Optional Diagnostic Output for FEER ................................. 4.2-18 The APPEND Feature .................................................. 4.2-18** 

**4.2.8 Rigid Format Error Messages from Modal Flutter Analysis ............. 4.2-18 4.3 MODAL AEROELASTIC RESPONSE ...................:.............................. 4.3-1 4.3.1 DMAP Sequence for Modal Aeroelastic Response ........................ 4.3-1** 

**4.3.2 Description of Important DMAP Operations for Modal Aeroelastic Response ............................................................ 4.3-8** 

**4.3.3 Output for Modal Aeroelastic Response ............................... 4.3-16 4.3.4 Case Control Deck for Modal Aeroelastic Response .................... 4.3-17 4.3.5 Parameters for Modal Aeroelastic Response ........................... 4.3-17 4.3.6 Optional Diagnostic Output for FEER ................................. 4.3-19 4.3.7 The APPEND Feature .................................................. 4.3-19 4.3.8 Rigid Format Error Messages from Modal Aeroelastic Response ......... 4.3-19** 

**ix (05/30/86)**  
**1\. RIGID FORMATS** 

**1.1 GENERAL DESCRIPTION OF RIGID FORMATS** 

**The most general way of using NASTRAN is with a user-written Direct Matrix Abstraction Program (DMAP). This procedure permits the user to execute a series of matrix operations of his choice along with any utility modules or executive operations that he may need. The user may even choose to write a module of his own. The rules governing all of these operations are described in Volume I, Section 5\.** 

**In order to relieve the user of the necessity of constructing a DMAP sequence for each of his problems, a number of such sequences, called rigid formats, have been included with NASTRAN, All of these rigid formats are resident on a data base called the Rigid Format Data Base, whfch is described in detail in Section 1.1.7. Each rigid format in this data base consists of a DMAP sequence and the associated restart tables. These restart tables are automatically used by the program to modify the series of DMAP operations to account for any changes that are made in any part of the Data Deck when making a restart, after having previously run all, or a part, of the problem. Without such tables, the user would have to carefully modify his DMAP sequence to account for the conditions surrounding each restart. The chances for error in making these modifications for restart are very great. The restart tables not only relieve the user of the burden of modifying his DMAP sequence, but also assure him of a correct and efficient program execution.** 

**In addition to the DkiAPsequence provided with each rigid format, a number of options are available, which are subsets of each complete DMAP sequence. Subsets are selected by specifying the subset numbers (zero for the complete DMAP sequence) along with the rigid format number on the SOL card in the Executive Control Deck. See the description of the SOL card in Volume I, Section 2.2 for the list of available subsets.** 

**If the user wishes to modify the DMAP sequence of a rigid format in some manner not provided for in the available subsets, he can use the ALTER feature described in Section 2.2. Typical uses are to schedule an EXIT prior to completion, in order to check intermediate output, schedule the printing of a table or a matrix for diagnostic purposes, and to delete or add a functional module to the DMAP sequence. (The manner in which DMAP ALTERs are handled in restarts is discussed in Section 1.1.5.) The user should be familfar with the rules for DMAP programing, as described in Volume I, Section 5, prior to making ALTERs to a rigid format.** 

**The following rigid formats for structural analysis are currently included in NASTRAN: 1\. Static Analysis** 

**1.1-1 (05/30/86)**  
**RIGID FORMATS** 

**2\. Static Analysis with Inertia Relief** 

**3\. Normal Modes Analysis** 

**4\. Static Analysis with Differential Stiffness** 

**5\. Buckling Analysis** 

**6\. Piecewise Linear Static Analysis** 

**7\. Direct Complex Eigenvalue Analysis** 

**8\. Direct Frequency and Random Response** 

**9\. Direct Transient Response** 

**10\. Modal Complex Eigenvalue Analysis** 

**11\. Modal Frequency and Random Response** 

**12\. Modal Transient Response** 

**13\. Normal Modes Analysis with Differential Stiffness** 

**14\. Static Analysis with Cyclic Synnnetry**   
I

**15\. Normal Modes Analysis with’Cyclic Symmetry** 

**16\. Static Aerothermoelastic Design/Analysis of Axial-Flow Compressors** 

**The following rigid formats for heat transfer analysis are included in NASTRAN:** 

**1\. Linear Static Heat Transfer Analysis** 

**3\. Nonlinear Static Heat Transfer Analysis** 

**9\. Transient Heat Transfer Analysis** 

**The following rigid formats foraeroelastic analysis are included in NASTRAN:** 

**9\. Blade Cyclic Modal Flutter Analysis** 

**10\. Modal Flutter Analysis** 

**11\. Modal Aeroelastic Response** 

**1.1.1 Input File Processor** 

**The Input File Processor operates in the Preface prior to the execution of the DMAP operations in the rigid format. A complete description of the operations in the Preface is given in the Programmer’s Manual. The main interest here is to indicate the source of data blocks that are created in the Preface and hence appear only as inputs in the DMAP sequences of the rigid formats. None of the data blocks created by the Input File Processor are checkpointed, as they are always regenerated on restart. The Input File Processor is divided into five parts, The first part (IFP1) processes the Case Control Deck, the second part (IFP) processes the Bulk Data Deck,** 

**1.1-2 (05/30/86)** 

**GENERAL DESCRIPTION OF**   
**RIGID FORMATS** 

**aconical shell element, and the fourth part (IFP4) performs additional processing of the bulk data**   
**the third part (IFP3) performs additional processing**   
**of the bulk data cards associated with the** 

**cards associated with the fluid element. The fifth section (IFP5) processes data related to acoustic cavity analysis.** 

**IFP1 processes the Case Control Deck and creates the Case Control Data Block (CASECC), the Plot Control Dat\~ Block (PCDB), and the XY-Plot Control Data Block (XYCDB). IFP1 also examines all of the cards, except those associated with plotting, for errors in format or use. If errors are detected, they are classed as either fatal or warning, and suitable error messages are provided. Reference to Volume I, Section 2.3 will assist the user in correcting errors in the Case Control Deck. If the error is fatal, the Executive System will not allow the execution to continue beyond the completion of the Preface.** 

**The Bulk Data Deck is sorted in the Preface, if necessary, before the execution of the second part of the Input File Processor. IFP checks all of the bulk data cards for errors according to the rules given for each card in Volum(iI, Section 2.4. If errors are detected, suitable messages are provided to the user. If the erlor is classed as fatal, the Executive System will not allow** 

**the execution to continue beyond the completion of the Preface. IFP creates the data blocks that oElement Properties Table (EP?’),the Material Properties Table (MPT), the Element Deformation Table**   
**are input to the various part of the Geometry Processor (GEOMl, GE\!3M2,GE@M3 and GE@M4), the** 

**(EDT), and the Direct Input Table (DIT).** 

**The third part of the Input File Processor (IFP3) converts the information on the special conical shell cards (CCONEAX, CTRAPAX, CTRIAAX, F\!3RCEAX,M\!3MAX,MPCAX, OMITAX, PCONEAX, P@INTAX, PRESAX, PTRAPAX, PTRIAAX, RINGAX, SECTAX, SPCAX, SUPAX, and TEMPAX) to reflect the number of harmonics specified by the user on the AXIC card. This converted information is added to any existing information on data blocks GEfJMl,GEk3M2,GE\!3M3and GE\!3M4.** 

**The fourth part of the input file processor (IFP4) converts the information on the fluid related cards (AXIF, BDYLIST, CFLUID2, CFLUII13,CFLUID4, DMIAX, FLSYM, FREEPT, FSLIST, GRIDB, PRESPT, and RINGFL) to reflect the desired harmonics, bolmdaries, and matrix input. This converted information is added to GEOMl, GE@M2, GE0M4 and MATP\!30L.** 

**The fifth part of the input file processor (IFP5) converts the information on the acoustic cavity related cards (AXSi.OT,CAXIF2, CAXIF3, CAXIF4, CSL0T3, CSL0T4, GRIDF, GRIDS, and SLBDY) to equivalent structural scalar points, elements, scalar springs and plotting elements. This** 

**converted information is added to the GEflMl** `1.`   
**and GE0M2 data blocks. \-3 (05/30/86)**

**RIGID FORMATS** 

**1.1.2 Functional Modules and Supporting DMAP Operations** 

**The DMAP listings of the rigid formats currently included with NASTRAN are presented in the following sections. Following each listing are subsections that deal with the following items for e each rigid format:** 

**1\. Brief description of important DMAP operations for the rigid format** 

**2\. Output available from the rigid format** 

**3\. Case Control Deck setup for the rigid format** 

**4\. Parameters used in the rigid format** 

**5\. Automatic ALTERs for Automated Multi-stage Substructuring (if applicable to the rigid format)** 

**6\. Rigid format error messages** 

**7\. Any other features peculiar to the rigid format** 

**Descriptions of all major functional modules are given in the Programmer’s Manual. Additional information is also given in the Theoretical Manual. Descriptions of all other NASTRAN modules are given in Volume I, Section 5\.** 

**The modules in the following list appear repeatedly in the rigid formats. Since the purpose of these operations in a rigid format is obvious, they are generally omitted from the descriptions** 

**of the DMAP operations in the following sections. given in Volume I, Section 5\.** 

**1\. BEGIN indicates the beginning of the DMAP**   
**More complete descriptions of these modules are** ● **sequence constituting the rigid format.** 

**2\. END indicates the end of the DMAP sequence constituting the rigid format \~mal termination when executed.** 

**3\. \_FILE makes declarations relative to a particular file.** 

**ABC \= TAPE states that file ABC will be assigned as a sequential file.** 

**DEF \= APPEND states that file DEF may be extended as the result of an in the rigid format.** 

**GHI \= SAVE states that file GHI should not be dropped after use as it for subsequent executions of an interna\~oop.** 

**4, LABEL specifies a labeled point in the sequence of DMAP instructions. referenced by REPT, JUMP and CI?JNDinstructions.** 

**5\. PARAM performs specified operations on integer DMAP parameters.**   
**and causes a** 

**internal loop may be needed Labels are** 

**6\. PRECHK actuates the automatic generation of explicit CHKPNT instructions. (PRECHK ALL Immediately and automatically CHKPNTS all output data blocks from each functional module, all data blocks mentioned in each PURGE instruction and all secondary data blocks in each EQUIV instruction.)\* The CHKPNT instruction specifies a list of files to be written on** 

**% The only exceptions to output in substructure**   
**this are the CASESS, CASEI and CASECC data blocks appearing as analyses.** 

**1.1-4 (05/30/86)**

**GENERAL DESCRIPTION OF RIGID FORMATS** 

**the new problem tape (NPTP), including files that may have been purged, either because they were not generated in this particular execution or were explicitly purged with a PURGE instruction.** 

**7\. PURGE specifies the names of files that.are conditionally dropped based on the parameter named.** 

**1.1.3 Checkpoint/Restart Procedures** 

**The checkpoint/restart feature available in NASTRAN is a very sophisticated and useful capability. The purpose of ttlisfeature is to enable a user to checkpoint a NASTRAN run and then restart it (with or without changes in data) by executing only those modules that need to be executed for the restart.** 

**There are several situations in which the use of the checkpoint/restart feature may be desirable. Some of these are listed below:** 

**1\. The user may wish to perform his analysis task in two or more stages by specifying scheduled exits in one or more runs.** 

**2\. The user may want to ensure that unscheduled exits (resulting from such causes as data errors, insufficient timej ii;suffic,ientcore or hardware failures) will not require him to repeat his entire analysis.** 

**3\. The user may wish to rerun his problem by making limited changes in his data. Scheduled exits can be requested at any point in a rigid format by means of the ALTER feature. (The manner in which ALTERs are handled in restarts is discussed in Section 1.1.5). An exit is scheduled by insertirl\~the following cards in the Executive Ccmtt’olDeck: ALTER K1 $** 

**EXIT K2 $** 

**ENDALTER $** 

**where K1 \= DMAP statement number after which exit will take place** 

**and K2 \= Number of times EXIT instruction will be skipped before zero, For use with loops, where the user wishes to execute scheduling the exit.** 

**If the user chooses to restart the problem without making any changes, execute an unmodified restart following the last completed checkpoint. Unscheduled exits are usually caused by errors on input cards or**   
**I\~eing executed \- default is the loop K2 times before** 

**the Executive Systerrjwill errors in the structural**   
**model resulting from missing or inconsistent input data. When such errors are detected, an unscheduled exit is performed accompanied with the olutputof the applicable user error messages. Following the correction of the input data errors, a modified restart can be performed.** 

**1.1-5 (05/30/86)**  
**RIGID FORMATS** 

**Unscheduled exits may also occur because of machine failure or insufficient time allowance. In these cases, an unmodified restart is usually made following the last completed checkpoint. In some cases, where a portion of the problem has been completed, including the output for the completed portion, a modified restart must be made following an unscheduled exit due to insufficient time allowance. These situations are discussed under Case Control Deck requirements in the sections dealing with the individual rigid formats.** 

**The initial execution of any problem must be made with a complete NASTRAN Data Deck, including all of the bulk data. However, all or part of the bulk data may be assembled from alternate input sources, such as the User’s Master File or a module written by the user to generate** 

**input. The User’s Master File is described in Volume I, Section 2.5 discussed in Volume I, Section 2,6.** 

**For restarts, the Bulk Data Deck consists only of delete cards and new cards which the user wishes to add. The previous Bulk Data**   
**and user generated input is** 

**(see Volume I, Section 2.4) Deck is read from the Old** 

**Problem Tape. All other parts of the NASTRAN Data Deck, including the Executive Control Deck, the Case Control Deck, the BEGIN BULK card and the ENDDATA card must be resubmitted even though no changes are made in the control decks and no new bulk data is added. In addition, the RESTART cards (or dictionary) punched during the previous execution must be included in the Executive** 

**Control Deck. When changing rigid formats, the solution number of the new rigid format.** 

**A New Problem Tape (NPTP) is constructed only when checkpo**   
**S@L) must be changed to the number nting is requested (CHKPNT YES) in**   
**the Executive Control Deck. The NPTP should be assigned to a physical tape or other storage device that can be dismounted and saved at the conclusion of the execution. At the completion of an initial execution, the NPTP contains the input deck, with the bulk data in sorted form, and all of the files that were checkpointed during the execution.** 

**For restarts, the Old Problem Tape (13PTP)is defined as the Problem Tape that was written during the previous execution. The NPTP is defined as the Problem Tape written during the current execution, beginning with the restart. At the completion of an unmodified restart, the NPTP contains the input deck, with the bulk data in sorted form, all files from the OPTP that are necessary to complete the solution, and all of the files checkpointed during the current executicn. At the completion of a modified restart, the NPTP is similar, except that the inFut deck is modified according to the information shbmitted for the restart.** 

**1.1-6 (05/30/86)**

**1.1.4**   
**GENERAL DESCRIPTION OF RIGID FORMATS** 

**Types of Restarts** 

●**The type of a restart is determined automatically by the program by comparing the input data of the restart run with that of the checkpoint run. The user need not be concerned about the manner in which this is done, but may be interested in knowing the resulting type.** 

**The types of restarts presently recognized in NASTRAN are summarized in the following table. Types of Restarts in NASTRAN** 

**Restart data compared to checkpoint data** 

**No effective changes** 

**Effective**   
**changes only to the Case Control Deck andlor the Bulk Data** 

**Deck** 

**Change in**   
**rigid format**   
**Resulting type**   
**of restart** 

**e** 

**Unmodified Yes restart** 

**Modified Yes restart** 

**Modified restart Yes with rigid**   
**format switch** 

I   
**mment DMAP** 

**Yes** 

**Yes** 

**No** 

**In earlier**   
**\~ersions of NASTRAN, an additional type of restart, called the pseudo modified** 

**restart, was recognized for cases involving changes only in output requests. This is no longer done since it is now handled as a special case of the modified restart.** 

**The manner in which a restart is handled by the program depends on its type and on its environment (rigid format or DMAP environment). This is discussed in the following sections. An important term that is frequently encountered in the following discussion is the reentry point for a, restart. This is defined as the last reentry point specified in the restart dictionary. It is an integer equal to the instruction number of the DMAP instruction in the checkpoint run at which an unmodified restart will resume execution. (See Volume I, Section 2.2.)** 

**1.1-7 (05/30/86)**  
**RIGID FORMATS** 

**1.1.4.1 Unmodified Restart** 

**An unmodified restart involves no effective changes to the data. The execution in this type of restart resumes at the reentry point. Unmodified restarts in both rigid format and DMAP e environments are handled in an identical manner.** 

**It is useful to distinguish between two types of unmodified restarts. These are described below.** 

**\- Unmodified restart in which the reentry point is not within a DMAP loop** 

**This is the simplest type of restart possible. In this case, the execution flags for all DMAP instructions prior to the reentry point are turned off and the execution flags for all DMAP instructions from the reentry point onwards are turned on. All input files or data blocks required for the restart already exist on the J3PTPand will be retrieved.** 

**\- Unmodified restart in which the reentry point is within a DMAP loop.** 

**In this case, initially, the execution flags for all DMAP instructions prior to the reentry point are turned off and the execution flags for all DMAP instructions from the reentry point onwards are turned Gn. This is so indicated in the DMAP source listing. However, subsequently, the DMAP instructions prior to the reentry point and within the DMAP loop are recognized and their execution flags are turned on. The user is informed about this in the output. Note, however, that the execution does resume at the reentry point, even though DMAP instructions prior to this point are turned on. DMAP instructions within the DMAP loop and prior to the reentry point are executed only o if additional passes in the loop need to be executed. If the restart is within the last pass of the DMAP loop, obviously DMAP instructions within the loop and prior to the reentry point are not executed even though their execution flags are on.** 

**All input files or data blocks required by the restart already exist on the OPTP and will be retrieved.** 

**1.1.4.2 Modified Restart** 

**This type of restart involves one or more effective changes to the data in the Case Control Deck and/or in the Bulk Data Deck,** 

**The heart of the restart logic for modified restarts in the rigid format environment is the Modu”leExecution Decision Table (MEDT) associated with each rigid format. The MEDT for each rigid furmat dciually comprises three distinct tables. These are the Card Name Restart Table, the Rigid \~crmat Change Restart Table and the File Name Restart Table associated with that rigid format. fr{.ue discussion in Section 1.1.7. See also Sections 1.10 and 7 of the Programmer’s Manual.) 1.1-8 (05/30/86)** 

“  
**GENERAL** 

**In the case of modified restarts**   
**DESCRIPTION OF RIGID FORMATS** 

**in the rigid format environment, all DMAP instructions from** 

**the reentry points onwards have their execution flags turned on. In addition, this type of restart generally requires that certain DMAP instructions prior to the reentry point also be turned on, depending on the specific data changes involved. The DMAP instructions that need to be so turned on are determined from the Card Name Restart Table. The DMAP source listing provided in the output indicates all the DMAP instructions whose execution flags are initially turned on by the above procedure.** 

**Once the DMAP instructions are initially turned on as described above, the program checks to see if all of the required input data blocks are either being generated by prior modules or are available on the 13PTPfor retrieval. If so, no additional DMAP instructions need to be turned on. If, however, there are any input data blocks that are neither being generated by prior modules nor are available on the OPTP, the program needs to turn on additional DMAP instructions in order to generate the required data blocks. The DMAP instructions that need to be so turned on are determined from the File Name Restart Table.** 

**After the additional DMAP instructions are turned on as described in the above paragraph, the process is repeated until it is ensured that all of the required input data blocks are either being generated by prior modules or can be retrieved from @PTP.** 

**All the DMAP instructions that are turned on as per the above logic (by the use of the Fil”e Name Restart Table) are identified and listed in the restart output just after the DMAP source listing.** 

**It should be noted that the execution in a modified restart will start at the first module in the DMAP sequence whose execution flag is turned on. Generally, this is before the reentry point. In the case of modified restarts in the DMAP environment, the effect of changes in the Case Control Deck and/or in the Bulk Data Deck on particular modules cannot be determined since the DMAP itself is, by definition, not predefine. (An MEDT is meaningless for a DMAP.) Hence, it is assumed that the changes will affect the entire DMAP which, therefore, needs to be re-executed. This is accomplished in the program by re-setting the reentry point to zero-and treating this case as an unmodified restart. This causes the entire DMAP to be re-executed.** 

**Those input files or data blocks that are needed for the restart and that are available on the jlPTPare retrieved, just as it is done in the** `case`**of modified restarts in the rigid format environment.** 

**1.1-9 (05/30/86)**

**RIGID FORMATS** 

**1.1.4.3 Modified Restart with Rigid Format Switch** 

**This type of restart involves a switch from one rigid format to another. It may or may not involve effective changes to the data in the Case Control Deck and/or in the Bulk Data Deck. The most important point to recognize in this type of restart is that the reentry point is quite meaningless since it was determined in relation to another rigid format. This is handled in the program by resetting the reentry point to an extremely high value which, for all practical purposes, can be considered to be infinite. As a result, all DMAP instructions in the restart are considered to be before the reentry point and no DMAP instructions are considered to exist after the reentry point.** 

**Once this important change is made, this type of restart is handled in the program in the same manner as a modified restart, with one important modification: the DMA.Pinstructions that are initially turned on are determined not only from the Card Name Restart Table, but also from the Rigid Format Change Restart Table.** 

**1.1.5 Use of DMAP ALTERs in Restarts** 

**Because different types of restarts are handled differently by the program, the user should be careful in the use of DMAP ALTERs in restarts.** 

**In the case of an unmodified restart in which the reentry point is not within a DMAP loop, the only DMAP instructions that are flagged for execution are those that are beyond (and include) the reentry point. Hence, a DMAP ALTER will be flagged for execution only if it is beyond the reentry point and will be ignored if it is before the reentry point.\*** 

**In the case of an unmodified restart in which the reentry point is within a DMAP loop, the only DMAP instructions flagged for execution are those that are beyond (and include) the reentry point and those that are before the reentry point but within the DMAP loop. Hence, a DMAP ALTER will be flagged for execution only if it is beyond the reentry point or before it but within the** 

**DMAP loop. Otherwise, it will be.ignored.\*** 

\* **The user can ensure that a DMAP ALTER in an unmodified restart is flagged for execution by suitably deleting the latter part of the restart dictionary so that the reentry point is before the DMAP ALTER. This, of course, will cause more modules to be executed in the restart.** 

**1,1-10 (05/30/86)**  
**GENERAL DESCRIPTION OF RIGID FORMATS** 

**In the case of a modified restart and a modified restart with rigid format switch, a DMAP ALTER will be flagged for execution regardless of its position in the DMAP with respect to the reentry point.** 

**1.1.6 Rigid Format Output** 

**Although most of the rigid format output is optional, some of the printer output is automatic. The printer output is designed for 132 characters per line, with the lines per page controlled by the NLINES keyword on the NASTRAN card (see Volume I, Section 2.1) and the LINE card in the Case Control Deck (see Volume I, Section 2.3). The NLINES and LINE default is set to fft on n-inch paper. Optional titles are printed at the top of each page from information in the Case Control Deck. These titles may be defined at the subcase level. The pages are automatically dated and numbered.** 

**The output from the data recovery and plot modules is all optional, and its selection is controlled by cards in the Case Control Deck. The details of making selections in the Case Control Deck are described in Volume I, Section 2.3 for printer and punch output, and in Volume I, Section 4 for plotter output. Since the outputs from the data recovery and plot modules vary considerably with the rigid format, a list of available output is included in the section on the Case Control Deck for each rigid format. Information on the force and stress output available for each element type is given in Volume I, Section 1.3.** 

**The first part of the output for a NASTRAN run is prepared during the execution of the Preface, prior to the beginning of the DMAP sequence of the rigid format. The following output is either automatically or optionally provided during the execution of the Preface:** 

**NASTRAN title page \- Two full pages automatic, unless changed with the TITLEOPT keyword**   
**1\.**   
**on the NASTRAN card (see Volume I, Section 2.1) before the Executive Control Deck. 2\.**   
**Executive Control Deck echo \- Automatic.** 

**Case Control Deck echo \- Automatic.**   
**3\.** 

**Unsorted Bulk Data Deck echo \- Optional, selected in Case Control Deck with the ECHO 4\.**   
**Card. (Automatic in restart runs and in runs employin suppressed in the Case Control Oeck with the ECHO card.**   
**7**   
**the User’s Master File, unless** 

**Sorted Bulk Data Deck echo \- Automatic, unless suppressed in the Case Control Deck with**   
**5\.**   
**the ECHO Card,** 

**DMAP listing \- Selected with DIAG 14 (or the LIST option on an XDMAP card) in the**   
**6\.**   
**Executive Control Deck. Provides the list OF DMAP instructions, including those resulting from ALTERs, for the subset of the rigid format being executed, (Automatic in restart runs and in runs using the DMAP approach (APP DMAP) or the substructure capability (APP DISP, SUBS), unless suppressed by the NOLIST option on an XDMAP card in the Executive Control Deck.)** 

**1.1-11 (05/30/86)**

**KLtil\!Ji\_UKM/41S** 

**7, Checkpoint Dictionary \- Automatic, when operating in the checkpoint mode. A printed echo (unless suppressed with the DIAG 9 card in the Executive Control Deck) and punched output are prepared for additions to the checkpoint dictionary after the execution of each checkpoint.** 

**When making restarts, the following additional output is automatically prepared during the execution of the Preface:** 

`1,`   
**Asterisks (\*) are placed beside the DMAP statement numbers of all instructions that are flagged for execution in the restart. (It should be emrIhasizedthat a DMAP instruction**   
**marked with the symbol \* is only fla ed for execution; ’whether it actually g \*AP.)**   
**or not is decided by the logic in the**   
**ets \-executed** 

**2\.**   
**Pluses (+) are placed beside the DMAP statement numbers of all instructions that are processed only at DMAP compilation time. (DMAP instructions BEGIN, COMPOFF, C@MPON, FILE, LABEL, PRECHK and XDMAP are the only instructions that belong to this category,)** 

**3\.**   
**Message indicating the bit position activated by a rigid format change. 4\.**   
**Message indicating the type of restart (unmodified, modified or modified with rigid format switch).** 

**5\.**   
**Table indicating, among other things, the effective data changes (if any) and the associated “packed bit positions” that control the restart. The table distinguishes between effective changes made to the Case Control Deck and those made to the Bulk Data Deck, The reader is referred to the Programmer’s Manual for the full interpretation of this table.** 

**6\.**   
**List of files along with the DMAP instructions that were marked for execution (if any) by the File Name Restart Table.** 

**7\.**   
**List of files from the Old Problem Tape, including**`-r-`**purqed files, used to initiate the estart.** 

**A number of fatal errors are detected by the DMAP statements in the various rigid formats. These messages indicate the presence of fatal user errors that either cannot be determined by the functional modules or can be more effectively detected by the DMAP statements in the rigid format. The detection of such an error causes a transfer to a LABEL instruction near the end of the rigid format. The text of the message is output and the execution is terminated. These messages will always appear at the end of the NASTRAN output. The messages applicable to each rigid format are described under the description of that rigid format.** 

**NASTRAN diagnostic messages are usually identified by numbers. These messages may be program diagnostics or user diagnostics, and they may contain information, warnings, or indication of a fatal error. There are also a few unnumbered, self-explanatory messages, example, the time that the execution of each functional module begins and ends.**   
**either an** 

**for** 

**The Grid Point Singularity Table (GPST) is automatically output following the execution of the Grid Point Singularity Processor (GPSP) if singularities remain in the stiffness matrix at the grid point level. This table contains all possible combinations of single-point constraints, in the global coordinate system, that can be used to remove the singularities. Entries in this table** 

**1,1-12 (05/30/86)**  
**GENERAL DESCRIPTION OF RIGID FORMATS** 

**should only be treated as warnings, because it cannot be determined at the grid point level whether** 

**or not the singularities are removed by other means, such as general elements or multipoint** @ 

**constraints. Further information on this matter is given in the Theoretical Manual. Several items of output are discussed in other sections. Output that is not associated with** 

**all of output (PARAM**   
**the rigid formats is discussed in the sections treating the individual rigid formats. Some is under the control of PARAM cards. These items are discussed in Volume I, Section 2.4 card). The DIAG card is used to control the printing of some output. A list of the** 

**available output under DIAG control is given in the description of the Executive Control Deck in Volume I, Section 2.2.** 

**Any of the matrices or tables that are prepared by the functional modules can be printed by using selected utility modules described in Volume I, Section 5.5. These utility modules can be scheduled at any point in a rigid format by using the ALTER feature. (See Section 1.1.5 for the manner in which ALTERs are handled in restarts.) In general, they should be scheduled irrrinediately after the functional module that generates the table or matrix to be printed. Note that functional modules cannot be separated from a SAVE instruction. However, the user is cautioned to check the** 

**calling sequence for the utility**   
**egenerated prior to this point. 1.1.7 Rigid Format Data Base \-——.** 

**As indicated earlier, the** 

**information for all of the rigid**   
**module, in order to be certain that all required inputs have been** 

**Rigid Format Data Base contains the DMAP sequences and other formats in NASTRAN. Its design allows for convenient maintenance** 

**of the existing rigid formats as well as the addition of new rigid formats. Editing of the data base may be done by using standard text editors provided on the host computer systems.** 

**1.1.7.1 Design of the Data Base** 

**The Rigid Format Data Base is a collection of all rigid formats available to the user in NASTRAN. Each Rigid Format is maintained as a separate card-image entry within the data base. The entry for each rigid format consists of three parts. The first part is the DMAP part. It.contains the DMAP sequence for the rigid format, the DMAP sequence subset flags, the restart flags (card name, file name and rigid format switch restart flags) and the substructure DMAP ALTER control flags. The second part contains the card name table and the third part contains the file name table. The restart flags in the first part and the name tables comprising the second and third** 

**1.1-13 (05/30/86)**  
**RIGID FORMATS** 

**parts are not processed by NASTRAN in non-restart runs. Similarly, the substructure control flags in the first part are not processed in non-substructure runs. @ The format of the data base is free field. Each of the three parts in a rigid format entry is separated from’the other parts by a “$\*” card. The following fictitious example illustrates a rigid format entry in the data base.** 

**APR.86**   
**$$$$ THIS IS A COMMENT $$$$ \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*** 

**MODULEl INl,IN2,/f3uTl,guT2//\*PARMl\*$**   
**\*\*\*\*s8ST 1,3,9-12**   
**\*\*\*\*RFMT 188,200-201**   
**\*\*\*\*CARD 1-20,30,44**   
**\*\*\*\*FILE 100-104,110**   
**\*\*\*\*pHSl II**   
**\*\*\*\*pHS2 DB5**   
**\*\*\*\*PHS3 D7** 

**$$$$ \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*** 

**MgDuLE2 IN3,1N4/0UT3/\*PARM2\* $**   
**\*\*\*\*CARD 1-40,45**   
**\*\*\*\*FILE 101,102**   
**\*\*\*\*pHS2 DE5** 

**$$$$ \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*** 

.   
.   
. 

**$$$$**   
**$\*CARD NAME TABLE** 

**$$$$AXIC AXIF CELAS1**   
**CELAS2**   
**;**   
**ADUM1 CDUM1 CR@D**   
.   
. 

**$$$$ “**   
**$\*FILE NAME TABLE**   
**$$$$**   
**94 SLT GPTT**   
**95 KGGX GPST**   
.   
. 

**$\* “** 

**The very first card of an entry identifies the release of NASTRAN with which the rigid format is associated. In this example, the rigid format is associated with the April 1986 release. The “$\*CARD” card separates the card name table from the DMAP part of the entry and the “$\*FILE” card separates the file name table from the card name table. A “$\*” card terminates the file ndme table and the rigid format entry.** 

**Comment cards are identified in the data base by the “$$$$” identification in the first four columns of the field and control cards are identified by the “\*\*\*\*” identification in the first four columns of the field.** 

**1.1-14 (05/30/86)**

●   
**GENERAL DESCRIPTION OF RIGID FORMATS** 

**Comment cards may be placed anywhere in the card name or file name tables (the second and third parts of a rigid format entry). However, comment cards have a required usage and serve a specific purpose in the DMAP part of a rigid format entry. In this part, a conment card is used to distinguish and separate a OMAP entry (that is, a DMAP statement and its associated control cards)** 

**from another DMAP entry. from the next DMAP entry. string of “\*” is used for entries.** 

**All DMAP statements**   
**Hence, there must be at least one comment card separating a DMAP entry In the data base supplied with NASTRAN, a comment card with a trailing this purpose to serve as a cosmetic delineation between successive DMAP** 

**must conform to the rules as specified in Volume I, Section 5,2. Any** 

**card in the DMAP part of a rigid format entry that does not begin with “$$$$” or “\*\*\*\*” in the** 

**first four columns of the field is consi(**   
**ered to be a DMAP statement or part of a DMAP statement.** 

**Comment and control cards in a rig’ cards can only extend up to 72 columns. Control cards (that is, cards that** 

**d format entry can extend up .to80 columns. begin with “\*\*\*\*” in the first four columns**   
**However, DMAP of the field)** 

● ●   
**\~re permitted only in the DMAP part of a rigid format entry. A control card must have any one of seven four-character names in columns five through eight. The permissible names are: SBST, RFMT, CARD, FILE, PHS1, PHS2 and PHS3. Control cards follow the corresponding DMAP statement in the entry and may be specified in any order.** 

**The “SBST”, “RFMT”, “CARD” and “FILE” control cards contain sequences of numbers and/or ranges of numbers in ascending order represe\~itedby the use of a dash. A comma is required after each number in a sequence or after a range of numbers, if an additional number or range of numbers is to fo”llow. There may be multiple cards for any one of these control cards for a specific DMAP statement.** 

**The “SBST” control card provides DMAP sequence subset controls. If a user requests a 9iven subset on the SOL card of a NASTRAN run and that number is in the sequence of numbers given on the “SBST” card, then the associated DMAP statement is deleted. The range of subset numbers is from 1 to 9 and each number is documented under the description of the SOL Executive Control card in Volume I, Section 2.2.** 

**The “RFMT” control card is processed in restart runs and is applicable to cases where a rigid format switch has occurred. Each rigid format has a unique number assigned to it. For APPROACH DISP, rigid formats 1 through 16 are assigned the numbers 187 through 202, respectively. For APPROACH HEAT, rigid formats 1, 3 and 9 are assigned the numbers 207, 2C8 and 209, respectively.** 

**1.1-15 (05/30/86)**  
**Kltill.1tUKPIAIS** 

**For APPROACH AERO, rigid formats 9, 10 and 11 are assigned the numbers 216, 214 and 215, respectively. A DMAP statement is flagged for execution in a modified restart if the number associated with the rigid format that was used in the checkpointed run is listed in the sequence of numbers given on the “RFMT” card provided with the DMAP statement.** 

**The “CARD” and “FILE” control cards provide restart information for changes that involve input data or files within the DMAP. For a given rigid format, every type of effective change in the Case Control and Bulk Data Decks and each output file (or data block) in the DMAP is assigned a number as defined in the card name and file name tables in the second and third parts of a rigid format entry. In a modified restart, if the number associated with an input data change or an affected file appears in the sequence of numbers given on the “CARD” or “FILE” cards, then the corresponding DMAP statement is flagged for execution in the restart run.** 

**The information provided by all of the “CARD” control cards in a rigid format entry is collectively referred to as the Card Name Restart Table. Similarly, the information provided by all of the “FILE” and “RFMT” control cards in a rigid format entry is collectively referred to as the File Name Restart Table and the Rigid Format Change Restart Table, respectively. For a given rigid format, these three restart tables compose the Module Execution Decision Table (MEDT) of that rigid format.** 

**The “PHS1”, “PHS2” and “PHS3” control cards are used to indicate where substructure DMAp ,,LTERs are to be generated. The number following the “PHS” refers to the substructure phase number. These cards must have one of the following flags: “In”, “Dn”, “DBn” or “DEn”. The “n” in these flags is an integer that refers to the subroutine governing the substructure run (subroutine ASCMOI, ASCM05, ASCM07 or ASCM08) and must have the value “l” for Phase 1 cards, either the value “5” or “8” for Phase 2 cards, and either the value “l” or “7” for Phase 3 cards. The “I” in the “In” flag indicates that a DMAP ALTER is to be inserted after this DMAP statement. The “D” in the “Dn” flag indicates that this DMAP statement is to be deleted and possibly replaced by a DMAP ALTER. The “DB” in the “DBn” flag and the “DE” in the “DEn” flag indicate the beginning and the end of a group of contiguous DMAP statements that are to be deleted and possibly replaced by a DMAP ALTER. Users are cautioned to be very careful in making any changes to these substructure control cards because of their impact on the DMAP ALTERs automatically generated in substructure analyses. (The automated substructure capability is currently implemented only in rigid formats 1, 2, 3, 8 and 9, APPROACH DISP.)** 

**1.1-16 (05/30/86)**  
**GENERAL DESCRIPTION OF RIGID FORMATS** 

**The card name and file name tables assign numbers to every type of effective change in the Case Control and Bulk Data Decks and to every output file (or data block) in the DMAP. Numbers 1 through 93 are allocated to card names and numbers 94 through 186 are allocated to file (or data block) names. This information is used subsequently to determine the DMAP statements to be flagged for execution in modified restarts. The format of these tables is free field. Each entry in these tables must have an integer number in the first field and a list of names in the remaining fields** 

**of the entry. characters. No these tables to**   
**All names are to be alphanumeric and may contain up to a maximum of eight name should appear twice in these “tables. Comment cards may be freely used in facilitate readability.** 

**1.1,7.2 Implementation of the Data Base** 

**The Rigid Format Data Base is implemented differently on the CDC, DEC VAX, IBM and UNIVAC versions. On the CDC and DEC VAX versions, each rigid format entry is stored as a separate file. The local names of these files during a NASTRAN execution are: DISPI through DISP16 for APPROACH DISP; HEAT1, HEAT3 and HEAT9 for APPROACH HEAT; AER09, AEROIO and AERf311for APPROACH AERi3. These same files are stored as members of a partitioned data set (PDS) on the IBM version and iiselements of the \*NASTRAN file on the UNIVAC version. The member and element names are exactly the same as** 

**the local file names on the CDC and DEC VAX versions. Rigid Format Data Base must be referred to by a Data RFDATA. On the UNIVAC version, the \*NASTRAN file is absolutes. (See References 1 and 2 for the formats of**   
**On the IBM version, the PDS containing the Definition card, “DD”, with the DDname of the file containing the NASTRAN program file names for the CDC and DEC VAX versions,** 

**respectively. See Reference 3 for the formats of DDnames and member names for the IBM version. See Reference 4 for the format of UNIVAC file names.)** 

**1.1.7.3 Usage of the Data Base** 

**The following examples illustrate the manner in which the Rigid Format Data Base is accessed and used on all of the,four versions of NASTRAN.** 

**CDC VERSION** 

**/J17B.**   
**.** 

**\~ET,DISpl,DISP2,DISP3,DISP4,DISP5.**   
**GET,DISP6,DISP7,DISP8,DISP9,DISP1O.**   
**GET,DISP11,DISP12,DISP13,DISP14,DISP15,DISP16.** 

**1.1-17 05/30/86)**

**RIGID FORMATS** 

**GET,HEAT1,HEAT3,HEAT9,AER\!39,AER@10,AER011.**   
**RFL,220000.**   
**REDUCE,-.**   
**LINKl,INPUT,@UTPUT,PUNCH,UT1.** 

**{\~@R**   
**....**   
. 

**\~NDDATA**   
**/Ef3F** 

**DEC VAX VERSION** 

**ASSIGN DDB1:\[NASOIR\]DISP1.DT DISP1.**   
**ASSIGN DDB1 :\[NASOIR\]DISP2.OT DISP2.**   
. 

**AssIGN bOBI:\[NASOIR\]HEAT1.DT HEATI.**   
. 

**ASSIGN 6DBI:\[NASDIR\]AER011.DT AER1311.**   
**@DoBl:\[NASDIR\]NASTRAN DEM@.DT** 

**IBM VERSION** 

**// EXEC NASTRAN**   
**//NS.RFDATA DD DSN=RIGID.FORMAT.DATA.DISP=SHR \\{NS.SySIN DD \* ‘ ‘-**   
**....**   
**.** 

**iNDDATA** 

**//** 

**UNIVAC VERSION** 

**@ASG,A \*NASTRAN.**   
**@XQT \*NASTRAN.LINK1** 

**1.1.7.4 Development of User Rigid Formats** 

**In addition to using COSMIC-supplied formats, with restart capabilities included. rules explained earlier and must be similar**   
**rigid formats, users may develop their own rigid Rigid formats developed by users must conform to the in content and structure to the COSMIC-supplied rigid** 

**formats. Each user-developed rigid format must reside as a separate file on the CDC and DEC VAX versions, as a member of a PDS on the IBM version and as a file or file.element on the UNIVAC version.** 

**Before developing their own rigid formats, users are strongly advised to carefully study and examine the COSMIC-supplied rigid formats, particularly with regard to their use of control cards. The following important guidelines should help users in developing their own rigid formats.** 

**1.1-18 (05/30/86)**  
**GENERAL DESCRIPTION OF RIGID FORMATS** 

**The DMAP sequence of the user rigid format must be tested for its correctness and logic.** `1.` 

**This testing may be done either in a DMAP environment or in the environment of an existing rigid format by use of ALTERs.** 

**2\.**   
**The card name table (the second part of a rigid format entry) must be constructed by assigning numbers 1 through 93 for all types of Case Control and Bulk Data Deck changes that will affect the logic of the rigid format. Normally, those input data changes that have the same effect on the logic of the rigid format are assigned the same number. The file name table (the third part of a rigid format entry) must be constructed by 3\.** 

**assigning numbers 94 through 186 for all files (or data blocks) that are output by the functional modules in the rigid format. Normally, all files (or data blocks) output from a given functional module are assigned the same number.** 

**The DMAP part (the first part of a rigid format entry) must be constructed by following 4,** 

**each statement in the DMAP sequence by the appropriate control cards and by ensuring that each DMAP entry (that is, a DMAP statement and its associated control cards) is separated from the next DMAP entry by at least one comment card.** 

**A given DMAP statement must be followed by a “SBST” control card if that DMAP statement 5\.** 

**belongs to one or more of the DMAP subsets. These subset numbers must be specified on the “SBST” card. The acceptable subset numbers and their meanings are documented under the description of the SOL Executive Control card in Volume I, Section 2.2. A “RFMT” control card must follow a DMAP statement if that DMAP instruction is to be 6\.** 

**flagged for execution on restart from a checkpoint of one of the COSMIC-supplied rigid formats. (It is not possible to have a restart in a COSMIC-supplied rigid format from a checkpoint of an user-developed rigid format.) This will be so if this DMAP instruction is not part of the DMAP sequence of the rigid format that was used in the checkpoint run. The “RFMT” control card must list the numbers of the appropriate COSMIC-supplied rigid formats (187 through 202 for rigid formats 1 through 16, respectively, for APPROACH DISP; 207, 208 and 209 for rigid formats 1, 3 and 9, respectively, for APPR9ACH HEAT; and 216, 214 and 215 for rigid formats 9, 10 and 11, respectively, for APPROACH AERO). A DMAP statement must be followed by one or more “CARD” control cards indicating the 7\.** 

**effective input data changes that require that DMAP instruction to be flagged for execution on restart. Any effective input data change will affect one or more files (or data blocks) or parameters in the DMAP sequence. Therefore, for a given data change, all** 

**1.1-19 (05/30/86)**  
**RIGID FORMATS** 

**CMAP instructions that use the affected files (or data blocks) or parameters as input are potential candidates to be flagged for execution on restart. However, the logic of these individual OMAP instructions must be checked further (see the Programmer’s Manual) to see if they are really impacted by the given data change. This procedure must be applied in** 

**turn to those input. This considered.**   
**DMAP instructions that use the output of the affected DMAP instructions as procedure must be repeated until the entire DMAP sequence has been** 

**8,**   
**ADMAP statement must be followed by one or more “FILE” control cards indicating the DMAP files (or data blocks) whose generation requires the execution flag for that DMAP statement to be turned on during restart. Normally, for a given DMAP file (or data block) that is required on restart but is not available from the checkpoint run, the DMAP instruction that generated it must be flagged for execution. However, in practice, additional DMAP instructions like PURGE and EQUIV that manipulate the given file (or data block) must also be flaggedfor execution.** 

**9\.**   
**The restart flags for a C9ND DMAP instruction (and its companion LABEL DMAP instruction) must include the restart flags for those DMAP instructions whose execution it controls. “PHS1”, “PHS2” and “PHS3” control cards must not be used as the substructure capability 10\.** 

**is not applicable to user rigid formats.** 

**1.1.7.5 Usage of User-Developed Rigid Formats** 

**An user-developed rigid format is referenced through the use of the SOL card in the Executive Control Deck. However, instead of specifying the solution number or the name of the COSMIC-supplied rigid format on this card, the name of the user-developed rigid format is specified. This name is a file name on the CDC and DEC VAX versions, a member nameof a PDS on the IBM version and a file or file.element name on the UNIVAC version. The member name given on the IBM version must be in the file referenced on the RFDATA DO statement. The manner in which an user-developed rigid format is accessed and used is similar to that of a COSMIC-supplied rigid format, as explained in the examples given Section 1.1.7.3. Thus, for instance, an user-developed rigid format can be accessed and used on the CDC version in the following manner.** 

**/J@B.**   
**.** 

**GET,NEWRF.**   
**RFL,220000.** 

**1.1-20 (05/30/86)**  
**GENERAL DESCRIPTION OF RIGID FORMATS** 

**REDUCE.-.**   
**LINK1,iNPUT,OUTPUT,pUNCH,UT1.**   
**lEOR**   
**ID” ....**   
**S@L NEWRF** 

**;EOF** 

**1.1-21 (05/30/86)**  
**RIGID FORMATS** 

**REFERENCES** 

**1\. Control Data Corporation NOS 1.0 Reference Manual, Document No. 60435400\. 2\. VAX/VMS Command Language User’s Guide, Digital Equipment Corporation, Order No. AA-D023C-TE. 3, IBMOS/VS2 MVS JCL, Document No, GC28-0692-4.** 

**4\. Sperry UNIVAC 1100 Series Executive System EXEC Programmer Reference, Volume 2, Document No. UP-4144.2.** 

**1.1-22 (05/30/86)**  
**2\. DISPLACEMENT RIGID FORMATS** 

**2,1 STATIC ANALYSIS** 

**2,1.1 DMAP Sequence for Static Analysis** 

**RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 1** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**OPTIONS IN EFFECT GO ERR=2 LIST NODECK NOREF NOOSCAR \-----------------** 

**1 BEGIN DISP 01 \- STATIC ANALYSIS \- APR.86 $** 

**2 FILE oPTP2=sAvE/EsTl=sAvE $** 

**3 FILE QG=APPEND/PGG=APPEND/UGV-APPEND/GM=SAVE/KNN=SAVE $ 4 SETVAL //V,Y,lNTERACT/0/v,Y,5YS21/O $** 

**5 PARAM //\*14PY\*/CARDNO/O/O$** 

**6 COhPOFF l,INTERACT $** 

**7 PRECHK ALL $** 

**8 COMPON I,INTERACT $** 

**10 COMPOFF LBLINT02,SYS21 $** 

**v11 GPl GEOMl,GEOM2,/GPL,EQEXIN,GPDT, CSTM,BGPDT,SIL/S,N,LUSET/ NOGPDT/ALWAYS=-l $** 

**12 PLTTRAN BGPDTsSIL/BGPDP,SIP/LUSET/.S,N, LUSEP $** 

**13 GP2 GEoM2,EQExlN/EcT $** 

**14 PARAML PCOR//\~\~PRES\*////JUMPPLOT$** 

**15 PURGE PLTSETX,PLTPAR,GPSETS,ELSETS/JUMPPLOT $** 

**16 COND P1,JUMPPLOT $** 

**17 PLTSET PCOB,EQEXIN,ECT/?LTSETX,PLTPAR,GPSETS,ELSETS/S,N,NSIL/ S,N,JUMPPLOT $** 

**18 PRTMSG PLTSETX// $** 

**19 PARAM //\*MPY\*/PLTFLG/l/l $** 

**20 PARAM //\*MPY\*/PFILE/O/O $** 

**21 COND P1,JUMPPLOT $** 

**22 PLOT PLTPAR,GPSETS,ELSETS,CASECC,BGPDT, EQEXIN,SIL, ,ECT, ,/PLOTXl/ NSIL/LUSET/S,N,JUMPPLOT/S,N, PLTFLG/S,N,PFILE $** 

**2.1-1 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 1** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**23 PRTMSG 24 LABEL 25 GP3** 

**26 PARAM 27 TA1** 

**28 PARAH 29 coNo 30 PURGE 31 oPTPR1 32 LABEL 33 CONO 34 PARA14 35 EQUIV 36 Et4G** 

**37 COND 38 EMA** 

**39 LABEL 40 PURGE 41 COND** 

**42 EMA** 

**43 LABEL 44 COND** 

**45 COND** 

**46 GPWG**   
**PLOTX1// $** 

**PI $** 

**GEOM3,EQEXlN,GEOM2/SLT,GPTT/S,N,NOGRAV/NEVER=l $ /l\*ANO\*/NOFtGG/NOGRAv/V,y,GRDPNT--I $** 

**ECT,EPT,BGPDT,SIL,GPTT,CSTM/EST,GE l,GPECT,,/**   
**LUSET/S,N,NOSIMP/l/S,N,NOGENL/S,N,GENEL $** 

**//\*\~NO\*/NOELMT/NOGENL/NOslMp $** 

**ERRORk,NOELMT $** 

**KGGX,GPST/NOSIMP/OGPST/GENEL $** 

**MPT,EPT,ECT,OIT,EST/OPTPl/S,N,PR lNT/S,N,TSTART/S,N,COUNT $ LOOPTOP $** 

**LBL1,NOSIMP $** 

**//\*ADD\*/NOKGGX/l/O $** 

**oPTPl,oPTP2/NEvER/EsT,EsTl/NEvER $** 

**EST,CSTM,MPT,DIT,GEOM2,/KELM,KDl CT,MEL/l,MDICT,,,/S,N,NOKGGX/ S,N,NOMGG////C,Y, COUPMASS/C,Y,CPBAR/** 

**C,Y,CPROD/C,Y,CPQUADl/C,Y, CPQUA02/C,Y,CPTRIAl/C,Y,CPTRl A2/ C,Y,CPTUBE/C,Y,CPQOPLT/C,Y, CPTRPLT/C,Y,CPTRBSC/ V,Y,VOLUME/V,Y,SURFACE $** 

**JMPKGG,NOKGGX $** 

**GPECT,KO}CT,KELM/KGGX,GPST $** 

**JMPKGG $** 

**f4GG/NOMGG $** 

**JMPMGG,NOMGG $** 

**GPECT,MDICT,MELM/MGG,/-l/C,Y,WTMASS=l .0 $** 

**JMPMGG $** 

**LBL1,GRDPNT $** 

**ERROR2,NOMGG $** 

**BGPOP,CSTM,EQEXlN,/IGG/OGPWG/V,Y,GRDPNT/C,Y,WTMASS $ 2.1-2 (05/30/86)**  
**STATIC ANALYSIS** 

**RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 1** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**41** 

`48 49 50` **51** 

**52** 

**53** 

**54** 

**55** 

**56** 

**57** 

**58** 

**59** 

**60** 

**61** 

**62** 

**63** 

**6k** 

**65** 

**66** 

**67** 

**68** 

**69** 

**10** 

**71**   
**OFP** 

**LABEL EQUIV CONO** 

**SMA3** 

**LABEL PARAM LABEL GPk** 

**CONO** 

**PARAH PURGE** 

**COND** 

**PARAM COND** 

**GPSP** 

**OFP** 

**LABEL EQU\[V COND** 

**HCE1** 

**MCE2** 

**LABEL EQU IV COND**   
**OGPWG,,,,,//S,N,CARDNO $** 

**LBL1 $** 

**KGGX,KGG/NOGENL $** 

**LBLIIA,NOGENL $** 

**GEl,KGGX/KGG/LUSET/NOGENL/NOS IMP $** 

**LBL1lA $** 

**//\*MPY\*/NSK IP/O/O $** 

**LBL1l $** 

**CASECC,GEOM4,EQEX lN,GPDT,BGPDT,CSTM,GPST/RG, YS,USET,ASET/ LUSET/S,N,MPCFl/S,N,MPCF2/S,N,Sl NGLE/S,N,OMIT/S,N,REACT/ S,N,NSKlP/S,N,REPEAT/S,N,NOSET/S,N,NOL/S,N,NOA/C,Y,ASETOUT/ S,Y,AUTOSPC $** 

**ERROR3,NOL $** 

**//\*AND\*/NOSR/SINGLE/REACT $** 

**KRR,KLR,QR,DM/REACT/GM/MPCF l/GO,KOO,LOO,PO ,UOOV,RUOV/OMIT/PS , KFS,KSS/SINGLE/QG/NOSR $** 

**LBL4,GENEL $** 

**//\* EQ\*/GPSPFLG/AUTOSPC/O $** 

**LBL4,GPSPFLG $** 

**GPL,GPST,USET,SIL/OGPST/S,N,NOGPST $** 

**OGPST,,,,,//S,N,CARDNO $** 

**LBL4 $** 

**KGG,KNN/MPCFi $** 

**LBL2,MPCF2 $** 

**USET,RG/GM $** 

**USET,GM,KGG,,,/KNN,,, $** 

**LBL2 $** 

**KNN,KFF/SINGLE $** 

**LBL3,SINGLE $** 

**2.1-3 (05/30/86)**

**DISPLACEMENT RIGID FORMATS** 

**RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 1** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**72 SCE1** 

`73` **LABEL 74 EQUIV 75 COND** 

**76 S14PI 77 LABEL 78 EQtJIV 79 COUD** 

**80 RBMG1 81 LABEL 82 RBMG2 83 CONO** 

**8k RBMG3** `85` **LABEL 86 SSG1** 

**87 EQUIV 88 CONO 89 SSG2 90 LABEL 91 SSG3** 

**92 “COND** `93` **MATGPR 94 MATGPR 95 LABEL 96 SDRI**   
**USET,KNN,,./KFF,KFS,KSS,,, $** 

**LBL3 $** 

**KFF,KAA/OMiT $** 

**LBL5,0MIT $** 

**USET,KFF,,,/GO,KAA,KOO,LOO, ,,,, $** 

**LBL5 $** 

**KAA,KLL/REA.CT $** 

**LBL6,REACT $** 

**USET,KAA,/KLL,KLR,KRR,,, $** 

**LBL6 $** 

**KLL/LLL $** 

**LBL7,REACT $** 

**LLL,KLR,KRR/DM $** 

**LBL7 $** 

**SLT,BGPDT,CSTM,SIL,EST,MPT,GPTT, EDT,MGG,CASECC,OIT,/PG,,,,/ LUSET/NSKIP’ $** 

**PG,PL/NOSET $** 

**LBL1O,NOSET $** 

**USET,GM,YS,KFS,GO,OM,PG/QR,PO,PS,PL $** 

**LBL1O $** 

**LLL,KLL,PL,LOO,KOO,PO/ULV,UOOV,RULV,RUOV/OMlT/V,Y, iRES=-1/ NSKIP/S,N,EPSl $** 

**LBL9,1RES $** 

**GPL,USET,SIL,RULV//\*L\* $** 

**GPL,USET,SIL,RUOV//\*O\* $** 

**LBL9 $** 

**USET,PG,ULV,UOOV,YS,GO,GM,PS, KFS,KSS,QR/UGV,PGG,QG/NSKIP/ \*sTATlcs\* $** 

**2.1-4 (05/30/86)**  
**STATIC ANALYSIS** 

**RIGID FORMAT OMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 1** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**97 COND 98 REPT 99 JUMP** 

**100 PARAM 101 COND 102 LABEL 103 GPFDR** 

**104 OFP 105 COND 106 EQMCK** 

**107 OFP 108 LABEL 109 SOR2** 

**110 COND 111 CURV** 

**112 LABEL 113 PURGE llk COND 115 SOR2** 

**116 COND 117 CURV** 

**118 LABEL 119 PURGE**   
**LBL8,REPEAT $** 

**LBL11,360 $** 

**ERROR1 $** 

**//\*NoT\*/TEST/REPEAT $** 

**ERROR5,TEST $** 

**LBL8 $** 

**CASECC,UGV,KELM,KDICT,ECT,EQEX lN,GPECT,PGG,QG/ONRGYl,DGPFBl/ \*sTATlcs\* $** 

**ONRGY1,OGPFB1 ,,,,//S,N,CARONO $** 

**NOMPCF,GROEQ $** 

**CASECC,EQEXIN,GPL,BGPDT,SI L,USET,KGG,GM,UGV,PGG,QG,CSTM/ OQMl/V,Y,OPT=O/V,Y,GRDEQ/NSK IP $** 

**OQMl,,,,,//S,N,CARDNO $** 

**NOMPCF $** 

**CASECC, CSTM,MPT,DIT,EQEX IN, SIL,GPTT, EDT,BGPDP, ,QG, UGV,EST, XYCOB,PGG/OPGl ,OQG1,OUGV1,OES1 ,OEFl,PUGV1/\*STATICS\*/S,N, NosoRT2/-l/s,N,sTRNFLG $** 

**LBLSTRS,STRESS $** 

**OESl,MPT,CSTM,EST,SIL,GPL/OESIM,OES lG/V,Y,STRESS/ V,Y,NINTPTS $** 

**LBLSTRS $** 

**OESIM/STRESS $** 

**LBLSTRN,STRNFLG $** 

**,CASECC,CSTM,MPT,OIT,EQEXIN ,SIL,GPTT,EDT,BGPDT, ,,UGV,EST, ,/ ,,,OESIA,,/\*STATICS\*//l $** 

**LBLSTRN,STRAIN $** 

**OESIA,MPT,CSTM,EST,SIL,GPL/OES lAM,OESIAG/V,Y,STRAIN/ V,Y,NINTPTS $** 

**LBLSTRN $** 

**OESIA/STRNFLG $** 

**2.1-5 (05/30/86)**

**DISPLACEMENT RIGID FORMATS** 

**RIGID FORMAT OMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGIO FORMAT 1** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**120 COND 121 SOR3 122 PARAM 123 COND 124 OFP** 

**125 SCAN 126 OFP** 

**127 JUMP 128 LABEL 129 oFP** 

**130 SCAN 131 OFP** 

**132 LABEL 133 OFP** 

**134 XYTRAN** 

**135 XYPLOT 136 JUMP 137 LABEL 138 PURGE 139 COND 140 0PTPR2** 

**141 EQUIV 142 COND 143 LABEL 144 OFP**   
**LBL17,NosoRT2 $** 

**ouGvl,oPGl,oQGl,oEFl,oEsl,/ouGv2 ,0PG2,0QG2,0EF2,0ES2, $** 

**//\*suB\*/pRTsoRTz/NosoRT2/I $** 

**LBLSORT1,PRTSORT2 $** 

**0UGV2,0PG2,0QG2,0EF2,0ES2,//S,N, CARDNO $** 

**CASECC,0ES2,0EF2/OESF2/\*RF\* $** 

**0ESF2 ,,,,,//S,N,CARDNO $** 

**LBLXYPLT $**   
**I**   
**LBLSORT1 $** 

**OUGVl,OPGl,OQGl,OEFl,OESl,//S,N,CARDNO $** 

**CASECC,OESl,OEFl/OESFl/\*RF\* $** 

**OESF 1,,,,,/lS,N,CARDNO $** 

**LBLXYPLT $** 

**OESIM,OESIG,OESIA,OESIAM,OESIAG,//S,N, CARDNO $** 

**xYcDB,oPG2,oQG2,ouGv2,oEs2,oEF2/xYPLTT/\*TRAN\*/\*PsET\*/s,N,**   
**PFILE/S,N,CARONO $** 

**XYPLTT// $** 

**DPLOT $** 

**LBL17 $** 

**ouGv2/NosoRT2 $** 

**LBLOFP,COUNT $** 

**OPTPl,OESl,EST/OPTP2,ESTl/S,N,PRlNT/TSTART/S,N,COUNT/S, N,**   
**CARONO $** 

**EsTl,EsT/ALwAYs/oPTP2,0PTPl/ALwAYs $** 

**LOOPENO,PRINT $** 

**LBLOFP $** 

**OUGVl,OPGl,OQGl,OEFl,OESl,//S,N,CARDNO $** 

**2.1-6 (05/30/86)**

**STATIC ANALYSIS** 

**RIGID FORMAT DMAP LISTING**   
**APRIL Ig86 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT I** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**lk5 SCAN** 

**146 OFP** 

**147 OFP** 

**148 LABEL 149 CONO** 

**150 PLOT** 

**151 PRTMSG )52 LABEL 153 LABEL 154 COND** 

**155 REPT** 

**156 JUMP** 

**157 LABEL 158 PRTPARM 159 LABEL 160 PRTPARM 161 LABEL 162 PRTPARM 163 LABEL 164 PRTPARM 165 LABEL**   
**CASECC,OESl,OEF1/OESFIX/\*RF\* $** 

**OESFIX,,,,,//S,N;CARDNO $** 

**OESIM,OESIG,OESIA,OESIAM,OESIAG,//S,N,CARONO $ OPLOT $** 

**P2,JUMPPLOT $** 

**PLTPAR,GPSETS, ELSETS,CASECC,BGPDT,EQEXIN,SI P,PUGVl,,GPECT,OESl/ PLoTx2/NsIL/LuSEP/JUMPPLOT/PLTFLG/S,N,PF ILE $** 

**PLoTx2// $** 

**P2 $** 

**LOOPENO $** 

**FINIS,COUNT $** 

**LOOPTOP,360 $** 

**FINIS $** 

**ERROR1 $** 

**//-l/\*STATICS\* $** 

**ERROR2 $** 

**//-2/\*sTATlcs\* $** 

**ERROR3 $** 

**//-3/\*sTATlcs\* $** 

**ERROR4 $** 

**//-4/\*sTATlcs\* s** 

**ERROR5 $** 

**166 PRTPARM //-5/\*STATlcs\* $** 

**167 LABEL FINIS $** 

**168 PURGE OUMMY/ALWAYS $** 

**169 LABEL LBLINT02 $** 

**170 CO14PON LBLINT01,SYS21 $** 

`2.1-7`**(05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**RIGID FDRMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGIO FORMAT 1** 

**LEVEL 2.0 NASTRAN OMAP COMPILER \- SOURCE LISTING** 

**224 LABEL LBLINT1 $** 

**225 END $** 

**2.1-8 (05/30/86)**  
**STATIC ANALYSIS** 

**2.1.2 Description of Important DMAP Operations for Static Analysis** 

**Note: The DMAP sequence for static analysis involves the use of parameters INTERACT and ml (see Section 2.1.5), These parameters are of relevance only when the primary purpose of the user is to make interactive restart runs. (The two parameters are then specified via the PARAM card in the Bulk Data Deck.) However, these two parameters are not required for normal non-interactive batch runs. Consequently, the rigid format DMAP listing shown in Section 2.1.1 was generated by not specifying these parameters (via the PARAM bulk data card).** AS a result., the **COMPOF\~nd COMPON instructions using these parameters assume a value of O for these parameters (see Volume I, Section 5.7).** 

**6\. COMPOFF causes the DMAP compiler to compile the next instruction (DMAP No. 7\) as the parameter INTERACT is O (see Note above).** 

**8\. COMPON causes the DMAP compiler to skip the compilation of the next instruction (DMAP No. 9, not shown) as the parameter INTERACT is O (see Note above).** 

**10\. CklMPOFFcauses the DMAP compiler to compile all of the following instructions through LABEL LBLINT02 (DMAP Nos. 11 through 169\) as the parameter SYS21 is O (see Note above).** 

**11, GP1 generates coordinate system transformation matrices, tables of grid point locations, and tables relating the internal and external grid point numbers.** 

**12\. PLTTRAN modifies special scalar grid points in the BGPDT and SIL tables. 13\. GP2 generates Element Connection Table with internal indices.** 

**16\. Go to DMAP No. 24 if there are no structure plot requests.** 

**17\. PLTStr transforms user input into a form used to drive the structure plotter. 18, PRTMSG prints error messages associated with the structure plotter.** 

**21\. Go to DMAP No. 24 if no undeformed structure plots are requested,** 

**22\. PLOT generates all requested undeformed structure plots.** 

**23\. PRTMSG prints plotter data and engineering data for each undeformed plot generated. 25\. GP3 generates Static Loads Table and Grid Point Temperature Table.** 

**27\. TA1 generates element tables for use in matrix assembly and stress recovery. 29\. Go to DMAP No. 163 and print Error Message No. 4 if no elements have been defined. 31\. i3PTPRlperforms phase one property optimization and initialization check. 32\. Beginning of loop for property optimization,** 

**33\. Go to DMAP No, 48 if there are no structural elements.** 

**36\. ‘EMGgenerates structural element stiffness and mass matrix tables and dictionaries for later assembly,by the EMA module.** 

**37\. Go to DMAP No. 39 if no stiffness matrix is to be assembled.** 

**38\. EMA assembles stiffness matrix \[K\~g\] and Grid Point Singularity Table. 41\. Go to DMAP No. 43 if no mass matrix is to be assembled.** 

**42\. EMA assembles mass matrix \[Mgg\].** 

**44\. Go to DMAP No. 48 if no weight and balance information is requested.** 

**45\. Go to DMAP No. 159 and print Error Message No. 2 if no mass matrix exists. 2.1-9 (05/30/86)**

**DISPLACEMENT RIGID FORMATS** 

**46\. GPWG generates weight and balance information.** 

**47\. klFPformats the weight and balance information prepared by GPWG and places it on the system output file for printing.m** 

**49\.**   
**Equivalence \[K\~g\] to \[Kgg\] if no general elements exist.** 

**Go to DMAP No. 52 if no general elements exist.**   
**50\.** 

**51\.**   
**SMA3 adds general elements to \[K\~g\] to obtain stiffness matrix \[Kgg\].** 

**Beginning of loop for multiple constraint sets.**   
**54\.** 

**GP4 generates flags defining members of various displacement sets (USET), forms multipoint**   
**55\.**   
**constraint equations \[Rg\] {ug} \= O and forms enforced displacement vector {Ys}.** 

**Go to DMAP No. 161 and print Error Message No. 3 if no independent degrees of freedom are**   
**56\.**   
**defined.** 

**59\.**   
**Go to DMAP No. 64 if general elements are present,** 

**61\.**   
**Go to DMAP No. 64 if no potential grid point singularities exist.** 

**62,**   
**GPSP generates a table of potential grid point singularities,** 

**63\.**   
**flFPformats the table of potential grid point singularities prepared by GPSP and places it**   
**1**  
**on the system output ile for printing.** 

**65\.**   
**Equivalence \[Kgg\] to \[Knn\] if no multipoint constraints exist.** 

**66\.**   
**Go to DMAP No. 69 if the MPC set for the current pass is unchanged from that of the previous pass.** 

**67\.**   
**MCE1 partitions multipoint constraint equations \[Rg\] \= \[Rm\~Rn\] and** 

**solves for multipoint constraint transformation matrix \[Gm\] \= \-\[Rm\]-l\[Rn\].** 

**68\. MCE2 partitions stiffness matrix** 

**\[Kgg\] \=** 

**and performs matrix reduction** 

**\[Knn\] \= \[Knm\] \+ \[G:\]\[\\n** \+ **\[\~n\]\[Gm\]**   
\+ **\[G;\]\[Km\]\[Gm\].** 

**70\. Equivalence \[Knn\] 71\. Go to DMAP No. 73**   
**to \[Kfflif no single-point constraints if no single-point constraints exist.**   
**exist.** 

**72\. SCE1 partitions out single-point constraints \[Knn\] \=**\[1**\~fy- ,**   
**Ksf 1 Kss** 

**74\. Equivalence \[Kff\] 75\. Go to DMAP No. 77**   
**to \[Kaa\] if no omitted coordinates if no omitted coordinates exist.** 

**2.1-10 (05/30/86)**   
**exist.**   
**STATIC ANALYSIS** 

**76\. SMP1 partitions constrained stiffness matrix** 

**K IK** 

**\[Kff\] \= ‘a+ N** 

**‘oa I ’00** \[ 

**solves for transformation matrix** \[Gol \= \-\[Kool-l\[Koal **and performs matrix reduction** \[Kaal \= \[Kaal \+ \[K\~al\[Gol . 

**78\. Equivalence \[Kaa\] to 79\. Goto DMAPNo. 81 if**   
**\[KLL\] if no free-body supports exist. no free-body supports exist.** 

**80\. RBMG1**   
**partitions out**   
**free-body supports**\[1**Kkk IKgr**   
**\[Kaa\]= –+– .** 

**‘rt I‘rr** 

**82\. RBMG2 83\. GO to 84\. RBMG3**   
**decomposes constrained stiffness matrix \[KLB\] \= \[LLL\]\[ULR\]. DMAP No. 85 if no free-body supports exist.** 

**forms rigid body transformation matrix** 

**\[D\] \=** \-\[ KLJ1\[Kkr\] , 

**calculates rigid body check matrix** 

\[xl \= \[Krrl \+ \[K;rl\[Dl 

**and calculates rigid body error ratio** 

**e= T14T x.**   
**Krr** 

**86\. SSG1 generates static load vectors {Pg}.** 

**87\. Equivalence {Pgl to {pi} if no constraints are aPpliedO 88\. Go to DMAP No. 90 if no constraints are applied. 89\. SSG2 applies constraints to static load vectors HPn**   
**{Pg}= —– , {Pn} \= {\~n} \+ \[G;\]{pml , Pm** 

**2.1-11 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**(Pf} \= {Pf} \- \[KfJ{YJ ,** 

**(Pa} \= {;a} \+ \[G:\]{PO} ,** 

**and calculates determinate forces of reaction {qr} \= \-{Pr} \- \[DT\]{PLI. 91\. SSG3 solves for displacements of independent coordinates {ui} \= \[KIL\]-l{Pl} ,** 

**solves for displacements of omitted coordinates** 

**{u:} \= \[KOO\]-l{PO} ,** 

**calculates residual vector (RULV) and residual coordinates** 

**{6PL} \= {Pi} \- \[Kli\]{ug}** 

**{u:}{\&Pk}** 

**‘t** ❑ 

**{P:}{ui}**   
**vector error ratio for independent 9** 

**and calculates residual vector (RU@V) and residual vector error ratio for omitted coordinates** 

**{tSPo}= {Po} \- \[Koo\]{u:l ,** 

**\=**   
**‘o**   
**{u:){fsPo? {P:}{u:}**   
**92\. Go to DMAP No. 95 if residual vectors are not to be printed. 93\. MATGPR prints the residual vector for independent coordinates (RULV), 94\. MATGPR prints the residual vector for omitted coordinates (RUOV), 96\. SDR1 recovers dependent displacements**   
**H‘k**   
**—— \= {Ua} , ‘r** 

**HUa**   
**—— \= {Uf} , ‘o**   
**{Uo} \= \[Go\]{ual \+ {u:} , H‘f ——** ❑ **{Un} ,**   
**Y5** 

**2,1-12 (05/30/86)**

**{um} \= \[Gm\]{un} ,**   
**STATIC ANALYSIS H‘n —. \= {Ugl**   
**Um** 

**and recovers single-point forces of constraint** 

{q5} \= \-{p\~} \+\[K\~J{uf} \+ \[K5\~l{y\~}. 

**97\.**   
**Go to DMAP No. 102 if all constraint sets have been processed.** 

**98,**   
**Go to DMAP No. 54 if additional sets of constraints need to be processed.** 

**Go to DMAP No. 157 and print Error Message No. 1 as the number of constraint sets exceeds**   
**99\.**   
**360\.** 

**Go to DMAP No. 165 and print Error Message No. 5 if multiple boundary conditions are**   
**101\.**   
**attempted with an improper subset.** 

**I**  
**103\.**   
**GPFDR calculates the grid point force balance (OGPFB1) and element strain energy** (ONRGyl) **for requested sets.** 

**104,**   
**OFP formats the tables prepared by GPFDR and places them on the system output file for printing.** 

**Go to DMAP No. 108 if no multipoint constraint force balance is requested.**   
**105\.** 

**106\.**   
**EQMCK calculates the force and moment equilibrium check and prepares the multipoint constraint force balance (OQMl) for output.** 

**\!dFP formats the table prepared by EQMCK and places it on the system output file for**   
**107\.**   
**printing.** 

**109\.**   
**SDR2 calculates the element forces (\!3EFI)and stresses (PES1) and prepares load vectors (OPGl), displacement vectors (OUGVl) and single-point forces of constraint (OQGl) for output and translation components of the displacement vectors (PUGV1).** 

**Go to DMAP No. 112 if element stresses in material coordinate system and stresses at the**   
**110\.**   
**connected grid points are not to be calculated.** 

**111\.**   
**CURV calculates element stresses in material coordinate system (\!JESIM)and stresses at the connected grid points (9ES1G).** 

**114\.**   
**Go to DMAP No. 118 if element strains/curvatures are not to be calculated.** 

**115\.**   
**SDR2 calculates element strains/curvatures (\!i3ESlA).** 

**Go to DMAP No. 118 if element strains/curvatures in material coordinate system and**   
**116\.**   
**strains/curvatures at the connected grid points are not to be calculated.** 

**CURV calculates element strains/curvatures in material coordinate system (OESIAM) and**   
**117\.**   
**strains/curvatures at the connected grid points (\!JESIAG).** 

**Go to DMAP No. 137 if there are no requests for output sorted by grid point number or**   
**120\.**   
**element number.** 

**SDR3 prepares requested output sorted by grid point number of element number.**   
**121\.** 

**Go to DMAP No. 128 if printed output sorted by grid point number or element number is not**   
**123\.**   
**required.** 

**@tP formats the tables prepared by SDR3 for output sorted by grid point number or element**   
**124\.**   
**number and places them on the system output file for printing.** 

**2.1-13 (05/30/86)**   
1 

**DISPLACEMENT RIGID FORMATS** 

**125\.**   
**SCAN examines the element stresses and forces calculated by SDR3 and generates scanned output that meets the specifications set by the user.** 

**126,**   
**OFP formats the scanned output table prepared by SCAN and places it on the system output file for printing.** 

**Go to DMAP No. 132\.**   
**127,** 

**13FPformats the tables prepared by SDR2 for output sorted by subcase number and places them**   
**129\.**   
**on the system output file for printing.** 

**SCAN examines the element stresses and forces calculated by SOR2 and generates scanned**   
**130\.**   
**output that meets the specifications set by the user.** 

**@FP formats the scanned output table prepared by SCAN and places it on the system output**   
**131\.**   
**file for printing.** 

**13FPformats the tables prepared by CURV and SDR2 for output sorted by subcase number and**   
**133\.**   
**places them on the system output file for printing.** 

**XYTRAN prepares the input for requested X-Y plots.**   
**134\.** 

**XYPL13T prepares the requested X-Y plots of displacements, forces, stresses, loads and**   
**135\.**   
**single-point forces of constraint vs. subcase.** 

**Go to DMAPNo. 148\.**   
**136\.** 

**Go to DMAP No. 143 if there is no phase two property optimization.**   
**139\.** 

**0PTPR2 performs phase two property optimization.**   
**140\.** 

**Equivalence EST1 to EST and 0PTP2 to OPTP1.**   
**141\.** 

**Go to DMAP No. 153 if no additional output is to be printed for this loop.**   
**142\.** 

**OFP formats the tables prepared by SDR2 for output sorted by subcase number and places them**   
**144\.**   
**on the system output file for printing.** 

**SCAN examines the element stresses and forces calculated by SDR2 and generates scanned**   
**145\.**   
**output that meets the specifications set by the user.** 

**OFP formats the scanned output table prepared by SCAN and places it on the system output**   
**146\.**   
**file for printing.** 

**147\.**   
**\!3FPformats the tables prepared by CURV and SDR2 for output sorted by subcase number and places them on the system output file for printing.** 

**149\. 150\. 151\.**   
**Go to DMAP No. PLOT generates** 

**PRTMSG prints generated.**   
**152 if no deformed structure plots are requested.** 

**all requested deformed structure and contour plots.** 

**plotter data, engineering data, and contour data for each deformed plot**

**154, 155\. 156,**   
**Go to Go to Go to**   
**DMAP No. DMAP No. DMAP No.** 

**167 and make normal exit if property optimization is complete. 32 if additional loops for property optimization are needed. 167 and make normal exit.** 

**158\. 160\. 162,**   
**Print Print Print**   
**Error Message No. 1 and terminate execution. Error Message No. 2 and terminate execution. Error Message No, 3 and terminate execution. 2.1-14 (05/30/86,**   
**STATIC ANALYSIS** 

**164\. Print Error Message No. 4 and terminate execution.**   
● **166\. Print Error Message No. 5 and terminate execution. 170\. C0MP$3Ncauses the \!3MAPcompiler to skip the compilation of al through LABEL LBLINTOI (DMAP Nos. 171 through 223, not shown (see Note at the beginning of this section).** 

**2.1-15 (05/30/86)**  
**of the following instructions as the p\~rameter SYS21 is O**   
**DISPLACEMENT RIGID FORMATS** 

**2.1.3 Output for Static Analysis** 

**The following printed output, sorted by loads (S9RT1) or by grid point number or element number (S\!dRT2),may be requested for Static Analysis solutions:** 

**1\. Displacements and components of static loads and single-point forces of constraint at selected grid points or scalar points.** 

**2\. Forces and stresses in selected elements.** 

**3\. Strains/curvatures in selected elements (only for TRIA1, IRIA2, QUAD1 and QUAD? elements).** 

**The following plotter output may be requested:** 

**1\. Undeformed and deformed plots of the structural model.** 

**2\. Contour plots of stresses and displacements.** 

**3\. X-Y plot of any component of displacement, static load, or single-point force of constraint for a grid point or scalar point versus subcase.** 

**4\. X-Y plot of any stress or force component for an element versus subcase.** 

**2.1.4 Case Control Deck for Static Analysis** 

**The following items relate to subcase definition and data selection for Static Analysis: 1\. A separate subcase must be defined for each unique combination of constraints and static loads.** 

**2\. A static loading condition must be defined for (not necessarily within) each subcase with a LOAD, TEMPERATURE(L\!3AD),or DEF\!3RMselection unless all loading is specified with grid point displacements on SPC cards.** 

**3\. An SPC set must be selected for (not necessarily within) each subcase, unless the model is a properly supported free body, or all constraints are specified on GRIO cards, Scalar Connection cards, or with General Elements.** 

**4, Loading conditions associated with the same sets of constraints should be in contiguous subcases in order to avoid unnecessary looping.** 

**5\. REPCASE may be used to repeat subcases in order to allow multiple sets of the same output item.** 

**2.1.5 Parameters for Static Analysis** 

**The following parameters are used in Static Analysis:** 

**2.1-16 (05/30/86)**  
**STATIC ANALYSIS** 

**ASET@UT \- optional. A positive integer value of ——— 1\.**   
**datiiblock to be generated by the GP4 module. A**   
**this parameter causes the ASET output negative integf;rvdlue or O suppresses** 

**the generation of this output data block. The default value is O.** 

**2\.**   
**AUTffSPC- reserved for future optional use. The default value is \-1. .\_.\_\_\_\_ C@UPMASS \- CPllAR,CPRf)D,CPQUAD1, CPQUAD2, CPTRIA1, CPTRIA2, CPTUBE, CPQDPLT, CPTRPLT, 3\.** 

**CPTRBSC \- optional. These parameters cause the generation of coupled mass matrices rather than lumped mass matrices for all bar elements, rod elements, and plate elements that include bending stiffness.** 

**GRDEQ \- optional. A positive integer value of this parameter selects the grid point —— 4\.**   
**about which equilibrium will be checked for the Case Control output request, MPCFf3RLt. If the integer value is zero, the basic origin is used. The default value is \-1. GRDPNT \- optional. A positive integer value of this parameter causes the Grid Point 5\.** 

**Weight Generator to be executed and the resulting weight and balance information to be printed.** 

**INTERACT \- optional. This parameter, —— 6\.**   
**when the primary purpose of the user**   
**like the SYS21 parameter, is of relevance only is to make interactive restart runs. In such a** 

**case, the integer v\~lue of this parameter must be set to \-1 (via a PARAM bulk data card) in both t.hcbi}t\~hcheckpoint run (that precedes the interactive restart run) as well as in the interactive rest.\~rtrun. If not so specified via a PARAM bulk data card, the CJ3MP(CIFFand C@MPON instructions in the DMAP sequence that use this parameter assume a value of O for this parameter (see Volume I, Section 5.7).** 

**jRES \- optional. A positive integer value of this parameter causes the printing of the 7\.** 

**residual vectors following each execution of the SSG3 module.** 

**\~INTPTS \- optional. A positive integer value of this parameter specifies the number of 8\.** 

**closest independent points to be used in the interpolation for computing stresses or strains/curvatures at grid points (only for TRIA1, TRIA2, QUAD1 and QUAD2 elements). A negative integer value or O specifies that all independent points are to be used in the interpolation. The default value is O.** 

**(4PT- optional. A positive integer value of this parameter causes both equilibrium and 9\.** 

**multipoint constraint forces to be calculated for the Case Control output request, MPCF@RCE, A negative integer value of this parameter causes only the equilibrium force balance to be calculated for the output request. The default value is O which causes only the multipoint constraint forces to be calculated for the output request. 2.1-17 (05/30/86)**

**10\.**   
**STRAIN \- optional. This**   
**DISPLACEMENT RIGID FORMATS** 

**parameter controls the transformat on of element** 

**strains/curvatures to the material coordinate system (only for TRIA1, TRIA2, QUAD1 and QUAD2 elements). If it is a positive integer, the strains/curvatures for these elements are transformed to the material coordinate system. If it is zero, strains/curvatures at the connected grid points are also computed in addition to the element strains/curvatures in the material coordinate system. A negative integer vtilueresults in no transformation of the strains/curvatures. The default value is \-1. 11,**   
**STRESS \- optional. This parameter controls the transformation of element stresses to the material coordinate system (only for TRIA1, TRIA2, QUAD1 and QUAD2 elements). If it is a positive integer, the stresses for these elements are transformed to the material coordinate system. If it is zero, stresses at the connected grid points are also computed in addition to the element stresses in the material coordinate system. A negative integer value results in no transformation of the stresses. The default value is \-1,** 

**12\.**   
**SURFACE \- optional. The computations of the external surface areas for the —— two-dimensional and three-dimensional elements are activated by this parameter when they are generated in the EMG module. The results are multiplied by the real value of this parameter. See the description under the PARAM bulk data card for details. SYS21 \- optional. This parameter, like the INTERACT parameter, is of relevance only 13\.** 

**when the primary purpose of the user is to make interactive restart runs. In such a case, the integer value of this parameter must be set to \-1 (via a PARAM bulk data card) in the interactive restart run (that follows a batch checkpoint run). Ifnot so specified via a PARAM bulk data card, the COMPOFF and COMPON instructions in the DMAP sequence that use this parameter assume a value of O for this parameter (see Volume I, Section 5.7).** 

**VOLUME \- optional. The volume computations for the two-dimensional and 14\.** 

**three-dimensional elements are activated by this parameter when they are generated in the EMG module. The results are multiplied by the real value of this parameter. See the description under the PARAM bulk data card for details.** 

**WTMASS \- optional. The terms of the mass matrix are multiplied by the real value of —-. 15,**   
**this parameter when they are generated in the EMA module.** 

**2.1-18 (05/30/86)**

**STATIC ANALYSIS** 

**2.1.6 Automatic ALTERs for Automated Multi-stage Substructuring** 

**The following lines substructure analyses. Phase 1: 5, 56,**   
**of the Static Analysis, Rigid Format 1, are ALTERed for automated 78-85, 87-153**   
**Phase 2: 5, 11-11, 14-24, 28-29, 35-35, 49-52, 59-64, 103-153** 

**Phase 3: 78-85, 88-95, 96** 

**If APP DISP, SU8S is used, the user may also specify ALTERs. However, these must not interfere with the automatically generated DMAP statement ALTERs listed above. See Volume I, Section 5.9 for a description and listing of the ALTERs which are automatically generated for substructuring.** 

**2.1.7 Rigid Format Error Messages from Static Analysis** 

**The following fatal errors are detected by the DMAP statements in the Static Analysis rigid format. The text for each error message is given below in capital letters and is followed by additional explanatory material, including suggestions for remedial action.** 

**STATIC ANALYSIS ERROR MESSAGE NO. 1 \- ATTEMPT TO EXECUTE MORE THAN 360 L\!30PS.** 

**An attempt has been made to use more than 360 different sets of boundary conditions or more than 360 passes in the optimization loop have been attempted. This number may be increased by ALTERing the REPT instruction following SDR1 in the former case and the REPT instruction following the last PRTMSG instruction in the latter case.** 

**STATIC ANALYSIS ERRklRMESSAGE NO. 2 \- MASS MATRIX REQUIRED FOR WEIGHT AND BALANCE CALCULATIONS,** 

**The mass matrix is null because either no elements were defined with Connection cards, nonstructural mass was not defined on a Property card, or the density was not defined on a Material card.** 

**STATIC ANALYSIS ERROR MESSAGE NO. 3 \- NO INDEPENDENT DEGREES OF** FREEDOMHAVEBEENDEFINED. 

**Either no degrees of freedom have been defined on GRID, SP131NTor Scalar Connection cards, or all defined degrees of freedom have been constrained by SPC, MPC, SUP@RT, OMIT or GRDSET cards, or grounded on Scalar Connection cards.** 

**STATIC ANALYSIS ERROR MESSAGE N@. 4 \- NO ELEMENTS HAVE BEEN DEFINED.** 

**No elements have been defined with either Connection cards or GENEL cards.** 

**STATIC ANALYSIS ERROR MESSAGE NO. 5 \- A LOOPING pROBLEM RUN ON A NON-LOOpING SUBSET.** 

**A problem requiring boundary condition changes was run on subset 1 or 3\. The problem should be restarted on subset O.** 

**2.1-19 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS 2.1-20 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**2.2 STATIC ANALYSIS WITH INERTIA RELIEF** 

**2.2.1 DMAP Sequence for Static Analysis With Inertia Relief** 

**RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 2** 

**LEVEL 2.o NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**OPTIONS IN EFFECT GO ERR=2 LIST NOOECK NOREF NOOSCAR \--------- \-------- \-** 

**1 BEGIN** 

**2 PRECHK** 

**3 FILE** 

**4 PARAM** 

**5 GPI** 

**6 PLTTRAN 7 GP2** 

**8 PARAML** 

**9 PURGE** 

**10 COND** 

**?1 PLTSET** 

**12 PRTMSG 13 PARAM lk PARAN 15 COND** 

**16 PLOT** 

**17 PR’TMSG \~8 LABEL 19 GP3** 

**20 TA1** 

**21 COND**   
**DISP02 \- STATIC ANALYSIS WITH INERTIA RELIEF \- APR. 1986 $ ALL $** 

**QG=APPENO/PGG=APPEND/UGV=APPEND/GMESAVE/KNN=SAVE/MNN=SAVE $ //\*MPY\*/CARDNO/O/O $** 

**GEOMl,GEOM2,/GPL,EQEXIN,GPDT,CSTM, BGPOT,SIL/S,N,LUSET/ NOGPDT/ALWAYS=-l $** 

**BGPDT,SIL/BGPOP,SIP/LUSET/S,N, LUSEP $** 

**GEoM2,EQExlN/EcT $** 

**PCDB//\~\~PREs\*////JuMppLoT $** 

**PLTSETX,PLTP.4R,GPSETS,ELSETS/JUHPPLOT $** 

**P1,JUMPPLOT $** 

**PCOB,EQEXIN,ECT/PLTSETX,PLTPAR,GPSETS ,ELSETS/S,N,NSIL/ S,N,JUMPPLOT S** 

**PLTSETX// $** 

**//\*Mpy\~,/pLTFLG/i/l $** 

**//\*MPv\~f/PFILE/O/O $** 

**P1,JUMPPLOT $** 

**PLTPAR,GPSETS, ELSETS,CASECC, BGPDT,EQEXIN,SIL,,ECT,,/PLOTXl/ NSIL/LUSET/S,N,JUMPPLOT/S,N ,PLTFLG/S,N,PFILE $** 

**PLOTX1// $** 

**PI $** 

**GEoM3.EQExlN,GEoM2/sLT$GpTT/NoGRAv $** 

**ECT,EPT,BGPDT,SIL,GPTT,CSTM/EST ,GEl,GPECT,,/**   
**LUSET/S,N,NOSIMP/l/S,N,NOGENL/S .N,GENEL $** 

**ERROR6,NOSIMP $** 

**2.2-1 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 2** 

**LEVEL 2.0 NASTRAN OMAP COMPILER \- SOURCE LISTING** 

**22** 

**23** 

**24** 

**25** 

**26** 

**27** 

**28** 

**29** 

`30` **31** 

**32** 

**33** 

**34** 

**35** 

**36** 

**37** 

**38** 

**39** 

**40** 

**41** 

**42** 

**43** 

**4k**   
**PURGE PARAM PARAM EMG** 

**PURGE COND** 

**EMA** 

**LABEL COND** 

**EMA** 

**COND** 

**GPWG** 

**OFP** 

**LABEL EQUIV COND** 

**SMA3** 

**LABEL PARAM LABEL GP4** 

**COND** 

**COND**   
**OGPST/GENEL $** 

**//\*ADD\* /NoKGGx/l /o $** 

**//\*ADD\*/NoMGG/l/o $** 

**EST,CSTM,MPT,DlT,GEOM2,/KELM, KDICT,MELM,MDICT,,,/S,N,NOKGGX/ S,N,NOMGG////C,Y,COUPMAC,/C, Y,CPBAR/** 

**c,Y,cPRoD/c,Y,cPQuAol/c,Y,cPQuAD2/c, Y,cPTRIA1/c,Y,cPTRlA2/ C,Y,CPTUBE/C,Y,CPQOPLT/C,Y,CPTRPLT/C,Y, CPTRBSC/ V,Y,VOLUME/V,Y,SURFACE $** 

**KGGX,GPST/NOKGGX $** 

**JMPKGG,NOKGGX $** 

**GPECT,KDICT,KELM/KGGX,GPST $** 

**JMPKGG $** 

**ERROR1,NOMGG $** 

**GPECT,MDICT,MELM/MGG,/-l/C,Y,WTMASS=l .0 $** 

**LGPWG,GRDPNT $** 

**BGPDP,CSTM,EQEXIN,MGG/OGPWG/V, Y.GROPNT=-I/C.Y.WTMASS $ OGPWG ,,,,,//S\!N,CARDNO $** 

**LGPWG $** 

**KGGX,KGG/NOGENL $** 

**LBL1lA,NOGENL $** 

**GEl,KGGX/KGG/LUSET/NOGENL/NOS lMP $** 

**LBLIIA $** 

**//\*Mpy\*/NsKIp/o/o $** 

**LBLII $** 

**CASECC,GEOM4,EQEXIN,GPDT,BGPDT ,CSTM,GPST/RG,YS,USET,ASET/ LUSET/S,N,MPCFl/S,N,MPCF2/S ,N,SINGLE/S,N,OMIT/S,N,REACT/ S,N,NSKIP/S,N,REPEAT/S,N,NOSET/S, N,NOL/S,N,NOA/C,Y,ASETOUT/ S,Y,AUTOSPC $** 

**ERROR3,NOL $** 

**ERROR4,REACT $** 

**2.2-2 (05/30/86)**  
**STATIC ANALYSIS WITH INERTIA RELIEF** 

**e RIGID FORMAT OMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 2** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**k5 PURGE**   
**GM/MPCFl/GO,KOO,LOO,MOO,MOA, PO,UOOV,RUOV/OMIT/KSS,KFS, PS/ SINGLE $** 

**k6 k7 48 49 50 51 52 53 54**   
**CONO PARAH CONO GPSP OFP** 

**LABEL EQUIV CONO NCE 1**   
**LBL4,GENEL $ “** 

**//\*EQ\*/GPSPFLG/AUTOSPC/O $** 

**LBLk,GPSPFLG $** 

**GPL,GPST,USET,SIL/OGPST/S,N,NOGPST $ OGPST ,,,,,//S,N,CARDNO $** 

**LBL4 $** 

**KGG,KNN/MPCFl/MGG,MNN/MPCFl $ LBL2,MPCF2 $** 

**USET,RG/Gll $** 

**55 MCE2 56 LABEL 57 EQUIV**   
**USET,GM,KGG,MGG,,/KNN,MNN, , $ LBL2 s** 

**KNN,KFF/SINGLE/MNN,MFF/SINGLE $** 

**58 59 60 61 62 63 64 65 66 67 68 69**   
**COND** 

**SCE 1 LABEL EQUIV COND** 

**SMP 1 LABEL RBMG 1 RBMG2 RBMG3 RBMG4 SSG1**   
**LBL3,SINGLE $** 

**USET,KNN,MNN,,/KFF,KFS,KSS,MFF ,, $** 

**LBL3 $** 

**KFF,KAA/OMIT/ MFF,MAA/OMIT $** 

**LBL5,0MIT $** 

**USET,KFF,MFF,,/GO,KAA,KOO, LOO,MAA,MOO,MOA, , $ LBL5 $** 

**USET,KAA,MAA/KLL,KLR,KRR,MLL,MLR,MRR s** 

**KLL/LLL $** 

**LLL,KLR,KRR/DM $** 

**DM,MLL,MLR,MRR/MR $** 

**SLT,BGPOT,CSTM,SIL,EST,MPT, GPTT,EDT,MGG,CASECC,DIT,/PG, ,,,/ LUSET/NSKIP $** 

**2.2-3 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 2** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**70 SSG2 71 SSGk 72 ssG3** 

**73 COND 74 MATGPR 75 MATGPR 76 LABEL 77 SOR1** 

**78 CONO 79 REPT 80 JUMP 81 PARAM** 

**82 COND 83 LABEL 84 CDND 85 EQMCK** 

**86 OFP 87 LABEL 88 SDR2** 

**89 OFP 90 SCAN 91 OFP 92 coNo 93 PLOT**   
**USET,GM,YS,KFS,GO,DM,PG/QR,PO,PS, PL $** 

**PL,QR,PO,MR,MLR,OM,MLL,MOO,MOA,GO,USET/pL I,pO\~/OM\~T $** 

**LLL,KLL,PLl,LOO,KOO,POl/ULV, UOOV,RULV,RUOV/OMIT/V,Y, lRES=-1/NSKIP/S,N,EPSl $** 

**LBL9,1RES $** 

**GPL,USET,SIL,RULV//\*L\* $** 

**GPL,USET,SIL,RUOV//\*O\* $** 

**LBL9 $** 

**USET,PG,ULV,UOOV,YS,GO,GM,PS ,KFS,KSS,QR/UGV,PGG,QG/NSKIP/ \*sTATlcs\* $** 

**LBL8,REPEAT $** 

**LBL1l ,360 $** 

**ERROR2 $** 

**//\*NoTf\</TEsT/REpEAT $** 

**ERROR5,TEST $** 

**LBL8 $** 

**NOMPCF,GRDEQ $** 

**CASECC, EQEXIN,GPL,BGPDT,SIL, USET,KGG,GM,UGV,PGG,QG,CSTM/ OQMl/V,Y,OPT=O/V,Y,GRDEQ/NSK 1P $** 

**OQMl,,,,,//S,N,CARDNO $** 

**NDMPCF $** 

**CASECC,CSTM,MPT,DIT,EQEXIN, SIL,GPTT,EDT,BGPDP, ,QG,LIGV,EST,,PGG/ OPG1,OQG1,OUGV1,OESI,OEF1, PUGV1/fSTATICS\~\< $** 

**OUGVl,OPGl,OQGl,OEFl,OESl,//S,N ,CARDNO $** 

**CASECC,OESl,OEF1/OESFl/\*RF\~: $** 

**OESF 1,,,,,//S,N,CARDNO $** 

**P2,JUMPPLOT $** 

**PLTPAR,GPSETS, ELSETS,CASECC, BGPOT, EQEXIN,S IP,PUGV1, ,GPECT,OES 1/ PLOTX2/NSlL/LUSEP/JUMPPLOT/PLTFLG/S,N,PF ILE $** 

**2.2-4 (05/30/86)**  
**STATIC ANALYSIS WITH INERTIA RELIEF** 

**e RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGIO FORMAT 2** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**94 PRTMSG PLoTx2// $** 

**95 LABEL P2 $** 

**g6 JUMP FINIS $** 

**97 LABEL ERROR\] $** 

**98 PRTPARM //-1/\*lNERTIA\* $** 

**99 LABEL ERROR2 $** 

**100 PRTPAR\!4 //-2/\*lNERTIA\* $** 

**101 LABEL ERROR3 $** 

**102 PRTPARM //-3/\*lNERTIA\~’r $** 

**103 LABEL ERROR4 $**   
**m 105 LABEL ERROR5 $**   
**104 PRTPARM //-4/\*lNERTIA\* $** 

**106 PRTPARM //-5/\>\~lNERTIA\* $** 

**107 LABEL ERROR6 s** 

**108 PRTPARM //-6/:\<lNERTIA\~\~ $** 

**109 LABEL FINIS $** 

**110 PURGE DUM\!4Y/ALWAYS $** 

**111 END $** 

**2.2-5 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**2.2,2 Description of Important DMAP Operations for Static Analysis with Inertia Relief** 

**5, GP1 generates coordinate system transformation matrices, tables of grid point locations, and tables relating the internal and external grid point numbers. a** 

**6\. PLTTRAN modifies special scalar grid points in the BGPDT and SIL tables.** 

**7\. GP2 generates Element Connection Table with internal indices,** 

**10, Go to DMAP No. 18 if there are no structure plot requests,** 

**11\. PLTSET transforms user input into a form used to drive the structure plotter. 12\. PRTMSG prints error messages associated with the structure plotter.** 

**15\. Go to DMAP No. 18 if no undeformed structure plots are requested,** 

**16\. PL17Tgenerates all requested undeformed structure plots.** 

**17\. PRTMSG prints plotter data and engineering data for each undeformed plot generated. 19\. GP3 generates Static Loads Table and Grid Point Temperature Table.** 

**20\. TA1 generates element tables for use in matrix assembly and stress recovery. 21\. Go to DMAP No. 107 and print Error Message No. 6 if there are no structural elements.** 

**25, EMG generates structural element stiffness and mass matrix tables and dictionaries for later assembly by the EMA module.** 

**27\. Go to DMAP No. ’29if no stiffness matrix is to be assembled.** 

**28\. EMA assembles stiffness matrix \[K&\] and Grid Point Singularity Table.** 

**30\. Go to DMAP No. 97 and print Error Message No, 1 if no mass matrix is to be assembled. 31\. EMA assembles mass matrix \[Mgg\].** 

**32\. Go to DMAP No. 35 if no weight and balance information is requested.** 

**33\. GPWG generates weight and balance information.** 

**34\. @FP formats the weight and balance information prepared by GPWG and places it on the system output file for printing.** 

**36\. Equivalence \[K\~g\] to \[Kgg\] if no general elements exist.** 

**37\. Go to DMAP No. 39 if no general elements exist,** 

**38\. SMA3 adds general elements to \[K\~g\] to obtain stiffness matrix \[Kgg\].** 

**41\. Beginning of loop for multiple constraint sets.** 

**42\. GP4 generates flags defining members of various displacement sets (USET), forms multipoint constraint equations \[Rg\]{ug} \= O and forms enforced displacement vector {Ys}.** 

**43\. Go to DMAP No. 10land print Error Message No. 3 if no independent degrees of freedom are defined.** 

**44\. Go to DMAP No. 103 and print Error Message No. 4 if no free-body supports exist. 46\. Go to DMAP No. 51 if general elements are present.** 

**2.2-6 (05/30/86)**  
**STATIC ANALYSIS WITH INERTIA RELIEF** 

**Go to DMAP No. 51 if no potential grid point singularities exist.**   
**48\.** 

**GPSP generates a table of potential grid point singularities.**   
**49\.** 

**50\.**   
**\!3FP formats the table of potential grid point singularities prepared by GPSP and places it on the system output file for printing.** 

**Equivalence \[Kgg\] to \[Knn\] and \[Mgg\] to \[Mnn\] if no multipoint constraints exist. 52\.** 

**Go to DMAP No. 56 if the MPC set for the current pass is unchanged from that of the previous**   
**53\.**   
**pass.** 

**MCEI partitions multipoint constraint equations** \[Rgl \= \[Rm\~Rnl **and solves for**   
**54\.**   
**.** 

**multipoint constraint transformation matrix \[Gm\] \= \-\[Rm\]-l\[Rn\].** 

**MCE2 partitions stiffness and mass matrices**   
**55\.** 

**and performs matrix reductions** 

**\[Knn\] \= \[iinn\]+** \[G$\[\\nl \+ \[\~nl\[Gml \+ \[G\~l\[$JIGml and 

**\[Mnn\] \= \[;nn\] \+** \[Gj\[Mmnl \+ \[M;nl\[Gml \+ \[G; IIMJIGMI. 

**Equivalence** \[Knnl **to \[Kff\] and** \[Mnnl to \[Mff\] **if no sin91e-Point constraints exist” 57\.** 

**Go to DMAP No. 60 if no single-point constraints exist.**   
**58\.** 

**SCE1 partitions out single-point constraints**   
**59\.**   
\[1**‘ff’ ‘fs \[Knn\] \= – \+ – and** \[1 **\[Mnn\] \= ‘ff \~‘fs**   
**‘Sf I ‘ss ‘Sf I‘ss** 

**Equivalence \[Kff\] to** \[Kaal and \[Mff\] to \[Maal **if no omitted 61\.** 

**GO to DMAP No. 64 if no omitted coordinates exist. 62\.**   
. 

**coordinates exist.** 

**63\.**   
**SMP1 partitions constrained stiffness** \[1**\~ lKao**   
**\[Kffl \= \~\~K– and**   
**and mass matrices** I**M IMao**   
**\[Mff\] \= \&a+ —** 

**oa 00**   
**L**   
**‘oa 1’00** 

**solves for transformation matrix \[Go\]**   
**\= \-\[ Koo\]-l\[Koa\]** 

**and performs matrix reductions** \[Kaal \= \[iaal \+ \[K\~al\[Gol **2.2-7 (05/30/86)**

**and** 

**65\. RBMG1** 

**66\. RBMG2 67\. RBMG3**   
**DISPLACEMENT RIGID FORMATS** 

**\[Maa\]** ❑ **\[;aa\] \+ \[M\~a\]\[Go\] \+ \[G\~\]\[Moa\] \+ \[G\~\]\[Moo\]\[Go\] . partitions out free-body supports** 

**decomposes constrained stiffness matrix \[Klg\] \= \[LIL\]\[ULL\], forms rigid body transformation matrix** 

**\[D\] \= \-\[KLl\]-l\[Kir\] ,** 

**calculates rigid body check matrix** 

**\[X\] \= \[Krr\] \+ \[K:r\]\[D\]** 

**and calculates rigid body error ratio** 

**l-l-%Krr**   
\~= **x** 

**68\. RBMG4 forms rigid body mass matrix** 

\[mr\] \= \[Mrr\] \+ \[M\~rl\[Dl \+ \[DTl\[MLrl \+ \[DTIIMLLIIDI. **69\. SSG1 generates static load vectors {Pg}.** 

**70\. SSG2 applies constraints to static load vectors HEn**   
**{Pg}= —– , {Pnl \= {\~n} \+ \[G:\]{Pm} ,**   
**Pm** 

**‘f {Pn}’ —– , {Pf} \= {Pf} \- \[Kfs\]{ys} ,** 

**11**   
**P5 ia**   
**{Pf}= —– , {Pa} \= {Pa} \+ \[G;\]{PO} ,** 

**\[1**   
**P.** 

**HP**   
**{Pa} \= —L**   
**Pr** 

**and calculates determinate forces of reaction {qr} \= \-{Pr} \- \[DT\]{Pi}. 2.2-8 (05/30/86)**

**71\.**   
**SSG4 calculates inertia**   
**STATIC ANALYSIS WITH INERTIA RELIEF loads and combines therewith static loads** 

**0** 

**72,**   
**(‘E ‘r) and {P\]I \= {Pil \+ \[M \]\[D\] \+ \[M \] \[mr\]-l{qr}**   
**‘p:’={’o’+\~“J\[GJ+\[Mq** H **“\[mr\]-’{qr’ \~ SSG3 solves for displacements of independent coordinates** 

**{uL} \= \[KLL\]-l{P:} ,** 

**solves for displacements of omitted coordinates** 

{u:} \= \[Kool-b) , 

**calculates residual vector (RULV) and residual vector error ratio for independent coordinates** 

**{u:}{dP:}** 

**‘L \=** 

**{P:}** 

**and calculates residual vector (RUOV) and coordinates** 

**{6P;} \= {P:} \-** 

**\-r**   
**{Ui}** 

**residual vector error ratio for omitted Koo\] {U:} ,** 

**F . \-0**   
**{U:}{6P:}** 

**73\. 74\. 75\. 77\.**   
**Go to DMAP No. 76 if residual vectors MATGPR prints the residual vector for MATGPR prints the residual vector for SDR1 recovers dependent displacements**   
**are not to be printed.** 

**independent coordinates (RULV). omitted coordinates (RUOV).** 

**H‘L \= {u \~ ,{uo} \= \[Go\]{ua} \+ {u:} \>**   
**–u;a** 

**HUaNUf**   
**—— \= {Uf} ,——. {Un} , Y5**   
**‘ouUn**   
**{um} \= \[Gm\]{un} , –– \= {Ugl**   
**urn** 

**2.2-9 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**and recovers single-point forces of constraint** 

**{q5} \= \-{P51 \+ \[K;\~\] {Uf} \+ \[Kss\] {Ys} .** 

**Go to DMAP No, 83 if all constraint sets have been processed.**   
**78\.** 

**Go to DMAP No. 41 if additional sets of constraints need to be processed.**   
**79\.** 

**Go to DMAP No. 99 and print Error Message No. 2 as the number of constraint sets exceeds**   
**80\.**   
**360\.** 

**Go to DMAP No. 105 and print Error Message No. 5 if multiple boundary conditions are**   
**82\.**   
**attempted with an improper subset.** 

**Go to DMAP No. 87 if no multipoint constraint force balance is requested.**   
**84\.** 

**EQMCK calculates the force and moment equilibrium check and prepares the multipoint**   
**85\.**   
**constraint force balance (OQMl) for output.** 

**OFP formats the table prepared by EQMCK and places it on the system output file for**   
**86\.**   
**printing.** 

**SDR2 calculates element forces (OEFl) and stresses (13ES1)and prepares load vectors (f3PGl),**   
**88\.**   
**displacement vectors (OUGVl), and single-point forces of constraint (k3QGl)for output and translation components of the displacement vector (PUGV1).** 

**\!3FPformats the tables prepared by SDR2 and places thereon the system output file for**   
**89\.**   
**printing.** 

90\.   
**SCAN examines the element stresses and forces calculated by SDR2 and generates scanned output that meets the specifications set by the user.** 

91\.   
**OFP formats the scanned output table prepared by SCAN and places it on the system output file for printing.** 

92\. 93\. 94\. 

96\.   
**Go to DMAP No. PLOT generates** 

**PRTMSG prints generated.** 

**Go to DMAP NO.**   
**95 if no deformed structure plots are requested.** 

**all requested deformed structure and contour plots.** 

**plotter data, engineering data, and contour data for each deformed plot 109 and make normal exit.**   
**98\.** 

**100\. 102\. 104\. 106\. 108\.**   
**Print Error Message No. 1 and terminate execution. Print Error Message No. 2 and terminate execution. Print Error Message No. 3 and terminate execution. Print Error Message No. 4 and terminate execution. Print Error Message No. 5 and terminate execution. Print Error Message No. 6 and terminate execution.** 

**2.2-10 (05/30/86)**  
**STATIC ANALYSIS WITH INERTIA RELIEF** 

**2.2.3 Output for Static Analysis with Inertia Relief** 

**The**   
**following output may be requested for Static Analysis with Inertia Relief: Displacements at selected grid points due to the sum of the applied loads and the 1\.** 

**inertia loads.** 

**Nonzero components of the applied static loads at selected grid points. 2\.** 

**Reactions on free-body supports due to applied loads (single-point forces of 3\.** 

**constraint).** 

**Forces and stresses in selected elements due to the sum of 4\.** 

**1oads.** 

**5\.**   
**Scanned output of forces and elements in selected elements. The**   
**following plotter output may be requested:** 

**1\.**   
**Undeformed and deformed plots of the structural model. Contour plots of stresses and displacements.**   
**2\.**   
**the applied loads and inertia** 

**2.2.4 Case Control Deck for Static Analysis with Inertia Relief** 

**The following items relate to subcase definition and data selection for Static Analysis with Inertia Relief:** 

**A separate subcase must be defined for each 1\.** 

**loads.** 

**2\.**   
**A static loading condition must be defined with a LllADselection.**   
**unique combination of constraints and static for (not necessarily within) each subcase** 

**3,**   
**An SPC set may be selected only if used to remove grid point singularities or some, but not all, of the free body motions. At least one free body support must be provided with a SUPORT card in the Bulk Data Deck.** 

**4\.**   
**Loading conditions associated with the same sets subcases in order to avoid unnecessary looping. 5\.**   
**REPCASE may be used to repeat subcases in order output item.**   
**of constraints should be in contiguous to allow multiple sets for the same** 

**2.2.5 Parameters for Static Analysis with Inertia Relief** 

**The following parameters are used in Static Analysis with Inertia Relief: 2.2-11 (05/30/86)**  
**DIsPLACEMENT RIGID FORMATS** 

**ASETliMJT- optional. A positive integer value of this parameter causes the ASET output** `1.` 

**data block to be generated by the GP4 module. A negative integer value or O suppresses the generation of this output data block. The default value is ().** 

**2\.**   
**AUT\~SPC \- reserved for future optional use. The default value is \-1.** 

**3\.**   
**CfJUPMASS- CPBAR, CPR@D, CPQUAD1, CPQUAD2, CPTRIA1, CPTRIA2, CPTUBE, CPQDPLT, CPTRPLT, CPTRBSC \- optional. These parameters cause the generation of coupled mass matrices rather than lumped mass matrices for all bar elements, rod elements, and plate elelllents that include bending stiffness.** 

**4\.**   
**GRDEQ \- optional. A positive integer value of this parameter selects the grid point about which equilibrium will be checked for the Case Control output request, MPCF@RCE. If the integer value is zero, the basic origin is used. The default value is \-1.** 

**5\. 6\.**   
**GRDPNT \- optional. Weight Generator to printed,** 

**IRES \- optional. A**   
**A positive integer value of this parameter causes the Grid Point be executed and the resulting weight and balance information to be** 

**positive integer value of this parameter causes the printing of the** 

**residual vectors following the execution of the SSG3 module.** 

**7\.**   
**13PT- optional. A positive integer value of this parameter causes both equilibrium and multipoint constraint forces to be calculated for the Case Control output request, MPCFfJRCE. A negative integer value of this parameter causes only the equilibrium force balance to be calculated for the output request. The default value is O which causes only the multipoint constraint forces to be calculated for the output request. SURFACE \- optional. The computations of the external surface areas for the 8\.** 

**two-dimensional and three-dimensional elements are activated by this parameter when they are generated in the EMG module. The results are multiplied by the real value of this parameter. See the description under the PARAM bulk data card for details. VOLUME \- optional. The volume computations for the two-dimensional and 9\.** 

**three-dimensional elements are activated by this parameter when they are generated in the EMG module. The results are multiplied by the real value of this parameter. See** 

**10\.**   
**the description under the PARAM bulk data WTMASS \- optional. The terms of the mass this parameter when they are generated in**   
**card for details.** 

**matrix are multiplied by the real value of the EMA module.** 

**2.2-12 (05/30/86)**

**STATIC ANALYSIS WITH INERTIA RELIEF** 

**2.2.6 Automatic ALTERs for Automated Multi-stage Substructurinq** 

**The following lines of the Static Analysis with Inertia Relief, Rigid Format 2, are ALTERed in a** 

**automated substructure analyses.** 

**Phase 1: 4, 44-44, 65-68, 70-96** 

**Phase 2: 4, 5-5, 8-18, 21-21, 30-30, 36-39, 46-51, 84-98** 

**Phase 3: 65-68, 70-76, 77** 

**If APP DISP, SUBS is used, the user may also specify ALTERs. However, these must not interfere with the automatically generated DMAP statement ALTLRs listed above. See Volume I, Section 5,9 for a description and listing of the ALTERs which are automatically generated for substructuring.** 

**2.2.7 Rigid Format Error Messages from Static Analysis with Inertia Relief** 

**The following fatal errors are detected by the DMAP statements in the Static Analysis with Inertia Relief rigid format. The text for each error message is given below in capital letters and is followed by additional explanatory material, including suggestions for remedial action.** 

● **STATIC ANALYSIS WITH INERTIA RELIEF ERROR MESSAGE NO. 1 \- MASS MATRIX REQUIRED FOR CALCULATION OF INERTIA Lf\!ADS.** 

**The mass matrix is null because either no elements were defined with Connection cards, nonstructural mass was not defined on a Property card, or the density was not defined on a Material card.** 

**STATIC ANALYSIS WITH INERTIA RELIEF ERROR MESSAGE NO. z \- ATTEMPT TO EXECUTE MORE THAN 360 LOllPS.** 

**An attempt has been made to use more than 360 different sets of boundary conditions. This number may be increased by ALTERing the REPT instruction following SDR1.** 

**STATIC ANALYSIS WITH INERTIA RELIEF ERROR MESSAGE ND. 3 \- No INDEPENDENT DEGREES OF FREED17MHAVE BEEN DEFINED.** 

**Either no degrees of freedom have been defined on GRID, SP$31NTor Scalar Connection cards, or all defined degrees of freedom have been constrained by SPC, MPC, YJPORT,OMITOr GRDsETcards,Or grounded on Scalar Connection cards.** 

**STATJC ANALYSIS WITH INERTIA RELIEF ERROR MESSAGE NO. 4 \- FREE-BODY SUPP@RTS ARE REQUIRED.** 

**A statically determinate set of supports must be specified on a SUPklRTcard in order to determine the rigid body characteristics of the structural model.** 

**2.2-13 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**STATIC ANALYSIS WITH INERTIA RELIEF ERR13RMESSAGE No. 5 \- SUBSET.** 

**A problem requiring boundary condition changes was run on restarted on subset O.** 

**STATIC ANALYSIS WITH INERTIA RELIEF ERR13RMESSAGE N@. 6 \-**   
**A LOOPING PR@BLEM RUN ON A N@N-LO@PING subset 1 or 3, The problem should be** 

**NO STRUCTURAL ELEMENTS HAVE BEEN DEFINED.** 

**No structural elements have been defined with Connection cards,** 

**I** 

**2.2-14 (05/30/86)**

**DISPLACEMENT** 

**2.3 NORMAL MODES ANALYSIS** 

**2.3.1 DMAP Sequence for Normal Modes Analysis** 

**RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGIO FORMAT 3**   
**RIGID FORMATS** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**OPTIONS IN EFFECT GO ERR-2 LIST NODECK NOREF NOOSCAR \-------- \-------- \-** 

**1 BEGIN** 

**2 PRECHK 3 FILE** 

**4 PARA14** 5 **GP1** 

**6 PLTTRAN \~ GP2** 

**8 PARAML 9 PURGE** 

**10 CONO** 

**11 PLTSET** 

**12 PRTMSG 13 PARAM J4 PARAfl 15 COND** 

**16 PLOT** 

**17 PRTMSG 18 LABEL 19 GP3** 

**20 TA1** 

**21 COND**   
**DISP 03 \- NORMAL MODES ANALYSIS \- APR. 1986 $ ALL $** 

**LAMA=APPEND/PHIA=APPEND $** 

**//\*HPY\*/CARONO/O/O $** 

**GEOMl,GEDM2,/GPL,EQEXIN,GPDT,CSTM,BGPDT,SIL/S,N,LUSET/ NOGPDT/ALWAYS=-l $** 

**BGPOT,SIL/BGPDP,SIP/LUSET/S,N,LUSEP $** 

**GEoM2,EQExlN/EcT $** 

**PCDB//\*PRES\*////JUMPPLOT $** 

**PLTSETX,PLTPAR,GPSETS,ELSETS/JUMPPLOT $** 

**Pl,JU14PPLOT$** 

**PCDB,EQEXIN,ECT/PLTSETX,PLTPAR,GPSETS,ELSETS/S,N,NS(L/ S,N,JUMPPLOT $** 

**PLTSETX// $** 

**//\*MPY\*/PLTFLG/l/l $** 

**//\*MPY\*/PFILE/O/O $** 

**P1,JUMPPLOT $** 

**PLTPAR,GPSETS,ELSETS,CASECC,BGPDT,EQEXIN,SIL,,ECT,,/PLOTXl/ NSIL/LUSET\\S,N,JUMPPLOT/S,N,PLTFLG/S,N,PFILE $** 

**PLOTX1//$** 

**P1 $** 

**GEoM3,EQExIN,GEom2/,GPTT/NoGRAv $** 

**ECT,EPT,BGPDT,SIL,GPTT,CSTM/EST,GE l,GPECT,,/**   
**LUSET/S,N,NOSIMP/l/S,N,NOGENL/S,N,GENEL $** 

**ERROR4,NOSIMP $** 

**2.3-1 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 3** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**22** 

**23** 

**24** 

**25** 

**26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41** 

**42** 

**43 44**   
**PURGE PARAII PARAM EMG** 

**PURGE CONO** 

**EMA** 

**LABEL COND** 

**EMA** 

**COND** 

**GPWG** 

**OFP** 

**LABEL EQUIV COND** 

**SMA3** 

**LABEL PARAM GPk** 

**COND** 

**PURGE COND**   
**OGPST/GENEL $** 

**//\*AoD\*/NoKGGx/I/o $** 

**//\*Aoo\*/NoMGG/I/o $** 

**EST,CSTM,MPT,DlT,GEOM2,/KELM, KDICT,MELM,MDICT,,,/S,N,NOKGGX/ S,N,NOMGG////C,Y,COUPMAC,Y,,Y, CPBAR/**   
**C,Y,CPROO/C,Y,CPQUADl/C,Y, CPQUAD2/C,Y,CPTRlAl/C,Y,CPTRl A2/ C,Y,CPTUBE/C,Y,CPQOPLT/C,Y, CPTRPLT/C,Y,CPTRBSC/** 

**V,Y,VOLUME/V,Y,SURFACE $** 

**KGGX,GPST/NOKGGX $** 

**JMPKGG,NOKGGX $** 

**GPECT,KDICT,KELM/KGGX,GPST $** 

**JMPKGG $** 

**ERROR1,NOMGG $** 

**GPECT,MDICT,MELM/MGG,/-l/C,Y,WTMASS=l .0 $** 

**LGPWG,GRDPNT $** 

**BGPDP,CSTM,EQEXIN,MGG/OGPWG/V,Y,GRDPNT=- l/C,Y,WTMASS $ OGPWG ,,,,,//S,N,CARDNO $** 

**LGPWG $** 

**KGGX,KGG/NOGENL $** 

**LBL1l,NOGENL $** 

**GEl,KGGX/KGG/LUSET/NOGENL/NOS IMP $** 

**LBL1l $** 

**//\~\~MPY\*/NSKIP/O/O $** 

**CASECC,GEOM4,EQEXIN,GPDT,BGPOT,CSTM, GPST/RG,YS,USET,ASET/ LUSET/S,N,MPCFl/S,N,MPCF2/S ,N,SINGLE/S,N,OMIT/S,N,REACT/ S,N,NSKIP/S,N,REPEAT/S,N,NOSET/S, N,NOL/S,N,NOA/C,Y,ASETOUT/ S,Y,AUTOSPC $** 

**ERROR3,NOL $** 

**KRR,KLR,DM,MLR,MR/REACT/GM/MPCF l/GO/OMIT/KFS/SINGLE/QG/NOSET $ LBL4,GENEL $** 

**2.3-2 (05/30/86)**

**NORMAL MODES ANALYSIS** 

**RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 3** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**45 PARAM b6 COND 47 GPSP 48 OFP** 

**49 LABEL 50 EQUIV 51 COND** `52 mcEl 53` **MCE2 54 LABEL 55 EQUIV 56 COND 57 ;CE1 58 LABEL 59 EQUIV 60 EQUIV 61 COND 62 SMP1 63 SMP2 64 LABEL 65 COND 66 RBMG1 67 RBMG2 68 RBMG3 69 RBMGk 70 LABEL**   
**//\*EQ\*/GPSPFLG/AUTOSPC/O $** 

**LBL4,GPSPFLG $** 

**GPL,GPST,USET,SIL/OGPST/S,N,NOGPST $ OGPST,, ,,, //S,N,CARDNO $** 

**LBL4 $** 

**KGG,KNN/MPCFl/MGG,HNN/t4PCFl $** 

**LBL2,MPCF1 $** 

**USET,RG/GM $** 

**USET,GM,KGG,MGG,,/KNN,HNN, , $** 

**LBL2 $** 

**KNN,KFF/SINGLE/MNN,MFF/SINGLE $ LBL3,SINGI.E $** 

**USET,KNN,MNN,,/KFF,KFS,,MFF ,, $** 

**LBL3 $** 

**KFF,KAA/OMIT $** 

**MFF,MAA/OMIT $** 

**LBL5,0MIT $** 

**USET,KFF,,,/GO,KAA,KOO, LOO, ,,,, $ USET,GO,MFF/t4AA $** 

**LBL5 $** 

**LBL6,REACT $** 

**USET,KAA,MAA/KLL,KLR,KRR,MLL ,MLR,MRR $ KLL/LLL $** 

**LLL,KLR,KRR/OM $** 

**Ofl,FILL,MLR,MRR/MR** 

**LBL6 $** 

**2.3-3 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**RIGID FORMAT OMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 3** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**71 DPD** 

**72 COND** 

**73 PARA\!4 74 READ** 

**75 OFP** 

**76 COND** 

**77 OFP** 

**78 SDR1** 

**79 COND** 

**80 EQHCK** 

**81 OFP** 

**82 LABEL 83 SOR2** 

**8k OFP** 

**85 SCAN** 

**86 OFP** 

**87 COND** 

**88 PLOT** 

**89 PRTflsG 90 LABEL 91 JUMP** 

**92 LABEL**   
**DYNAMICS,GPL,SIL,USET/GPLD,S lLD,USETD,,,,,,,EED,EQDYN/ LUSET/LUSETD/NOTFL/NODLT/NOPSDL/NOFRL/** 

**NONLFT/NOTRL/S,N,NOEED//NOUE $** 

**ERROR2,NOEED $** 

**//\*Hpy\*/NEIGv/I/-l $** 

**KAA,t4AA,MR,DM,EED,USET,CASECC/LAMA,PH lA,Ml,OEIGS/\*MODES\*/ S,N,NEIGV $** 

**OE IGS ,,,,,//S,N,CARDNO $** 

**FINIS,NEIGV $** 

**LAMA ,,,,,//S,N,CARDNO $** 

**USET, ,PHIA, ,,GO,GM,,KFS,,/PHIG,,QG/l/\*REl G\* $** 

**NOMPCF,GRDEQ $** 

**CASECC,EQEXIN,GPL,BGPDT,SIL, USET,KGG,GM,PHIG,LAMA,QG,CSTM/ OQM1/V,Y,OPT=O/V,Y,GRDEQ/-l $** 

**OQMl,,,,,//S,N,CARDNO $** 

**NOMPCF $** 

**CASECC,CSTM,MPT,DIT,EQEXI N,SIL, ,,BGPDP,LAMA,QG,PHI G,EST,,/ ,OQGl,OPHIG,OESl,OEFl,PPHIG/\>?RE lG\#\~ $** 

**OPHIG,OQGl,OEFl,OESl,,//S,N, CARDNO $** 

**CASECC,OESl,OEF1/OESFl/\*RF\* $** 

**OESF1 ,,,,,//S,N,CARDNO $** 

**P2,JUMPPLOT $** 

**PLTPAR,GPSETS,ELSETS,CASECC, BGPDT,EQEXIN,SI P,,PPHIG,GPECT,OES 1/ PLOTX2/NSlL/LUSEP/JUMPPLOT/PLTFLG/S ,N,PFILE $** 

**PLOfX2// $** 

**P2 $** 

**FINIS $** 

**ERROR1 $** 

**93 PRTPARM //-1/\*MoDES\* $** 

**2.3-4 (05/30/86)**  
**NORMAL MODES ANALYSIS** 

**RIGID FORMAT DMAP LISTING**   
**APRIL 1986 RELEASE** 

**DISPLACEMENT APPROACH, RIGID FORMAT 3** 

**LEVEL 2.0 NASTRAN DMAP COMPILER \- SOURCE LISTING** 

**gh** 

**95** 

**96** 

**97** 

**98** 

**99** 

**100 10I 102**   
**LABEL** 

**PRTPARM LABEL** 

**PRTPARH LABEL** 

**PRTPARtl LABEL** 

**PURGE** 

**ENO**   
**ERROR2 $** 

**//-2/\*HODES\* $** 

**ERROR3 $** 

**//-3/\*MODES\* $** 

**ERRORk $** 

**//-b/\*tIODES\* $** 

**FINIS $** 

**DUMMY/ALWAYS $** 

**s** 

**2.3-5 (05/30/86)**

**2.3.2 5,** 

**6\.** 

**7\.** 

**10\.** 

**110** 

**12\.** 

**15\.** 

**16\.** 

**17\.** 

**19\.** 

**20\.** 

**21\.** 

**25\.** 

**27\.** 

**28\.**   
**DISPLACEMENT RIGID FORMATS** 

**Description of Important DMAP Operations for Normal Modes Analysis** 

**GP1 generates coordinate system transformation matrices, tables of grid point locations, and tables relating the internal and external grid point numbers.** 

**PLTTRAN modifies special scalar grid points in the BGPDT and SIL tables. GP2 generates Element Connection Table with internal indices.** 

**Go to DMAP No. 18 if there are no structure plot requests,** 

**PLTSET transforms user input into a form used to drive the structure plotter. PRTMSG prints error messages associated with the structure plotter.** 

**Go to DMAP No. 18 if no undeformed structure plots are requested.** 

**PL@T generates all requested undeformed structure plots,** 

**PRTMSG prints plotter data and engineering data for each undeformed plot generated. GP3 generates Grid Point Temperature Table.** 

**TA1 generates element tables for use in matrix assembly and stress recovery. Go to DMAP No. 98 and print Error Message No. 4 if there are no structural elements.** 

**EMG generates structural element stiffness and mass matrix tables and dictionaries for later assembly by the EMA module.** 

**Go to DMAP No. 29 if no stiffness matrix is to be assembled.** 

**EMA assembles stiffness matrix \[K\~g\] and Grid Point Singularity Table,** 

**Go to DMAP No. 92 and print Error Message No. 1 if no mass matrix is to 30\.** 

**EMA assembles mass matrix \[Mgg\].**   
**31\.** 

**Go to DMAP No. 35 if no weight and balance information is requested. 32\.** 

**GPWG generates weight and balance information.**   
**33\.**   
**be assembled.** 

**OFP formats the weight and balance information prepared by GPWG and places it on the system**   
**34\.**   
**output file for printing.** 

**Equivalence \[K&\] to \[Kgg\] if no general elements exist.**   
**36\.** 

**Go to DMAP No. 39 if no general elements exist.**   
**37\.** 

**SMA3 adds general elements to \[K\~g\] to obtain stiffness matrix \[Kgg\].**   
**38\.** 

**GP4 generates flags defining members of various displacement sets (USET) and forms**   
**41\.**   
**multipoint constraint equations \[Rg\] {ugl \= O.** 

**Go to DMAP No. 96 and print Error Message No. 3 if no independent degrees of freedom are**   
**42\.**   
**defined.** 

**Go to DMAP No. 49 if general elements are present,**   
**44\.** 

**Go to DMAP No. 49 if no potential grid point singularities exist.**   
**46\.** 

**GPSP generates a table of potential grid point singularities.**   
**47\.** 

**2.3-6 (05/30/86)**  
**NORMAL MODES ANALYSIS** 

**48\. \!3FPformats the table of potential grid point singularities prepared by GPSP and places it on the system output file for printing.** 

**50\. Equivalence \[Kgg\] to \[Knn\] and \[Mgg\] to \[Mnn\] if no multipoint constraints exist. 51\. Go to DMAP No. 54 if no multipoint constraints exist.** 

**52\. MCE1 partitions multipoint constraint equations** \[Rgl \= **\[Rm\~Rnl and solves for multipoint constraint transformation matrix \[Gm\]** ❑ **\-\[Rm\]-l\[Rnj.** 

**53\. MCE2 partitions stiffness and mass matrices** 

`1`   
**K IK**   
**\[Kgg\] \= fl\~Km** 

**mn mm**   
\[ 

**and performs matrix reductions**   
**and \[Mgg\] \=**   
**M IM** 

**A“+ \~ Mmn IMmm ,1** 

\[Knnl \= \[\~nnl \+ \[G\~l\[Kmnl \+ \[K\~nl\[Gml \+ \[G\~l\[\\ml\[Gml and 

\[Mnnl \= \[inn\] \+ \[G;l\[Mmnl \+ \[M:nl\[Gml \+ \[G;l\[Mmml\[Gml . 

**55\. Equivalence \[Knnl to \[Kff\] and \[Mnn\] tO \[Mff\] if no sin91e-point constraints exist” 56\. Go to DMAP No. 58 if no single-point constraints exist.** 

**57\. SCE1 partitions out single-point constraints**   
\[1**Kff/ Kfs** \[1**‘ff’ ‘fs \[Knn\] . — \+ — and \[Mnn\]= –+– .**   
**Ksf I Ks\~ Msf I Mss** 

**59\. Equivalence \[Kff\] to \[Kaa\] if no omitted coordinates exist.** 

**60\. Equivalence \[Mff\] to \[Maa\] if no omitted coordinates ‘xiSt”** 

**61\. Go to DMAP No. 64 if no omitted coordinates exist.** 

**62\. SMP1 partitions constrained stiffness matrix**   
H**K IK**   
**\[Kff\] \= :\~K\~ ,** 

**oa 00** 

**solves for transformation matrix \[Go\] \=** \-\[Kool-l\[Koal 

**and performs matrix reduction \[Kaal \= \[\~aal \+ \[K\~al\[Gol .** 

**63\. SMP2 partitions constrained mass matrix** 

**2.3-7 (05/30/86)**  
**DISPLACEMENT RIGID** 

r- 7   
II**M \[M**   
**rMffl \= :-+M\~ ‘** 

**oa 00**   
**L J** 

**and performs matrix reduction** 

**FORMATS** 

**e** 

**65\. Go to 66\. RBMG1**   
**\[Maa\]** 

**DMAP No. 70 if partitions out** 

**\[Kaa\] \=** 

\= \[iaal \+ \[M\~al\[Gol \+ \[Gj\[Moal \+ \[G\~l\[Mool\[Gol . 

**no free-body supports exist.** 

**free-body supports**   
\[\~:\] **and \[M’J=\[?J?\]** 

**67\. RBt4G2 68, RBMG3**   
**decomposes constrained stiffness matrix \[Kgk\] \= \[LLL\]\[ULL\]. forms rigid body transformation matrix** 

**\[D\] \= \-\[KiL\]-l\[K1r\],** 

**calculates rigid body check matrix** 

**\[X\] \=** \[Krrl \+ \[K;rl\[rIl 

**and calculates rigid body error ratio** 

●   
**E .** 

**&** 

**69\. RBMG4 forms rigid body mass matrix**   
**x.** 

**Krr** 

\[q.\] \= \[Mrrl \+ \[Mjrl\[Dl \+ \[DTl\[Mkrl \+ \[DTIIMILIIDI. 

**71\. DPD extracts Eigenvalue Extraction Data from Dynamics data block.** 

**72\. Go to DMAP No. 94 and print Error Message No. 2 if there is no Eigenvalue Extraction Data. 74\. READ extracts real eigenvalues and eigenvectors from the equation** 

**\[Kaa \- AMaal{ua} \= O ,** 

**calculates rigid body modes by finding a square** 

**\[mol \=** \[o\~ol\[fnrl\[$rol 

**is diagonal and normalized, computes rigid body** \[1**DO**   
**\[Oaol \= – \~ ,** 

**‘$ro**   
**matrix \[@ro\] such that eigenvectors** 

**2.3-8 (05/30/86)**   
**e**

**NORMAL MODES ANALYSIS** 

`calculates`**modal mass matrix** 

\[Ml \= \[I$\~l\[Maal\[tIa\] 

**and normalizes eigenvectors according to one** 

**1\) Unit value of a selected component 2\) Unit value of the largest component 3\) Unit value of the generalized mass.**   
**of the following user requests:** 

**f5FPformats the summary ofeigenvalue extraction information (\!JEIGS)prepared by READ and**   
**75\.**   
**places it on the system output file for printing.** 

**Go to DMAP No.lOO and make normal exit if no eigenvalues were found.**   
**76\.** 

**@FP formats the eigenvalues (LAMA) prepared by READ and places them on the system output**   
**77\.**   
**file for printing.** 

**SDR1 recovers dependent components of the eigenvectors**   
**78\.** 

**H‘$a**   
**{$.} \= \[Go\] {$al , H4f**   
**——** ❑ **{On} , ‘$s** 

**H‘$n**   
**—— \=** `{$91`   
`‘$M`   
—— **\=** {of} , **40** 

{+m} \= \[Gml {tIn} , 

**and recovers single-point forces of constraint {qs} \= \[Kfs\]Ti$f}.** 

**Go to DMAP No. 82 if no multipoint constraint force balance is requested. 79\.** 

**EQMCK calculates the force and moment equilibrium check and prepares the multipoint**   
**80\.**   
**constraint force balance** (\!3QMl) **for output.** 

**OFP formats the table prepared by EQMCK and places it on the system output file for**   
**81\.**   
**printing.** 

**SDR2 calculates element forces (OEFl) and stresses** (OEsl) and prepares eigenvectors (WHIG)   
**83\.**   
**and single-point forces of constraint (OQGl) for output and translation components of the eigenvectors (PpHIG).** 

**i3FP formats the tables prepared by SDR2 and places them on the system output file for**   
**84\.**   
**printing.** 

**85\. 86\.**   
**SCAN examines the element stresses output that meets the specifications** 

**\!3FPformats the scanned output table file for printing.**   
**and forces calculated by SDR2 and generates scanned set by the user.** 

**prepared by SCAN and places it on the system output** 

**Go to DMAP No. 90 if no deformed structure plots are requested. 87\.** 

**2.3-9 (05/30/86)**  
**DISPLACEMENT RIGID FORMATS** 

**88\. PLOT generates all requested deformed structure and contour plots.** 

**89\. PRTMSG prints plotter data, engineering data, and contour data for each deformed plot generated.** 

**91\. Go to DMAP No. 100 and make normal exit.** 

**93\. Print Error Message No. 1 and terminate execution.** 

**95\. Print Error Message No. 2 and terminate execution.** 

**97\. Print Error Message No. 3 and terminate execution.** 

**99\. Print Error Message No. 4 and terminate execution.** 

**2.3-10 (05/30/86)**