NASA SP-223 (01) 
THE NASTRAN PROGRAMMER'S MANUAL 
SEPTEMBER 1972 
Scientific and Technical Information Office 1972 
NATIONAL AERONAUTICS AND SPACE ADMINISTRATION 
Washington, D.C. 
II] ]1] i,

For sale from Computer Software Management and Information Center (COSMIC) Barrows Hall, University of Georgia, Athens, Georgia 30601 -Price $27.50
PREFACE TO THE NASTRAN PROGRAMMER'S MANIIAL 
The Programmer's Manual is one of four manuals that constitute the documentation for NASTRAN, the other three being the Theoretical Manual, the User's Manual and the Demonstration Problem Manual. The Programmer's Manual is divided into seven major sections: Section l, NASTRAN Program ming Fundamentals; Section 2, Data Block and Table Descriptions; Section 3, Subroutine Descriptions; Section 4, Module Functional Descriptions; Section 5, NASTRAN - Operating System Interfaces; Section 6, Modifications and Additions to NASTRAN; and Section 7, NASTRAN Support Programs. 
Section l is a general overview of the program, and as such it should be read as background material for all sections which follow. 
Section 2 contains descriptions of the data blocks, which are the principal means of data communication between the program's functional modules (a module is defined to be a group of sub routines which perform a specific function) and the NASTRAN Executive System. Two indexes for the data block descriptions, one sorted alphabetically on data block names and the other sorted alpha betically on the names of the modules from which the data blocks are output, are given in Sections 2.2.1 and 2.2.2 respectively. Section 2 also contains a) descriptions of tables, both core and noncore resident, maintained by the NASTRAN Executive System and b) descriptions of miscellaneous tables which are accessed by a class of modules. Alphabetical indexes for these tables are given at the beginning of Sections 2.4 and 2.5 respectively. 
Sections 3 and 4 contain descriptions of the (utility or general purpose) subroutines and modules of NASTRAN respectively. The reader is directed to the alphabetical indexes, sorted on entry point names, in Sections 3.2 and 4.1.3 respectively for these sections. An index to the Module Functional Descriptions, sorted alphabetically on module names, is given in Section 4.1.2. The reader is urged to read the introductory material to Sections 3 and 4 before using these sections. 
Section 5 treats computer and operating system dependent matters such as operating system control cards and generation of the absolute (executable) NASTRAN system. 
Section 6 describes the means by which modifications and additions to NASTRAN are implemented. Section 7 describes several auxiliary programs used to maintain or interface with NASTRAN. 
The learning of any new system, whether it be an operating system or a large applications system like NASTRA_I,is made more difficult than it ought to be because of the use by the designers of the system of new mnemonics, acronyms, phrases and "buzz" words. In order to aid the reader in 
i (811172)
learning such commonly used NASTRAN terms, a single source reference, Section 7, the NASTRAN Dictionary, of the User's Manual is provided. The programmer is adivsed to secure a copy of at least this section of the User's Manual for his day-to-day reference. 
ii (8/I/72)

TABLE OF CONTENTS 
Section 
I. NASTRAN PROGRAMMING FUNDAMENTALS 
Page No. 

l.l 1.2 
PROGRAM 1.I.I 
l.l.2 
NASTRAN l.2.1 
l.2.2 
l.2.3 
OVERVIEW ........................................................... l.l-I Objectives ......................................................... l.l-I Program Organization .............................................. l.l-3 EXECUTIVE SYSTEM ................................................... 1.2-1 Introduction ....................................................... 1.2-1 Executive Operations During the Preface ............................ 1.2-4 Executive Operations During Problem Solution ....................... 1.2-9a 

1.3 WORD SIZE AND COMPUTER HARDWARE CONSIDERATIONS ............................. 1.3-1 1.3.1 Introduction ....................................................... 1.3-1 1.3.2 Alphanumeric Data .................................................. 1.3-2 1.3.3 Word Packing ....................................................... 1.3-2 
1.4 SYSTEM BLOCK DATA SUBPROGRAM (SEMDBD) ....................................... 1.4-1 1.5 THE OPEN CORE CONCEPT ...................................................... 1.5-1 1.5.1 Introduction ....................................................... 1.5-1 1.5.2 Definition of Open Core ............................................ 1.5-1 1.5.3 Example of an Application of Open Core ............................. 1.5-1 1.6 NASTRAN INPUT/OUTPUT ....................................................... 1.6-1 1.6.1 Introduction ....................................................... 1.6-1 1.6.2 Use of the Operating System Input File ............................. 1.6-1 1.6.3 Use of the Operating System Output File ............................ 1.6-2 1.6.4 GIN_ ............................................................... 1.6-3 1.7 NASTRAN MATRIX ROUTINES .................................................... 1.7-I 1.7.1 Introduction ....................................................... 1.7°l 1.7.2 Matrix Packing and Unpacking ....................................... 1.7-1 
1.7.3 The Nested Vector Set Concept Used to Represent Components 
of Displacement .................................................... 1.7-2 1.7.4 Processing of Matrices ............................................. 1.7-4 1.8 GENERATION OF MATRICES ..................................................... 1.8-1 1.8.1 The ECPT Data Block ................................................ 1.8-1 1.8.2 Structural Elements ................................................ 1.8-2 
iii (8/I/72)

,Section 
TABLE OF CONTENTS (Continued) 
Page No. 

TERMINATION PHILOSOPHY AND DIAGNOSTIC MESSAGES ............................. 1.9-I 1.9 
1 .I0 
RESTARTS IN NASTRAN ........................................................ I.I0-I 
2. 
DATA BLOCK AND TABLE DESCRIPTIONS 
2.1 INTRODUCTION .............................................................. 2.1-I 2.2 DATA BLOCK DESCRIPTIONS - GENERAL COMMENTS AND INDEXES ..................... 2.2-I 2.2.1 Index for Data Block Descriptions Sorted on Data Block Names ....... 2.2-3 2.2.2 Index for Data Block Descriptions Sorted Alphabetically by Module .. 2.2-11 2.3 DATA BLOCK DESCRIPTIONS .................................................... 2.3-I 2.3.1 Data Blocks Output From Module IFPI ................................ 2.3-I 

2.3.2 Data Blocks 2.3.3 Data Blocks 2.3.4 Data Blocks 2.3.5 Data Blocks 2.3.6 Data Blocks 2.3.7 Data Blocks 2.3.8 Data Blocks 2.3.9 Data Blocks 2.3.10 Data Blocks 2.3.11 Data Blocks 2.3.12 Data Blocks 2.3.13 Data Blocks 2.3.14 Data Blocks 2.3.15 Data Blocks 2.3.16 Data Blocks 2.3.17 Data Blocks 2.3.18 Data Blocks 2.3.19 Data Blocks 2.3.20 Data Blocks 2.3.21 Data Blocks 2.3.22 Data Blocks 
Output From Module IFP ................................. 2.3-5 Output From Module GPI ................................. 2.3-31 Output From Module GP2 ................................. 2.3-36 Output From Module PLTSET .............................. 2.3-37 Output From Module PL_T ................................ 2.3-40 Output From Module GP3 ................................. 2.3-41 Out)ut From Module TAI ................................. 2.3-45 Out)ut From Module SMAI ................................ 2.3-56 Out)ut From Module SMA2 ................................ 2.3-58 Out)ut From Module GPWG ................................ 2.3-59 Out)ut From Module SMA3 ................................ 2.3-60 Out)ut From Module GP4 ................................. 2.3-61 Out)ut From Module GPSP ................................ 2.3-63 Out)ut From Module MCEI ................................ 2.3-64 Out)ut From Module MCE2 ................................ 2.3-65 
Out)ut From Module SCEI ................................ 2.3-67 Out)ut From Module SMPI ............. ................... 2.3-70 OutDut From Module RBMGI ............................... 2.3-73 Output From Module RBMG2 ............................... 2.3-75 Output From Module RBMG3 ............................... 2.3-77 Output From Module RBMG4 ............................... 2.3-78 
iv (8/I172)

Section 
2.3.23 
2.3.24 
2.3.25 
2.3.26 
2.3.27 
2.3.28 
2.3.29 
2.3.30 
2.3.31 
2.3.32 
2.3.33 
2.3.34 
2.3.35 
2.3.36 
2.3.37 
2.3.38 
2.3.39 
2.3.40 
2.3.41 
2.3.42 
2.3.43 
2.3.44 
2.3.45 
2.3.46 
2.3.47 
2.3.48 
2.3.49 
2.3.50 
2.3.51 
2.3.52 
TABLE OF CONTENTS (Continued) 
Page No. 
Data Blocks Output From Module SSGI ................................ 2.3-79 Data Blocks Output From Module SSG2 ................................ 2.3-80 Data Blocks Output From Module SSG3 ................................ 2.3-81 Data Blocks Output From Module SSG4 ................................ 2.3-83 Data Blocks Output From Module SDRI ................................ 2.3-84 Data Blocks Output From Module SDR2 ................................ 2.3-88 Data Blocks Output From Module DPD ................................. 2.3-114 
Data Blocks Output From Module READ ................................ 2.3-125 Data Blocks Output From Module DSMGI ............................... 2.3-128 Data Blocks Output From Module SMP2 ................................ 2.3-129 Data Blocks Output From Module DSMG2 ............................... 2.3-130 Data Blocks Output From Module PLAI ................................ 2.3-132 Data Blocks Output From Module ADD ................................. 2.3-137 Data Blocks Output From Module PLA2 ................................ 2.3-138 Data Blocks Output From Module PLA3 ................................ 2.3-139 Data Blocks Output From Module PLA4 ................................ 2.3-140 Data Blocks Output From Module CASE ................................ 2.3-141 Data Blocks Output From Module MTRXIN .............................. 2.3-142 Data Blocks Output From Module GKAD ................................ 2.3-143 Data Blocks Output From Module CEAD ................................ 2.3-146 Data Blocks Output From Module VDR ................................. 2.3-149 Data Blocks Output From Module FRRD ................................ 2.3-158 Data Blocks Output From Module SDR3 ................................ 2.3-160 Data Blocks Output From Module XYTRAN .............................. 2.3-175 Data Blocks Output From Module RANDOM .............................. 2.3-179 Data Blocks Output From Module TRD ................................. 2.3-181 Data Blocks Output From Module GKAM ................................ 2.3-183 Data Blocks Output From Module DDRI ................................ 2.3-184 Element Stress Output Data Description ............................. 2.3-185 Element Force Output Data Description .............................. 2.3-189 
v (811172)
Secti on 2.4 
TABLE OF CONTENTS (Continued) 
2.3.53 Data Blocks Output From Module DDR2 ................................ 2.3.54 Data Blocks Output From Module BMG ................................. 2.3.55 Data Blocks Output From Module PLTTRAN ............................. EXECUTIVE TABLE DESCRIPTIONS ............................................... 
Page No. 2.3-192 
2.3-194 
2.3-194 
2.4-I 
2.4.1 Executive Tables Which are Permanently Core Resident ............... 2.4-2 2.4.2 Executive Tables Not Permanently Core Resident ..................... 2.4-15 2.5 MISCELLANEOUS TABLE DESCRIPTIONS ........................................... 2.5-I 2.5.1 Miscellaneous Tables Which are Permanently Core Resident ........... 2.5-2 2.5,2 Miscellaneous Tables Not Permanently Core Resident ................. 2,5-6 
3. 
SUBROUTINE DESCRIPTIONS 
3.1 INTRODUCTION .............................................................. 3.1-I 3.2 ALPHABETICAL INDEX OF ENTRY POINTS FOR SUBROUTINE DESCRIPTIONS ............. 3.2-I 3.3 EXECUTIVE SUBROUTINE DESCRIPTIONS ......................................... 3.3-I 3.3.1 XSEMI (Executive Sequence Monitor, Preface) ........................ 3.3-I 
3.3.2 3.3.3 3.3.4 3.3.5 
BTSTRP SEMINT GNFIAT ENDSYS 
(Bootstrap Generator) ....................................... 3.3-2 (Sequence Monitor Initialization) ........................... 3.3-3 (Generate FIAT) ............................................. 3.3-5 (End-of-Link) ............................................... 3.3-6 
3.3.6 3.3.7 3.3.8 3.3.9 3.3.10 
3.3.11 3.3.12 3.3.13 3.3.14 3.3.15 
SEARCH (Search, Load, and Execute Link) ............................ 3.3-8 XSEMi (Link i Main Program, i = 2,3 .... ) ........................... 3.3-9 XSEMXX (Sequence Monitor - Deck Generator) ......................... 3.3-11 
GNFIST (Generate FIST) ............................................. 3.3-12 XEOT (End-of-Tape) ................................................. 3.3-14 SSWTCH (Sense Switches) ............................................ 3.3-15 C_NMSG (Console Message Writer) ................................... 3.3-16 TTLPGE (Title Page Writer) ......................................... 3.3-17 SEMTRN (Transliteration) (IBH 360-370 only) ........................ 3.3-19 RETURN (Return) .................................................... 3.3-20 
3.4-I 
3.4 
UTILITY SUBROUTINE DESCRIPTIONS ............................................ 
3.4-I 
3.4.1 MAPFNS (Machine Word Functions) .................................... 
vi (8/I/72)

Section 
3.4.2 
3.4.3 
3.4.4 
3.4.5 
3.4.6 
3.4.7 
3,4.8 
3.4.9 
3.4.10 
3.4.11 
3.4.12 
3.4.13 
3.4.14 
3.4.15 
3.4.16 
3.4.17 
3.4.18 
3.4.19 
3.4.20 
3.4.21 
3.4.22 
3.4.23 
3.4.24 
3.4.25 
3.4.26 
3.4.27 
3.4.28 
3.4.29 
3.4.30 
3.4.31 
TABLE OF CONTENTS (Continued) 
Page No. 
_PEN (Initiate Activity on a File) ................................. 3.4-3 WRITE (Write Data in a Logical Record) ............................. 3.4-4 CLOSE (Terminate Activity on a File) ............................... 3.4-5 READ (Read Data From a Logical Record) ............................. 3.4-6 FWDREC (Forward Space One Logical Record) .......................... 3.4-8 BCKREC (Backspace One Logical Record) .............................. 3.4-9 REWIND (Position File to the Load Point) ........................... 3.4-I0 
EOF (Write an End-of-File) ......................................... 3.4-II SKPFIL (Skip Files Forward or Backward) ............................ 3.4-12 XGINO (GINO Utility Routine) ....................................... 3.4-13 GINO (General Input/Output Routine) ................................ 3.4-15 OPNCOR (Transmit Logical Records To/From Core Storage) ............. 3.4-20 
GOPEN (Short Form for Subroutine _PEN With Header Record 
Processing) ........................................................ 3.4-22 FREAD (Short Form for Subroutine READ) ............................. 3.4-23 WRTTRL (Write Trailer) ............................................. 3.4-24 FNAME (File Name) .................................................. 3.4-25 CLSTAB (Close a GINO File and Write a Nonzero Trailer) .............. 3.4-26 XRCARD (Executive Free-Field Card Data Conversion Routine).......... 3.4-27 RCARD (Fixed Field Card Data Conversion Routine) ................... 3.4-32 TAPBIT (Tape Bit Test) ............................................. 3.4-35 PEXIT (Problem Exit)................................................ 3.4-36 TMTOGO (Time-To-Go) ................................................ 3.4-37 PAGE (Page Heading) ...................._............................ 3.4-38 MESAGE (Message) ................................................... 3.4-39 MSGWRT (Message Writer) ............................................ 3.4-40 USRMSG (User Message Writer) ....................................... 3.4-41 MATDUM (Matrix Dump (Print) Routine) ............................... 3.4-42 TABPRT (Table Printer) ............................................. 3.4-43 PRELOC (Position Data Block to Requested Record) ................... 3.4-44 SORT (Sort a Table) ................................................ 3.4-46 
vii (811172)

Section 
3.4.32 
3.4.33 
3.4.34 
3.4.35 
3.4.36 
3.4.37 
3.4.38 
3.4.39 
GMMATD Precisi 
GMMATS Precisi 
INVERD INVERS PREMAT 
PRETRD Double 
PRETRS Single 
PRETAB 
TABLE OF CONTENTS (Continued) 
Page No. 
(General Matrix Multiply and Transpose - Double 
on) ......................................................... 3.4-49 
(General Matrix Multiply and Transpose - Single 
on) ......................................................... 3.4-52 (Double Precision In Core Inverse Routine) ................... 3.4-53 (Single Precision In Core Inverse Routine) .................. 3.4-54 (Material Property Utility) ................................. 3.4-55 
(Utility for Modules Which Use the CSTM Data Block - 
Precision Version) .......................................... 3.4-64 
(Utility for Modules Which Use the CSTM Data Block - 
Precision Version) .......................................... 3.4-66 (Table Look-Up) ............................................. 3.4-67 

3.4.40 3.4.41 3.4.42 3.4.43 3.4,44 3.4.45 3.4.46 3.4.47 3.4.48 3.4.49 3.4.50 3.4.51 3.4.52 3.4.53 3.4.54 3.4.55 3.4,56 3.4.57 3.4.58 3.4.59 3.4.60 
AXIS (Draw an Axis on a Plot) ...................................... 3.4-70 AXISi (Axis Routine for Plotter i) ................................. 3.4-72 SKPFRM (Skip a Variable Number of Frames) .......................... 3.4-73 SELCAM (To Initiate a New Plot) ................................... 3.4-74 IDPL_T (Generate an "ID" Plot) ..................................... 3.4-75 INTGPX (Search a List of Integers) ................................. 3.4-76 INTLST (Interpret a List of Integers) .............................. 3.4-77 LINE (Draw a Line on a Plotter) .................................... 3.4-78 LINEi (Draw a Line on Plotter i) ................................... 3.4-79 PRINT (Print a Title on a Plotter) ................................. 3.4-81 RDM_DX (Read a File Containing XRCARD Translations) ................ 3.4-83 SGINO (GI_!O for Unformatted Tapes) ................................. 3.4-85 STPL_T (To Initiate a New Plot or Terminate the Current Plot) ....... 3.4-87 SYMBOL (Type a Symbol on a Plotter) ................................ 3.4-88 TIPE (Type a Line of Characters on a Plotter) ...................... 3.4-90 TYPEi (Type a Line of Characters on Plotter i) ..................... 3.4-92 TYPFLT (Type a Floating Point Number on a Plotter) ................. 3.4-94 TYPINT (Type an Integer Number on a Plotter) ....................... 3.4-96 WPLTI (Write a Plotter Command for Plotter I) ...................... 3.4-98 WPLT2 (Write a Plotter Command for Plotters 2 and 8) ............... 3.4-100 
WPLT3 (Write a Plotter Command for Plotter 3) ...................... 3.4-102 viii (8/I/72)

Section 
TABLE OF CONTENTS (Continued) 
Page No. 

3.4.61 3.4.62 3.4.63 
3.4.64 3.4.65 3.4.66 
3.4.67 3.4.68 3.4.69 3.4.70 3.4.71 3.4.72 3.4.73 3.4.74 3.4.75 3.4.76 3.4.77 3.4.78 3.4.79 
GINOIO (GINO Input/Output Routine) ................................. 3.4-I03 EJECT (Automatic Page Eject) ....................................... 3.4-105 
PLAMAT (Material Property Utility for Two-Dimensional Elements in Piecewise Linear Analysis)....................................... 3.4-I06 
WPLT4 (Write a Plotter Command for Plotters 4 through 7) ........... 3.4-I08 WPLT9 (Write a Plotter Command for Plotter 9) ...................... 3.4-II0 
WPLTIO (Write a Plotter Command for the NASTRAN General Purpose Plotter) ........................................................... 3.4-III 
PLTSET (Plotting Parameter Initialization) ........................ 3.4-I13 DRWCHR (To Draw a Line of Characters) .............................. 3.4-I15 FNDPLT (Determine the Internal Plotter and Model Indices) .......... 3.4-I17 PHDMIA (DMI Punch Routine) ......................................... 3.4-I18 HEAD (Plot Heading) ................................................ 3.4-120 DELSET (Dummy Element Setup). ...................................... 3.4-121 HMAT (Heat Transfer Material Property Utility) ..................... 3.4-122 BISRCH (Binary Search) ............................................. 3.4-123 FORFIL (File Unit) ................................................. 3.4-126 DADOTB (Double Precision Vector Dot Product) ....................... 3.4-127 DAXB (Double Precision Vector Cross Product) ....................... 3.4-128 SADOTB (Single Precision Vector Dot Product) ....................... 3.4-129 SAXB (Single Precision Vector Cross Product) ....................... 3.4-130 

3.5 MATRIX SUBROUTINE DESCRIPTIONS ............................................. 3.5-I 

3.5 .l 3.5.2 3.5.3 3.5.4 
BLDPK (Build a Packed Column of a Matrix) .......................... 3.5-I PACK (Pack a Column of a Matrix) .................................. 3.5-5 INTPK (Interpret a Packed Column of a Matrix) ...................... 3.5-7 UNPACK (Unpack a Packed Column of a Matrix) ......................... 3.5-I0 

3.5.5 
CALCV 
(Compute a Partitioning Vector) .............................. 3.5-12 
3.5.6 
PARTN 
- MERGE (Partition a Matrix - Merge Matrices Together) ........ 3.5-13 
3.5.7 
SSG2A 
(Driver for PARTN) ........................................... 3.5-16 
3.5.8 
SDRIB 
(Driver for MERGE) ........................................... 3.5-17 
3.5.9 
UPART 
(Symmetric Partition Driver) ................................. 3.5-18 
ix (811172) 
L

TABLE OF CONTENTS (Continued) 
Section 
Page No. 

3.5.10 ADD (Driver for SADD) .............................................. 3.5-19 3.5.11 SSG2C (Driver for ADD) ............................................. 3.5-20 3.5.12 MPYAD (Matrix Multiplication Routine) .............................. 3.5-22 3.5.13 SSG2B (Driver for MPYAD) ........................................... 3.5-29 3.5.14 SDCOMP (Symmetric Decomposition) ................................... 3.5-30 3.5.15 DECOMP (Unsymmetric Matrix Decomposition) .......................... 3.5-44 3.5.16 CDCBMP (Complex Matrix Decomposition) .............................. 3.5-62 3.5.17 FBS (Forward - Backward Substitution) .............................. 3.5-64 3.5.18 SSG3A (Driver for FBS) ............................................. 3.5-66 3.5.19 GFBS (General Forward - Backward Substitution) ..................... 3.5-67 3.5.20 SOLVER (Simultaneous Equation Solution Routine) .................... 3.5-69 3.5.21 DMPY (Multiply a Diagonal Matrix by an Arbitrary Matrix) ........... 3.5-71 3.5.22 ELIM (Perform a Matrix Reduction) .................................. 3.5-73 3.5.23 FACTOR (Decompose a Matrix Into Triangular Factors) ................ 3.5-74 3.5.24 TRANPI (Driver for TRNSP) .......................................... 3.5-75 3.5.25 TRNSP (Matrix Transpose) ........................................... 3.5-76 3.5.26 SADD (Matrix Addition Routine) ..................................... 3.5-78 3.5.27 RSPSDC (Real Single Precision Symmetric Decomposition) ............. 3.5-80 3.5.28 CSPSDC (Complex Single Precision Symmetric Decomposition) .......... 3.5-82 3.5.29 CXFBS (Forward - Backward Substitution) ............................ 3.5-84 
4. 
MODULE FUNCTIONAL DESCRIPTIONS 
4.1 GENERAL COMMENTS AND INDEXES ............................................... 4.1-I 4.1.1 Use of Module Functional Descriptions .............................. 4.1-2 4.1.2 Alphabetical Index of Module Functional Descriptions .............. 4.1-7 
4.1.3 Alphabetical Index of Entry Points in Module Functional 
Descriptions ....................................................... 4.1-8 4.2 EXECUTIVE PREFACE MODULE XCSA (EXECUTIVE CONTROL SECTION ANALYSIS) ......... 4.2-I 4.3 EXECUTIVE PREFACE MODULE IFPI (INPUT FILE PROCESSOR, PART I) ............... 4.3-I 4.4 EXECUTIVE PREFACE MODULE XSORT (EXECUTIVE BULK DATA CARD SORT) ............. 4.4-I 4.5 EXECUTIVE PREFACE MODULE IFP (INPUT FILE PROCESSOR) ........................ 4.5-I 
x (811172)

Section 
4.6 
4.7 
4.8 
4.9 
4.10 
4.11 
4.12 
4.13 
4.14 
4.15 
4.16 
4.17 
4.18 
4.19 
4.20 
4.21 
4.22 
4.23 
4.24 
4.25 
4.26 
4.27 
4.28 
4.29 
4.30 
4.31 
4.32 
4.33 
4.34 
4.35 
TABLE OF CONTENTS (Continued) 
Page No. 
EXECUTIVE PREFACE MODULE IFP3 (II4PUTFILE PROCESSOR 3) ..................... 4.6-I EXECUTIVE PREFACE MODULE XGPI (EXECUTIVE GENERAL PROBLEM INITIALIZATION..... 4.7-I EXECUTIVE PREFACE MODULE UMFEDIT (USER MASTER FILE EDITOR) ................. 4.8-I EXECUTIVE MODULE XSFA (EXECUTIVE SEGMENT FILE ALLOCATOR) ................... 4.9-I EXECUTIVE DMAP MODULE CHKPNT (CHECKPOINT)................................... 4.10-1 
EXECUTIVE DMAP INSTRUCTION REPT (REPEAT A GROUP OF DMAP INSTRUCTIONS)....... 4.11-1 EXECUTIVE DMAP INSTRUCTION JUMP (UNCONDITIONAL DMAP TRANSFER) .............. 4.12-I EXECUTIVE DMAP INSTRUCTION C_ND (CONDITIONAL TRANSFER) ..................... 4.13-I EXECUTIVE DMAP INSTRUCTION EXIT (TERMINATE DMAP PROGRAM) ................... 4.14-I EXECUTIVE DMAP MODULE SAVE (SAVE VARIABLE PARAMETER VALUES) ................ 4.15-I EXECUTIVE DMAP MODULE PURGE (EXPLICIT DATA BLOCK PURGE) .................... 4.16-I EXECUTIVE DMAP MODULE EQUIV (DATA BLOCK NAME EQUIVALENCE) ................. 4.17-I EXECUTIVE DMAP INSTRUCTION END (END OF DMAP PROGRAM) ....................... 4.18-I EXECUTIVE DMAP MODULE PARAM (PARAMETER PROCESSOR) .......................... 4.19-I EXECUTIVE DMAP MODULE-SETVAL (SET VALUES) ................................. 4.20-I FUNCTIONAL MODULE GPI (GEOMETRY PROCESSOR - PHASE l) ....................... 4.21-I FUNCTIONAL MODULE GP2 (GEOMETRY PROCESSOR - PHASE 2) ....................... 4.22-I FUNCTIONAL MODULE PLTSET (PLOT SET DEFINITION PROCESSOR) ................... 4.23-I FUNCTIONAL MODULE PLBT (STRUCTURAL PLOTTER) ................................ 4.24-I FUNCTIONAL MODULE GP3 (GEOMETRY PROCESSOR - PHASE 3) ....................... 4.25-I FUNCTIONAL MODULE TAI (TABLE ASSEMBLER) .................................... 4.26-I FUNCTIONAL MODULE SMAI (STRUCTURAL MATRIX ASSEMBLER - PHASE l) ............. 4.27-I FUNCTIONAL MODULE SMA2 (STRUCTURAL MATRIX ASSEMBLER - PHASE 2) ............. 4.28-I FUNCTIONAL MODULE GPWG (GRID POINT WEIGHT GENERATOR) ....................... 4.29-I FUNCTIONAL MODULE SMA3 (STRUCTURAL MATRIX ASSEMBLER - PHASE 3).............. 4.30-I FUNCTIONAL MODULE GP4 (GEOMETRY PROCESSOR - PHASE 4) ........................ 4.31-I FUNCTIONAL MODULE GPSP (GRID POINT SINGULARITY PROCESSOR) .................. 4.32-I FUNCTIONAL MODULE MCEI (MULTIPOINT CONSTRAINT ELIMINATOR - PHASE l) ........ 4.33-I FUNCTIONAL MODULE MCE2 (MULTIPOINT CONSTRAINT ELIMINATOR - PHASE 2) ........ 4.34-I FUNCTIONAL MODULE SCEI (SINGLE-POINT CONSTRAINT ELIMINATOR) ................ 4.35-I 
xi (811172)
Secti on 
4.36 
4.37 
4.38 
4.39 
4.40 
4.41 
4.42 
4.43 
4.44 
4.45 
4.46 
4.47 
4.48 
4.49 
4.50 
4.51 
4.52 
4.53 
4.54 
4.55 
4.56 
4.57 
4.58 
4.59 
4.60 
4,61 
4.62 
4.63 
4.64 
TABLE OF CONTENTS (Continued) 
P_Pa_geNo. 
FUNCTIONAL MODULE SMPI (STRUCTURAL MATRIX PARTITIONER - PHASE I) .......... 4.36-I FUNCTIONAL MODULE RBMGI (RIGID BODY MATRIX GENERATOR - PHASE I) ........... 4.37-I FUNCTIONAL MODULE RBMG2 (RIGID BODY MATRIX GENERATOR - PHASE 2) ........... 4.38-I FUNCTIONAL MODULE RBMG3 (RIGID BODY MATRIX GENERATOR - PHASE 3) ........... 4.39-I FUNCTIONAL MODULE RBMG4 (RIGID BODY MATRIX GENERATOR - PHASE 4) ........... 4.40-I FUNCTIONAL MODULE SSGI (STATIC SOLUTION GENERATOR - PHASE I) .............. 4.41-I FUNCTIONAL MODULE SSG2 (STATIC SOLUTION GENERATOR - PHASE 2) .............. 4.42-I FUNCTIONAL MODULE SSG3 (STATIC SOLUTION GENERATOR - PHASE 3) .............. 4.43-I FUNCTIONAL MODULE SSG4 (STATIC SOLUTION GENERATOR - PHASE 4) .............. 4.44-I FUNCTIONAL MODULE SDRI (STRESS DATA RECOVERY - PHASE I) ................... 4.45-I FUNCTIONAL MODULE SDR2 (STRESS DATA RECOVERY - PHASE 2) ................... 4.46-I FUNCTIONAL MODULE DPD (DYNAMICS POOL DISTRIBUTOR) ......................... 4.47-I FUNCTIONAL MO[ULE READ (REAL EIGENVALUE ANALYSIS - DISPLACEMENT) .......... 4.48-I 
FUNCTIONAL MODULE DSMGI (DIFFERENTIAL STIFFNESS MATRIX GENERATOR - PHASE I) .................................................................. 4.49-I 
FUNCTIONAL MODULE SMP2 (STRUCTURAL MATRIX PARTITIONER - PHASE 2) .......... 4.50-I 
FUNCTIONAL MODULE DSMG2 (DIFFERENTIAL STIFFNESS MATRIX GENERATOR - PHASE 2) .................................................................. 4.51-I 
FUNCTIONAL MODULE PLAI (PIECEWISE LINEAR ANALYSIS - PHASE I) .............. 4.52-I FUNCTIONAL MODULE PLA2 (PIECEWISE LINEAR ANALYSIS - PHASE 2) .............. 4.53-I FUNCTIONAL MODULE PLA3 (PIECEWISE LINEAR ANALYSIS - PHASE 3) .............. 4.54-I FUNCTIONAL MODULE PLA4 (PIECEW!SE LINEAR ANALYSIS - PHASE 4) .............. 4.55-I FUNCTIONAL MODULE CASE (SIMPLIFY CASE CONTROL) ............................ 4.56-I FUNCTIONAL MODULE MTRXIN (MATRIX INPUT) ................................... 4.57-I FUNCTIONAL MODULE GKAD (GENERAL K ASSEMBLER DIRECT) ....................... 4.58-I FUNCTIONAL MODULE CEAD (COMPLEX EIGENVALUE ANALYSIS - DISPLACEMENT) ........ 4.59-I FUNCTIONAL MODULE VDR (VECTOR DATA RECOVERY) .............................. 4.60-I FUNCTIONAL MODULE FRRD (FREQUENCY RESPONSE - DISPLACEMENT APPROACH) ........ 4.61-I 
FUNCTIONAL MODULE SDR3 (STRESS DATA RECOVERY - PHASE 3 - S@RTI to S_RT2 PROCESSOR) .......................................................... 4.62-I 
FUNCTIONAL MODULE XYTRAN (XY - OUTPUT DATA TRANSLATOR) .................... 4.63-I FUNCTIONAL MODULE RANDOM (RANDOM ANALYSIS MODULE) .......................... 4.64-I 
xii (8/I/72)
TABLEOFCONTENTS (Continued) 
Section 
Page No. 

4.65 
FUNCTIONAL MODULE TRD (TRANSIENT ANALYSIS - DISPLACEMENT) ................. 4.65-I 4.66 
FUNCTIONAL MODULE GKAM (GENERAL K ASSEMBLER ,MODAL) ........................ 4.66-I 4.67 
FUNCTIONAL MODULE DDRI (DYNAMIC DATA RECOVERY - PART l) ................... 4.67-I 4.68 
FUNCTIONAL MODULE DDR2 (DYNAMIC DATA RECOVERY - PART 2) ................... 4.68-I 4.69 
OUTPUT MODULE XYPLOT (X-Y DATA PLOTTER) ................................... 4.69-I 4.70 
OUTPUT MODULE BFP (OUTPUT FILE PROCESSOR) ................................. 4.70-I 4.71 
OUTPUT MODULE MATPRN (GENERAL MATRIX PRINTER) ............................. 4.71-I 4.72 
OUTPUT MODULE MATGPR (DISPLACEMENT METHOD MATRIX PRI_ITER) ................. 4.72-I 4.73 
OUTPUT MODULE MATPRT (MATRIX PRINTER) .................................... 4.73-I 4.74 
OUTPUT MODULE SEEMAT (PICTORIAL MATRIX PRINTER) ........................... 4.74-I 4.75 
OUTPUT MODULE TABPT (TABLE PRINTER) ....................................... 4.75-I 4.76 
OUTPUT MODULE PRTMSG (MESSAGE WRITER) ..................................... 4.76-I 4.77 
OUTPUT MODULE PRTPARM (PARAMETER AND DMAP MESSAGE PRINTER) ................ 4.77-I 4.78 
MATRIX MODULE ADD (ADD TWO MATRICES) ...................................... 4.78-I 4.79 
.MATRIX MODULE MPYAD (MULTIPLY ADD) ........................................ 4.79-I 4.80 
MATRIX MODULE S_LVE (SOLVES THE MATRIX EQUATION [A][X] = [B]) .............. 4.80-I 4.81 
MATRIX MODULE DECAMP (MATRIX DECOMPOSITION) ............................... 4.81-I 4.82 
MATRIX MODULE FBS (FORWARD - BACKWARD SUBSTITUTION) ....................... 4.82-I 4.83 
MATRIX MODULE PARTN (PARTITION A MATRIX) .................................. 4.83-I 4.84 
MATRIX MODULE MERGE (MERGE MATRICES TOGETHER) ............................. 4.84-I 4.85 
MATRIX MODULE TRNSP (TRANSPOSE A MATRIX) .................................. 4.85-I 4.86 
MATRIX MODULE SMPYAD (STRI?IG MULTIPLY ADD) ................................. 4.86-I 4.87 
STRUCTURAL ELEMENT DESCRIPTIONS .......................................... 4.87-I 4.87.1 The R_D, C_IRBD, and TUBE Elements ............................... 4.87-7 4.87.1.1 Input Data for the R_D, TUBE, CBNR_D Elements ......... 4.87-7 
4.87.1.2 Stiffness Matrix Calculation (Subroutine KR_D 
and KTUBE of Module SMAI) ............................. 4.87-8 
4.87.1.3 Lumped Mass Matrix Calculation (Subroutine MR_D 
and MTUBE of Module SMA2) ............................. 4.87-9 
4.87.1.4 Element Load Calculations (Subroutine EDTL of 
Module SSGI) .......................................... 4.87-10 
4.87.1.5 Element Stress Calculations (Subroutines SR_DI 
and SR_D2 of Module SDR2) ............................. 4.87-10 
xiii (8/I/72)

Secti on 
4.87.2 
4.87.3 
TABLE OF CONTENTS (Continued) 
Page No. 
4.87.1.6 Differential Stiffness Matrix Calculation (Subroutine DROD of Module DSMGI) .................................. 4.87-12 
4.87.1.7 Piecewise Linear Analysis Calculations (Subroutine PSROD of Module PLA3 and Subroutine PKROD of Module 
PLA4) ................................................. 4.87-14 
4.87.1.8 Coupled Mass Matrix Calculation (Subroutine MCROD of Module SMA2) .......................................... 4.87-16a 
4.87.1.9 Thermal Analysis Calculations for the ROD Elements (Subroutine KROD of Module SMAI) ...................... 4.87-16b 
The BAR Element .................................................. 4.87-17 4.87.2.1 Input Data for the BAR Element ....................... 4.87-17 
4.87.2.2 Stiffness Matrix Calculation (Subroutine KBAR of Module SMAI) .......................................... 4.87-18 
4.87.2.3 Lumped Mass Matrix Calculation (Subroutine MBAR of Module SMA2) .......................................... 4.87-25 
4.87.2.4 Element Load Calculation (Subroutine BAR of Module SSGI) ................................................. 4.87-26 
4.87.2.5 Element Stress Calculations (Subroutines SBARI and SBAR2 of Module SDR2) ................................. 4.87-27 
4.87.2.6 Differential Stiffness Matrix Calculation (Subroutine DBEAM of Module DSMGI) ................................ 4.87-29 
4.87.2.7 Piecewise Linear Analysis Calculations (Subroutine PSBAR of Module PLA3 and Subroutine PKBAR of Module 
PLA4 .................................................. 4.87-32 
4.87.2.8 "Consistent" Mass Matrix Calculation (Subroutine 
MCBAR of Module SMA2) ................................. 4.87-36 
4.87.2.9 Thermal Analysis Calculations for the BAR Element (Subroutine KBAR of Module SMAI) ...................... 4.87-37 
The SHEAR Panel and TWIST Panel Elements ......................... 4.87-38 

4.87.3.1 4.87.3.2 4.87.3.3 4.87.3.4 
4.87.3.5 4.87.3.6 
Input Data for SHEAR and TWIST Panels ................. 4.87-38 Definition of Element Geometry ........................ 4.87-39 Coefficient Generation ................................ 4.87-41 
Stiffness Matrix Formulation for a SHEAR Panel 
(Subroutine KPANEL of Module SMAI) .................... 4.87-46 
TWIST Element Stiffness Matrix Generation (Subroutine KPANEL of Module SMAI) ................................ 4.87-47 
Mass Matrix Generation (Subroutine MASSTQ of Module SMA2) ................................................. 4.87-48 
xiv (8/I/72)

Section 
4.87.4 
4.87.5 
TABLE OF CONTENTS (Continued) 
Page No. 
4.87.3.7 SHEAR Element Stress and Force Calculations 
(Subroutine SPANLI and SPANL2 of Module SDR2) .......... 4.87-50 
4.87.3.8 TWIST Element Stress and Force Calculations 
(Subroutines SPANLI and SPANL2 of Module SDR2)......... 4.87-52' 
4.87.3.9 SHEAR Panel Differential Stiffness Calculations (Subroutine DSHEAR of Module DSMGI) ................... 4.87-54 
TRMEM and QDMEM Elements ......................................... 4.87-58 4.87.4.1 Input Data for the TRMEM and QDMEM Elements ........... 4.87-58 4.87.4.2 Basic Equations for TRMEM ............................. 4.87-59 
4.87.4.3 Stiffness Matrix Calculation for TRMEM (Subroutine KTRMEM of Module SMAI) ................................ 4.87-61 
4.87.4.4 Mass Matrix Calculation for the TRMEM Element 
(Subroutine MASSTQ of Module SMA2) .................... 4.87-62 
4.87.4.5 Element Load Calculations for the TRMEM Element (Subroutine TRIMEM of Module SSGI) .................... 4.87-63 
4.87.4.6 Element Stress Calculations for the TRMEM Element (Subroutines STRMEI and STQME2 of Module SDR2) ........ 4.87-63 
4.87.4.7 Differential Stiffness Matrix Calculations for the TRMEM Element (Subroutine DTRMEM of Module DSMGI)...... 4.87-67 
4.87.4.8 General Calculations for the QDMEM by the QDMEM Driver Routines (Subroutines KQDMEM of Module SMAI, 
SQDMEI of Module SDR2, DQDMEM of Module DSMGI)......... 4.87-67 4.87.4.9 Stiffness Matrix Calculations for the QDMEM .......... 4.87-70 
4.87.4.10 Element Stress Calculations for the QDMEM (Subroutine SQDMEI and STQME2 of Module SDR2) ..................... 4.87-70 
4.87.4.11 Mass Matrix Generation for the QDMEM Element 
(Subroutine MASSTQ of Module SMA2) .................... 4.87-74 4.87.4.12 Thermal Load Computation for the QDMEM ............... 4.87-76 
4.87.4.13 Differential Stiffness Computations for the QDMEM (Subroutines DQDMEM and DTRMEM of Module DSMGI) ....... 4.87-76 
4.87.4.14 Piece_ise Linear Analysis Calculations (Subroutines PSTRM and PSQDM of Module PLA3 and Subroutines 
PKTRM and PKQDM of Module PLA4)........................ 4.87-76a 
4.87.4.15 Thermal Analysis Calculations for the Membrane 
Elements (Subroutine KTRMEM and KQDMEM of Module 
SMAI) ................................................. 4.87-76d The TRBSC, TRPLT and QDPLT Elements .............................. 4.87-78 4.87.5.1 Input Data for the TRBSC and TRPLT Elements ........... 4.87-78 4.87.5.2 General Calculation for the TRBSC Element ............ 4.87-79 
xv (811172)
TABLE OF CONTENTS (Continued) 
Section 
Pa_a_eNo. 
4.87.6 
4.87.5.3 
4.87.5.8 
4.87.5.9 
4.87.5.10 
4.87.5.11 
4.87.5.12 
4.87.5.13 
4.87.5.14 
The TRIAl, 4.87.6.1 
4.87.6.2 
4.87.6.3 
4.87.6.4 
4.87.6.5 
4.87.6.6 
4.87.6.7 
Stiffness Matrix Calculations for the TRBSC Element (Subroutine KTRBSC of Module SMAI) .................... 4.87-84 
Stress Calculations for the TRBSC Element ............. 4.87-85 
Stiffness Matrix Calculations for the TRPLT Element (Subroutine KTRPLT of Module SMAI) .................... 4.87-87 
Structural Damping Matrices for the TRPLT Element ..... 4.87-95 
Stress and Element Force Calculations for the TRPLT Element (Subroutines STRPLI and SBSPL2 of Module 
SDR2) ................................................. 4.87-95 
Stiffness Matrix Calculations for the QDPLT Element (Subroutine KQDPLT of Module SMAI) .................... 4.87-97 
Stress and Element Force Calculations for the QDPLT Element (Subroutines SQDPLI and SBSPL2 of Module 
SDR2) ................................................. 4.87-102 
Lumped Mass Matrix Generation for the TRBSC, TRPLT, and QDPLT Elements (Subroutine MASSTQ of Module SMA2).. 4.87-104 
Coupled Mass Matrix Calculations for the TRBSC Element (Subroutine MTRBSC of Module SMA2) ..................... 4.87-I04a 
Mass Matrix Calculations for the TRPLT Element 
(Subroutine MTRPLT of Module SMA2) .................... 4.87-I04g 
Mass Matrix Calculations for the QDPLT Element 
(Subroutine MQDPLT of Module SMA2) .................... 4.87-I04j 
Thermal Load Equations for the Bending Element 
(Subroutine TRBSC, TRPLT and QDPLT of Module SSGI) .... 4.87-I04n TRIA2, QUADI and QUAD2 Elements ....................... 4.87-106 
Input Data for the TRIAl, TRIA2, QUADI and QUAD2 
Elements .............................................. 4.87-106 
Stiffness Matrix Calculations (Subroutine KTRIQD 
of Module SMAI) ....................................... 4.87-107 
Lumped Mass Matrix Generation (Subroutine MASSTQ 
of Module SMA2) ....................................... 4.87-108 
Thermal Load Calculations (Subroutine EDTL of Module SSGI) ................................................. 4.87-108 
Element Stress and Force Calculations (Subroutines 
STRQDI and STRQD2 of Module SDR2) ..................... 4.87-108 
Differential Stiffness Matrix Calculations 
(Subroutine MTRIQD of Module SMA2) .................... 4.87-I09 
Piecewise Linear Analysis Calculations (Subroutines 
PSTRII, PSTRI2, PSQADI, and PSQAD2 of Module PLA3, and PKTRII, PKTRI2, PKQADI and PKQAD2 of Module 
PLA4) ................................................. 4.87-I09a xvi (811/72)

Secti on 
4.87.6.8 
4.87.6.9 
TABLE OF CONTENTS (Continued) 
Page No. 
Differential Stiffness Matrix Calculations for the TRIAl and TRIA2 Elements (Subroutine DTRIA of 
Module DSMGI) ........................................ 4.87-I09d 
Differential Stiffness Matrix Calculations for the QUADI and QUAD2 Elements (Subroutine DQUAD of 
Module DSMGI) ........................................ 4.87-I09g 

4.87.7 
4.87.8 
4.87.9 
4.87.6.10 Differential Stiffness Matrix Calculations for the Basic Bending Triangle (Subroutine DTRBSC of 
Module DSMGI) ........................................ 4.87-I09j 
4.87.6.11 Thermal Calculations for the Combination Elements (Subroutine KTRIQD of Module SMAI) .................... 4.87-I09p 
The ELASi, MASSi and DAMPi Elements ............................... 4.87-II0 4.87.7.1 Input Data for the ELASi, MASSi and DAMPi Elements .... 4.87-II0 
4.87.7.2 ELASi Stiffness Matrix Generation (Subroutine KELAS of Module SMAI) ...................................... 4.87-II0 
4.87.7.3 MASSi Mass Matrix Generation (Subroutine MASSD of Module SMA2) ......................................... 4.87-III 
4.87.7.4 DAMPi Damping Matrix Generation (Subroutine MASSD of Module SMA2) ...................................... 4.87-III 
4.87.7.5 ELASi Stress and Force Recovery (Subroutines SELASI and SELAS2 of Module SDR2) ........................... 4.87-III 
Concentrated Mass Elements C_NMI, C_NM2 ......................... 4.87-113 4.87.8.1 ECPT Entries for the C_NMI Mass Element .............. 4.87-113 
4.87.8.2 Mass Matrix Calculations for the CONMI Element 
(Subroutine MC_NMX of Module SMA2) ................... 4.87-113 4.87.8.3 ECPT Entries for the COHM2 Mass Element .............. 4.87-114 
4.87.8.4 Mass Matrix Calculations for the CONM2 Element 
(Subroutine MCBNMX of Module STY2) .................. 4.87-114 The CONEAX Element ............................................... 4.87-117 4.87.9.1 Input Data for the CONEAX Element .................... 4.87-117 
4.87.9.2 Stiffness Matrix Calculations (Subroutine KCONE of Module SMAI) ......................................... 4.87-117 
4.87.9.3 Mass Matrix Computation (Subroutine MCONE of Module SMA2) ................................................ 4.87-118 
4.87.9.4 Element Load Calculations (Subroutine CONE of Module SSGI) ................................................. 4.87-118 
4.87.9.5 Element Stress Calculations (Subroutines SCONE1, SCONE2, SC@NE3 of Module SDR2) ....................... 4.87-123 
4.87.9.6 Differential Stiffness Matrix Calculations (Subroutine DCONE of Module DSMGI) ............................... 4.87-127a 
xvii (8/I/72)
Section 
4.87.10 
4.87.11 
4.87.12 
TABLE OF CONTENTS (Continued) 
No. 
The TRIARG Element ............................................... 4.87-128 4.87.10.1 Input Data for the TRIARG Element .................... 4.87-128 4.87.10.2 General Geometric Calculations ....................... 4,87-129 4.87.10.3 Integral Calculations ................................ 4.87-130 4.87.10.4 Elastic Constants Matrix Calculations ............... 4.87-132 
4.87.10.5 Stiffness Matrix Generation (Subroutine KTRIRG of Module SMAI) ......................................... 4.87-133 
4.87.10.6 Mass Matrix Calculations (Subroutine MTRIRG of Module SMA2) ......................................... 4,87-135 
4.87.10.7 Thermal Load Calculations (Subroutine TTRIRG of Module SSGI) .......................................... 4.87-136 
4.87.10.8 Element Force and Stress Calculations (Subroutines STRIRI and STRIR2 of Module SDR2) .................... 4.87-136 
4.87.10.9 Thermal Analysis Calculations for the TRIARG and TRAPRG Elements (Subroutine HRING of Module SMAI) ..... 4.87-138a 
The TRAPRG Element .............................................. 4.87-139 4.87.11.1 Input Data for the TRAPRG Element .................... 4.87-139 4.87.11.2 General Calculations ................................. 4.87-140 4,87.11.3 Integral Calculations ................................ 4.87-142 4.87.11.4 Elastic Constants Matrix Calculation ................. 4.87-144 
4.87.11.5 Stiffness Matrix Generation (Subroutine KTRAPR of Module SMAI) ......................................... 4.87-144 
4.87.11.6 Mass Matrix Calculation (Subroutine MTRAPR of Module SMA2) ......................................... 4.87-146 
4.87.11.7 Thermal Load Calculations (Subroutine TTRAPR of Module SSGI) ......................................... 4.87-147 
4.87.11,8 Element Force and Stress Calculations (Subroutines STRAP1 and STRAP2 of Module SDR2) .................... 4.87-148 
4.87.11.9 Thermal Analysis Calculations for the TRAPRG Element (Subroutine HRING of Module SMAI) .................... 4.87-151 
The T_RDRG Element .............................................. 4.87-152 

4.87.12.1 4,87.12,2 4.87.12.3 4.87.12.4 
Input Data for the T@RDRG Element .................... 4.87-152 General Calculations ................................. 4.87-153 Integral Calculations ................................ 4,87-156 Elastic Constants Matrix Calculations ................ 4.87-160 
xviii (8/I/72)

TABLE OF CONTENTS (Continued) 
Section 
4.87.12.5 Stiffness Matrix Calculations (Subroutine KT_RDR 
Page No. 

4.87.13 
of Module SMAI) ...................................... 4.87-160 
4.87.12.6 Mass Matrix Calculations (Subroutine MT_RDR of Module SMA2) ......................................... 4.87-165 
4.87.12.7 Thermal Load Calculations (Subroutine TT_RDR of Module SSGI) ........................................ 4.87-166 
4.87.12.8 Element Force and Stress Calculations (Subroutines STORDI and STORD2 of Module SDR2) .................... 4.87-168 
The VISC Element ................................................. 4.87-175 
4.87.13.1 4.87.13.2 
Input Data for the VISC Element ...................... 4.87-175 
Damping Matrix Calculations (Subroutine BVISC of Module SMA2) ......................................... 4.87-175 
4.87.14 
Integral Calculations for the TRIARG, TRAPRG Elements ............ 4.87-177 
4.87.14.1 4.87.14.2 4.87.14.3 4.87.14.4 4.87.14.5 4.87.14.6 
Integral Calculation for q > 0 and any p. (Function DKINT) .................... ? .......................... 4.87-179 
Integral Calculation for p > 0 and q < - l (Function DK8g) ..................... _ .......................... 4.87-179 
Integral Calculation for p < 0 and q < - l (Function DKIO0) ................................................ 4.87-180 
Integral Calculations for p > - l and q = -l (Function DKJAB) ............................................... 4.87-181 
Integral Calculations for p < - l and q = -l (Function DK219) ............................................... 4.87-182 
Integral Calculations for p = -l and q = -l (Function DK211) ............................................... 4.87-182 
4.87.15 
The FLUID2, FLUID3, FLUID4, AXIF2, AXIF3, AXlF4, and MFREE Elements ........................................................ 4.87-183 
4.87.15.1 4.87.15.2 
4.87.15.3 4.87.15.4 4.87.15.5 
Input Data for the Fluid Elements .................... 4.87-183 
Matrix Calculations for the FLUID2 Element 
(Subroutine KFLUD2 of Module SMAI and Subroutine 
MFLUD2 of Module SMA2) ............................... 4.87-183 
Matrix Calculations for the FLUID3 Element 
(Subroutine KFLUD3 of Module SMAI and Subroutine 
MFLUD3 of Module SMA2) ............................... 4.87-186 
Matrix Generation for the FLUID4 Element 
(Subroutine KFLUD4 in Module SMAI and Subroutine 
MFLUD4 in Module SF_2) ............................... 4.87-188 
Matrix Calculations for the MFREE Element (Subroutine MFREE in Module SMA2) ................................ 4.87-189 
xix (8/I/72)

Section 
4.87.16 
4.87.17 
TABLE OF CONTENTS (Continued) 
Page No. 
4.87.15.6 Stress Calculations for the AXIF Elements, 
Phase 1 .............................................. 4.87-189 
4.87.15.7 Stress Calculations for the AXIF Elements, 
Phase 2 .............................................. 4.87-194 The SL_T3 and SLOT4 Fluid Elements ............................... 4.87-194 4.87.16.1 Input Data for the SL_T3 and SL_T4 Elements .......... 4.87-194 4.87.16.2 General Calculations for the SLOT Elements ........... 4.87-195 4.87.16.3 Stiffness Matrix Generation for the SL_T3 Elements .... 4.87-195 4.87.16.4 Mass Matrix Generation for the SL@T3 Elements ........ 4.87-196 
4.87.16.5 Stress Matrix Calculations in the SL_T Elements (Phase I) ............................................ 4.87-196 
4.87.16.6 CSLOTi Element, Phase 2 ............................. 4.87-198 Solid Polyhedra Elements, TETRA, WEDGE, HEXAI, HEXA2 ............. 4.87-199 4.87.17.1 Input Data for the Solid Polyhedra Elements .......... 4.87-199 4.87.17.2 Basic Equations for the TETRA Element ................ 4.87-200 
4.87.17.3 Stiffness Matrix Generations for the TETRA Element (Subroutine KTETRA of Module SMAI) ................... 4.87-201 
4.87.17.4 Mass Matrix Generation for the TETRA Element 
(Subroutine MSOLID of Module SMA2) ................... 4.87-201 
4.87.17.5 Thermal Load Generation for the TETRA Element 
(Subroutine TETRA of Module SSGI) .................... 4.87-201 
4.87.17.6 Stress Calculations for the TETRA Elements 
(Subroutines SSOLIDI and SSOLID2 of Module SDR2) ..... 4.87-202 
4.87.17.7 Basic Equations for the WEDGE, HEXAI, and HEXA2 Elements ............................................. 4.87-203 
4.87.17.8 Stiffness Matrix Calculations and Geometry Checks for the WEDGE, HEXAI, and HEXA2 Elements (Subroutine 
KSOLID of Module SMAI) ............................... 4.87-204 
4.87.17.9 Mass Matrix Generation for the WEDGE, HEXAI, and HEXA2 Elements (Subroutine MSOLID of Module SMA2) ..... 4.87-205 
4.87.17.10 Thermal Load Generation for the WEDGE, HEXAI, and IIEXA2 Elements (Subroutine S_LID of Module SSG2) ...... 4.87-206 
4.87.17.11 Stress Data Recovery for the WEDGE, HEXAI, and IIEXA2 Elements (Subroutines SSOLIDI and SS_LID2 of 
Module SDR2) ......................................... 4.87-206 
4.87.17.12 Thermal Analysis Calculations for the Solid Elements (Subroutine KTETRA of Module SMAI) ................... 4.87-207 
xx (811172)

TABLE OF CONTENTS (Continued) 
Section 
e_. a 
4.87.18 The HBDY Elements ................................................ 4.87-208 4.87.18.1 Input Data for the HBDY Elements ..................... 4.87-208 
4.87.18.2 Stiffness Matrix Calculations (Subroutine HBDY 
of Module SMAI) ..................................... 4.87-208 
4.87.18.3 HBDY Element Thermal Loads (Subroutine HBDY of 
Module SSGI) ......................................... 4.87-210 
4.88 
DETERMINANT METHOD OF EIGENVALUE EXTRACTION .............................. 4.88-I 4.89 
EXECUTIVE PREFACE MODULE IFP4 (INPUT FILE PROCESSOR - PHASE 4) ............ 4.89-I 4.90 
FUNCTIONAL MODULE BMG (BOUNDARY MATRIX GENERATOR FOR HYDROELASTIC 
PROBLEMS) .................................................................. 4.90-I 4.91 
EXECUTIVE PREFACE MODULE IFP5 (INPUT FILE PROCESSOR - PHASE 5) ............. 4.91-I 4.92 
FUNCTIONAL MODULE PLI-TRAN ................................................. 4.92-I 4.93 
MATRIX MODULE UPARTN (PARTITIONS A MATRIX BASED ON USET) .................. 4.93-I 4.94 
MATRIX MODULE UMERGE (MERGES TWO MATRICES BASED ON USET) .................. 4.94-I 4.95 
MATRIX MODULE VEC (CREATES PARTITIONING VECTOR BASED ON USET) ............. 4.95-I 4.96 
MATRIX MODULE ADD5 (ADD MATRICES) ......................................... 4.96-I 4.97 
FUNCTIONAL MODULE INPUT (INPUT GENERATOR) ................................. 4.97-I 4.98 
FUNCTIONAL MODULE INPUTTI ................................................. 4.98-I 4.99 
FUNCTIONAL MODULE INPUTT2 ................................................. 4.99-I 4.100 
FUNCTIONAL MODULE BUTPUTI ................................................. 4.100-I 4.101 
FUNCTIONAL MODULE _UTPUT2 ................................................. 4.101-I 4.102 
OUTPUT MODULE _UTPUT3 ..................................................... 4.102-I 4.103 
OUTPUT MODULE TABPRT (FORMATTED TABLE PRINTER) ............................ 4.103-I 
5. 
NASTRAN - OPERATING SYSTEM INTERFACES 
5.1 INTRODUCTION .............................................................. 5.1-I 5.2 NASTRAN On The IBM 7094/7040(44) DCS (IBSYS) D E L E T E D ........... 5.2-I 5.3 NASTRAN ON THE IBM SYSTEM 360-370 OPERATING SYSTEM (_S) ................... 5.3-I 
5.3.1 
Introduction ..................................................... 5.3-I 5.3.2 
Input/Output .................................................... 5.3-I 5.3.3 
Link Switching ................................................... 5.3-4 5.3.4 
Overlay Considerations and Implementation of Open Core ............ 5.3-4 5.3.5 
Execution Deck Setup ............................................. 5.3-6 xxi (8/I/72)
Section 
5.4 
5.5 
TABLE OF CONTENTS (Continued) 
Page No. 
5.3.6 Physical Items and Generation of NASTRAN Executable System ....... 5.3-13 5.3.7 Machine Dependent Routines ....................................... 5.3-17 5.3.8 GIN_ (Generalized Input/Output Processor for NASTRAN) ............ 5.3-20 5.3.9 Special Error Codes from NASTRAN on the System 360 .............. 5.3-22 5.3.10 System 360 F_RTRAN Compilers used for NASTRAN .................... 5.3-23 5.3.11 IBM 360-370 Overlay Charts ....................................... 5.3-24 NASTRAN ON THE UNIVAC 1108 (EXEC 8) ....................................... 5.4-I 
5.4.1 Introduction ..................................................... 5.4-I 5.4.2 Input/Output ..................................................... 5.4-I 5.4.3 Link Switching ................................................... 5.4-4 5.4.4 Overlay Considerations and Implementation of Open Core ........... 5.4-5 5,4.5 Execution Deck Setup ............................................. 5.4-7 
5.4.6 Description of NASTRAN Physical Items and Generation of the NASTRAN Executable System ........................................ 5.4-10 
5.4.7 Machine Dependent Routines ...................................... 5.4-12 5.4.8 Procedure to Copy the Three System Tapes ......................... 5.4-15 5.4.9 NASTRAN Tapes (Files) Catalogue Procedure ........................ 5.4-17 5.4.10 NASTRAN Update Procedure ......................................... 5.4-19 5.4,11 Regenerate the Executable Tape .................................. 5.4-20 5.4.12 The ASGCRDS Program File ......................................... 5.4-22 5.4.13 The C_NTRL or C_NTRL42K Program File ............................ 5.4-23 5.4.14 Description of a Demonstration Problem Starter Deck .............. 5.4-24 
5.4.15 Tape and Problem Numbers for the NASTRAN Demonstration Problem Input Data Tape .................................................. 5.4-27 
5.4.16 GIN_ (Generalized Input/Output for NASTRAN) ...................... 5.4-28 5.4.17 Matrix Packing Routines .......................................... 5.4-32 5.4.18 1108 Time Estimation ............................................. 5.4-38 5.4.19 Single Precision Routines ....................................... 5.4-38 5.4.20 UNIVAC Overlay Diagrams .......................................... 5.4-39 NASTRAN ON THE CDC 6400/6600 (SCOPE 3) .................................... 5.5-I 
5.5.1 Introduction .................................................... 5.5-I 5.5.2 Input/Output ..................................................... 5.5-2 
xxii (8/I/72)

TABLE OF CONTENTS (Continued) 
Section 
Page No. 

5.5.3 5.5.4 5.5.5 5.5.6 
Layout of Core Storage ........................................... 5.5-4 Execution Deck Setup ............................................. 5.5-6 Physical Deliverables and Generation of Executable System ........ 5.5-9 Machine Dependent Routines ....................................... 5.5-12 

5.6 THE CDC 6400/6600 LINKAGE EDITOR .......................................... 5.6-I 5.6.1 Introduction .................................................... 5.6-I 5.6.2 Preparing for Linkage Editor Processing .......................... 5.6-6 5.6.3 Designing an Overlay Program ..................................... 5.6-7 5.6.4 Linkage Editor Control Statements ................................ 5.6-12 
5.6.5 Examples of Linkage Editor Processing ............................ 5.6-23 5.6.6 Storage Requirements for the Linkage Editor ...................... 5.6-29 5.6.7 Link-Edited Linkage Editor ....................................... 5.6-30 
6. 
MODIFICATIONS AND ADDITIONS TO NASTRAN 
6.1 INTRODUCTION .............................................................. 6.l-I 6.2 FBRTRAN IV LANGUAGE RESTRICTIONS .......................................... 6.2-I 6.3 THE EXECUTIVE CONTROL DECK ................................................ 6.3-I 
6.3.1 The NASTRAN Card ................................................. 6.3-I 6.4 THE CASE CONTROL DECK ..................................................... 6.4-I 6.5 THE BULK DATA DECK ........................................................ 6 5-I 6.6 RIGID FORMATS ............................................................. 6.6-I 6.7 FUNCTIONAL MODULES ........................................................ 6 7-I 6.8 ADDING A STRUCTURAL ELEMENT ............................................... 6 8-I 
6.8.1 Introduction to the Problem ...................................... 6.8-I 6.8.2 General Guidelines ............................................... 6 8-16 6.8.3 Specific Checklists .............................................. 6.8-27 6.8.4 Updating the NASTRAN Manuals ..................................... 6.8-49 6.8.5 Dummy User Elements (DUMI through DUM9) .......................... 6.8-54 
6.9 PRINTED OUTPUT ............................................................ 6.9-I 6.10 PLOTTER OUTPUT ............................................................ 6.10-1 6.10.1 Changes to the Plotter Software .................................. 6.10-1 
xxiii (8/I/72)

TABLE OF CONTENTS (Continued) 
Section 
Pa_e No. 

6.11 
6.10.2 
6.10.3 
6.10.4 
6.10.5 
6.10.6 
ADDITION 6.11 .I 
6.11.2 
Changes to the PL_T Module, the Structural Plotter .............. 6.10-3 Changes to the XYPLOT Module, the XY Plotter .................... 6.10-4 Changes to the SEEMAT Module, the Matrix Plotter ................ 6.10-4 Use of the NASTRAN Plotter Software in a New Module ............. 6.10-6 NASTRAN General Purpose Plotter ................................. 6.10-14 
OF A NEW LINK ................................................... 6.11-I Modules to Include .............................................. 6.11-I Addition of _ew Modules ......................................... 6.11-I 
6.11.3 
6.11.4 6.11.5 
Generation of a New Link Specification Table and a New Link Driver .......................................................... 
Subsys the New Link ............................................. 
Increasing the Link Limit ....................................... 
6.11-2 6.11-4 6.11-4 
6.12 
WRITING A NEW MODULE ..................................................... 
6.12-I 
6.12,1 
6.12.2 
6.12.3 
6.12.4 
6.12.5 
7, 
NASTRAN SUPPORT 
Summary of NASTRAN Coding Conventions and Terminology ........... Module Design ................................................... 
Implementing the New Module ..................................... 
Coding a Module Subroutine ...................................... 
Sample Module Coding ............................................ 
PROGRAMS 
6.12-I 6.12-3 6.12-7 6.12-8 6.12-12 

7.1-I 
7.1 
INTRODUCTION ............................................................. 
7.2-I 
7.2 
DESIGN OF THE CDC 6400/6600 LINKAGE EDITOR ............................... 
7.2.1 
Introduction .................................................... 7.2-2 7.2.2 
Discussion of the Major Divisions of the Linkage Editor/Loader .. 7.2-14 7.2.3 
Flowcharts ...................................................... 7.2-79 7.2.4 
Subroutine Descriptions ......................................... 7.2-134 7.2.5 
Object Deck Format .............................................. 7.2-176 7.2.6 
Principal Linkage Editor Variable ............................... 7.2-183 7.2.7 
Linkage Editor Output and Diagnostic Messages ................... 7.2-191 7.2.8 
Recommended Improvements to the Level 2.0 Version ............... 7.2-204 7.2.9 
Linkage Editor Glossary ......................................... 7.2-205 xxiv (8/I/72)

Section 7.3 
TABLE OF CONTErJTS (Continued) 
Page No. 
THE SOURCE ................................................................ 7.3-I 

7.3.1 
Purpose of the Source Conversion Program ......................... 7.3-I 7.3.2 
Conversion Performed ............................................. 7.3-I 7.3.3 
Major Divisions in the Program .................................. 7.3-8 7.3.4 
Use of the SCP ................................................... 7.3-19 7.3.5 
SCP Flowcharts ................................................... 7.3-20 xxv (8/I/72)

Most Recent 
811172 
*i 811172 *ii 811172 *iii BII172 *iv 811172 
*v 8/1/72 
*vi 8/1/72 
*vii 8/1/72 
*viii 811172 *ix 811172 *x 8/I/72 *xi 8/I/72 
*xii 8/I/72 *xiii BII/72 *xiv 8/3/72 *xv 8/1/72 
*xvi 811172 *xvii 8/I/72 *xviii B/1/72 
*xix B/I/72 *xx 811/72 *xxi 8/I/72 *xxii 8/l/72 
*xxiii 8/I/72 *xxiv Bl1172 *xxv B11172 *xxvi 8/I/72 
*xxvii 8/I/72 *xxviii 8/I/72 *xxix 811/72 *XXX 
l.I-I 
l.I-2 
1 .I-3 
1 .I-4 
I.2-I 
l.2-2 8/I/72 
PAGE sTATUS LOG 
Most Recent 
12/1/69 
811172 
811172 
12/I/69 
811172 
1111170 
1111170 
1111/70 
1111170 
8/1/72 
8/1/72 
8/1/72 
1111170 
8/1/72 
8/1/72 
811172 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
_P,__ e ° 
*2.3-28a 
*2.3-29 
-2.3-29a 
**2.3-29b 
*2.3-30 
2.3-31 
2.3-32 
2.3-33 
2.3-34 
2.3-35 
2.3-36 
2.3-37 
2.3-38 
2.3-39 
2.3-40 
,2.3-41 
2.3-42 
2.3-43 
*2.3-44 
2.3-45 
*2.3-46 
**2.3-46a 
2.3-47 
2.3-48 
*2.3-49 
*2.3-49a 
**2.3-49b 
*,2.3-49c 
2.3-50 
2.3-51 
*2.3-52 
2.3-53 
2.3-54 
2.3-55 
2.3-56 
2.3-57 
2.3-58 
2.3-59 
2.3-60 
2.3-61 
Most Recent 
811172 
8/1/72 
811172 
8/1/72 
811172 
1111170 
8/1/72 
811172 
1211169 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
811172 
8/1/72 
8/1/72 
1211169 
*l .2-3 
1.2-4 
1.2-5 
I.2-6 
1.2-7 8/1/72 *I .2-8 811172 *l •2-9 8/l/72 **l .9-9a 
1.2-10 8/I/72 *I .2-11 
l.2-12 ll/I/70 1.2-13 II/1/70 1.2-14 
l.3-I 
I .3-2 
1.3-3 
1.4-I 
I .5-I 
I .5-2 12/I/69 1.6-I 
1.6-2 
1.6-3 
l.6-4 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
811172 
8/1/72 
8/1/72 
8/1/72 
811172 
8/1/72 
8/1/72 
8/1/72 
xxvi (8/1/72) 
f
2.3-62 
2.3-63 
2.3-64 
2.3-65 
2.3-66 
2.3-67 
2.3-68 
2.3-69 
2.3-70 
2.3-71 
2.3-72 
2.3-73 
2.3-74 
2.3-75 
2.3-76 
2.3-77 
2.3-78 
2.3-79 
2.3-80 
3/1/71 

Most Recent 
PAGE STATUS LOG 
Most Recent 
Most Recent 

Page No. 
2.3-81 
2.3-82 
2.3-83 
2.3-84 
2.3-85 
2.3-86 
*2.3-87 
2.3-88 
2.3-89 
2.3-90 
2.3-91 
2.3-92 
2.3-93 
2.3-94 
2.3-95 
2.3-96 
2.3-97 
2.3-98 
*2.3-99 
2.3-I00 
2.3-I01 
2.3-I02 
2.3-I03 
2.3-104 
2.3-I05 
2.3-I06 
2.3-I07 
2.3-I08 
2.3-I09 
2.3-II0 
2.3-II 
2.3-12 
2.3- 13 
2.3- 14 
2.3- 15 
2.3- 16 
2.3- 17 
2.3- 18 
2.3-I19 
2.3-120 
2.3-121 
2.3-122 
2.3-123 
2.3-124 
"2.3-125 "2.3-126 "2.3-127 
2.3-I27a 2.3-128 
2.3-129 
2.3-130 
2.3-131 
2.3-132 
2.3-133 
2.3-134 
2.3-134a 2.3-135 
2.3-136 
2.3-136a 
Date Changed 811172 
811172 
7/I/70 
7/I/70 
12/I/69 
8/I/72 
8/I/72 
8/I/72 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
Page No. 
2.3-137 
2.3-138 
2.3-139 
2.3-140 
2.3-141 
"2.3-142 
2.3-143 
*2.3-I44 *2.3-I45 2.3-146 
2.3-147 
2.3-148 
2.3-149 
*2.3-I50 
2.3-151 
2.3-152 
2.3-153 
2.3-154 
2.3-155 
2.3-156 
2.3-157 
2.3-158 
2.3-159 
2.3-160 
2.3-161 
2.3-162 
2.3-163 
2.3-164 
2.3-165 
2.3-166 
2.3-167 
2.3-168 
2.3-169 
2.3-170 
2.3-171 
2.3-172 
2.3-173 
2.3-I74 
2.3-175 
2.3-176 
2.3-177 
2.3-178 
2.3-179 
2.3-180 
2.3-181 
2.3-182 
2.3-183 
"2.3-184 
2.3-185 
*2.3-I86 "2.3-187 
*2.3-I88 2.3-189 
"2.3-190 
"2.3-191 
*'2.3-191a 2.3-192 
2.3-193 
"2.3-194 
Date Changed 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
6/I/71 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
e_. Pa 
2.4-I 
2.4-2 
2.4-3 
2.4-4 
2.4-5 
2.4-6 
2.4-7 
2.4-8 
2.4-9 
2.4-I0 
2.4-II 
2.4-12 
"2.4-13 
"2.4-13a 2.4-14 
2.4-15 
2.4-16 
2.4-17 
2.4-18 
2.4-19 
2.4-20 
2.4-21 
2.4-22 
2.4-23 
2.4-24 
2.4-25 
2.4-26 
2.4-27 
2.4-28 
2.4-29 
2.4-30 
2.4-31 
2.4-32 
2.4-33 
2.4-34 
2.4-35 
2.4-36 
2.4-37 
2.4-38 
2.4-39 
2.4-40 
2.5-I 
2.5-2 
2.5-3 
2.5-4 
2.5-5 
*2.5-6 
**2.5-6a 2.5-7 
2.5-8 
2.5-9 
2.5-I0 
2.5-II 
2.5-12 
2.5-13 
3.l-I 
3.1-2 
3.1-3 
Date Changed 311171 
8/I/72 
8/I/72 
12/I/69 
12/I/69 
3/I/71 
3/I/71 
3/I/71 
3/I/71 
3/I/71 
311171 
311171 
311171 
311171 
311171 
1211169 
8/I/72 
8/I/72 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 

xxvii (8/I/72)

Most Recent 
PAGE STATUS LOG Most Recent 
Most Recent 

Page No. 
"3.2-I 
*3.2-2 
*3.2-3 
*3.2-4 
*3.2-5 
*3.2-6 
**3.2-7 
3.3-I 
3.3-2 
3.3-3 
3.3-4 
3.3-5 
3,3-6 
3.3-7 
3.3-8 
3.3-9 
3.3-10 
3.3-11 
3.3-12 
3.3-13 
3.3-14 
"3.3-15 
"3.3-15a 
3.3-16 
"3.3-17 
*'3.3-18 
*'3.3-19 
**3.3-20 
3.4-I 
3.4-2 
3.4-3 
3.4-4 
3.4-5 
3.4-6 
3.4-7 
3.4-8 
3.4-9 
3.4-10 
3.4-11 
3.4-12 
3.4-13 
3.4-14 
3.4-15 
3.4-16 
3.4-17 
"3.4-18 
3.4-19 
3.4-20 
3.4-21 
3.4-22 
3.4-23 
*3.4-24 
3.4-25 
3.4-26 
3.4-27 
*3.4-28 
3.4-29 
3.4-30 
3.4-31 
3.4-32 
Date Changed 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
12/I/69 
8/I/72 
8/I/72 
8/I/72 
Pase No 
3.4-33 
3.4-34 
3.4-35 
*3.4-36 
3.4-37 
3.4-38 
3.4-39 
3.4-4O 
3.4-41 
3.4-42 
3.4-43 
3.4-44 
3.4-45 
3.4-46 
3.4-47 
3.4-48 
3.4- 49 
3.4-50 
3.4-51 
3.4-52 
3.4-53 
3.4-54 
3.4-55 
3.4-56 
3.4-57 
3.4-58 
3.4-59 
3.4-60 
3.4-61 
3.4-62 
3.4-63 
3.4-63a 
*3.4-64 
*3.4-65 
3.4-66 
3.4-67 
3.4-68 
3.4-69 
3.4-70 
3.4-71 
3.4-72 
3.4-72a 
3.4-73 
3.4-73a 
3.4-74 
3.4-74a 
3.4-75 
3.4-75a 
3.4-76 
3.4-77 
3.4-78 
3.4-78a 
3.4-79 
3.4-80 
3.4-81 
3.4-82 
3.4-83 
3.4-84 
3.4-85 
3.4-86 
Date Chansed 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
7/I/70 
7/I/70 
12/I/69 
12/I/69 
8/I/72 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
xxviii
Date Chan_ed 3/I/71 
8/I/72 
12/I/69 
12/I/69 
3/I/71 
12/I/69 
12/I/69 
3/I/71 
3/I/71 
3/I/71 
3/I/71 
3/I/71 
3/I/71 
3/I/71 
3/I/71 
8/I/72 
8/I/72 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
Page No. 
3.4-87 
3.4-87a 
3.4-88 
3 ._-89 
3.4-90 
3.4-91 
3.4-92 
3.4-93 
3.4-94 
3.4-95 
3.4-96 
3.4-97 
3.4-98 
3.4-99 
3.4-100 
3.4-101 
3.4-102 
3.4-103 
3.4-104 
3.4-105 
3.4-106 
3.4-107 
3.4-108 
3.4-109 
3.4-110 
3.4-111 
"3.4-112 
3.4-113 
3.4-114 
3.4-115 
3.4-116 
3.4-117 
*'3.4-118 
*'3.4-119 
**3.4-120 
*'3.4-121 
*'3.4-122 
*'3.4-123 
*'3.4-124 
*'3.4-125 
*'3.4-126 
*'3.4-127 
*'3.4-128 
*'3.4-129 
**3.4-I 30 "3.5-I 
3.5-2 
3.5-3 
*3.5-4 
3.5-5 
3.5-6 
*3.5-7 
*3.5-8 
*3.5-9 
3.5-10 
3.5-11 
3.5-12 
3.5-13 
3.5-14 
3.5-15 

Most Recent 
PAGE STATUS LOG Most Recent 
Most 
Recent 

e_. Pa 
3.5-16 3.5-17 3.5-18 3.5-19 3.5-20 3.5-21 
Date Changed 6/I/71 
Page No. 
3.5-73 3.5-74 3.5-75 3.5-76 3.5-77 3.5-78 
Date Changed 12/I/69 
6/I/71 
Page No. 
4.4-6 
4.4-7 
4.4-8 
4.4-9 
4.4-10 
4.4-11 
Date 
Changed 

3.5-22 
*3.5-23 
3.5-24 
3.5-25 
*3.5- 26 *3.5-27 
*3.5-28 
**3.5-28a 3.5-29 
3.5-30 
3.5-31 
3.5-32 
3.5-33 
3.5-34 
3.5-35 
3.5-36 
3.5-37 
3.5-38 
3.5-39 
3.5-40 
3.5-41 
3.5-42 
*3.5-43 
*3.5-44 
3.5-45 
3.5-46 
3.5-47 
3.5-48 
3.5-49 
3.5-50 
3.5-51 
3.5-52 
3.5-53 
3.5-54 
3.5-55 
3.5-56 
3.5-57 
3.5-58 
3.5-59 
3.5-60 
3.5-61 
3.5-62 
*3.5-63 
3.5-64 
*3,5-65 
**3.5-65a 3.5-66 
3.5-67 
3.5-68 
3.5-69 
3.5-70 
3.5-71 
3.5-72 
8/I/72 
8/I/72 8/I/72 8/I/72 8/I/72 
8/I/72 8/I/72 
3/I/71 
12/I/69 
8/I/72 
8/I/72 8/I/72 
3.5-79 
**3.5-80 **3.5-81 
**3.5-82 
**3.5-83 
**3.5- 84 **3.5-85 
*4. I-I 
4.1-2 
4.1-3 
4.1-4 
4.1-5 
4.1-6 
*4. I-7 
**4.1-7a 
*4.1-8 
*4. I-9 
"4.1-10 
*4.1 -I1 "4.1-12 
"4.1-13 
"4.1-14 
"4.1-15 
*4.1-16 
"4.1-17 
*4. I-I8 *4.1-19 
*4.1-20 
*4.1-21 
**4.1-22 
**4.1-23 
4.2-I 
*4.2-2 
4.2-3 
4.2-4 
4.2-5 
4.2-6 
4.3-I 
4.3-2 
4.3-3 
4.3-4 
4.3-5 
4.3-6 
4.3-7 
4.3-8 
4.3-9 
4.3-10 
"4.3-11 
"4.3-12 
4.4-I 
4.4-2 
4.4-3 
4.4-4 
4.4-5 
6/I/71 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
3/I/70 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
811/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
3/I/71 
8/I/72 
8/I/72 
xxix (8/I/72)
"4.5-I 
*4.5-2 
4.5-3 
4.5-4 
*4.5-5 
*4.5-6 
*4.5-7 
*4.5-8 
*4.5-9 
"4.5-10 
*4.5-I1 "4.5-12 
"4.5-13 
**4.5-13a "4.5-14 
"4.5-15 
"4.5-16 
"4.5-17 
"4.5-18 
"4.5-19 
**4.5- 20 4.6-I 
4.6-2 
4.6-3 
4.6-4 
4.6-5 
4.6-6 
4.6-7 
4.6-8 
4.6-9 
4.6-10 
4.6-11 
4.6-12 
4.6-13 
4.6-14 
4.6-15 
4.7-I 
4.7-2 
4.7-3 
4.7-4 
4.7-5 
*4.7-6 
**4.7-6a 
4.7-7 
4.7-8 
4.7-9 
4.7-10 
4.8-I 
4.8-2 
4.9-I 
*4.9-2 
4.9-3 
4.9 -4 
8/I/72 8/I/72 
8/I/72 8/I/72 8/I/72 8/I/72 8/I/72 8/I/72 8/I/72 8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
Page No. 
Most Recent Date Changed 
e_. Pa 
PAGESTATUS LOG 
Most Recent 
Date Changed 
Page No. 
Most Recent Date Changed 
4.9-5 
4.9-6 
4.9-7 
4.9-8 
4.9-9 
4.9-10 4.10-I 
4.10-2 4.10-3 4.10-4 4,11-I 
4.11-2 4.11-3 4.12-I 
4.13-I 
4.13-2 4.14-I 
4.14-2 4.15-I 
4.16-I 
4.16-2 4,16-3 4.16-4 4.17-I 
4.17-2 4.17-3 4.17-4 4.17-5 4.17-6 4.18-I 
4.19-I 
4.19-2 4.20-I 
4.21 -I 4.21-2 4.21-3 4.21-4 4.21-5 4.21-6 
"4.21-7 4.21-8 4.21-9 4.22-I 
4.22-2 *4.22-3 4.23-I 
4.23-2 *4.23-3 *4.23-4 *4.23-5 4.24-I 
4.24-2 4.24-3 4.24-4 4.24-5 4.24-6 4.24-7 4.24-8 4.24-9 
8/I/72 
11/I/70 
8/]/72 
1211169 811/72 
811/72 
811/72 
12/I/69 
12/I/69 3/I/71 3/I/71 
4.24-10 
4.24-I 1 4.24-12 
*4.24-I 2a 4.24-13 
"4.24-14 
4.24-15 
4.24-16 
4,24-17 
4.24-18 
4.25-I 
4.25-2 
4.25-3 
4.25-4 
4.25-5 
4.25-6 
4.25-7 
4.25-8 
4.25-8a 
4.25-9 
4.25-10 
4.26-I 
4.26-2 
4.26-3 
4.26 -4 
4.26-5 
4.26 -6 
4.26-7 
4.26-8 
4.26-9 
4.26-10 
4.26-I 1 4.26-12 
4.26-13 
4.26-14 
*4.26-15 
4.26-16 
4.26-17 
4.26-18 
4.27-I 
4.27-2 
4.27-3 
4.27-4 
4.27-5 
*4.27-6 
4.27-7 
*4.27-8 
4.27-9 
4.27-10 
4.27-11 
4.27-12 
"4.27-13 
4.27-14 
4.27-15 
4.27-16 
4.27-17 
4.27-18 
4.27-19 
4.27-20 
3/I/71 3/I/71 3/I/71 8/I/72 
8/I/72 12/I/69 12/I/69 
9/I/70 
9/I/70 
1111170 911170 
1111170 1111170 
811172 
811172 311171 811172 
811172 
"4.27-21 
**4.27-21a **4.27-21 b *4.27-22 
4.27-23 
4.27-24 
4.27-25 
*4.27-26 
*4.27-27 
4.28-I 
4.28-2 
4.28-3 
4.28-3a 
4.28-4 
4.28-5 
4,28-6 
4.28-7 
4.28-8 
"4.28-8a 
"4.28-8b 
4.28-9 
"4.29-I 
*4.29- 2 
*4.29- 3 
*4.29-4 
*4.29 -5 
4.29-6 
4.29 -7 
4.30-I 
4.30-2 
4.30-3 
4.30 -4 
4.30-5 
4.30-6 
4.30-7 
4.30-8 
"4.31 -I 
*4.31-2 
*4.31-3 
"4.31-4 
*4.31-5 
**4.31-6 
4.32-I 
4.32-2 
4.32-3 
4.32-4 
4.33-I 
4.33-2 
4.33-3 
4.34-I 
4.34-2 
4.35-I 
4,35-2 
4.35-3 
*4.36-I 
*4.36-2 
*4.36-3 
4.37-I 
4.37-2 
811172 811/72 8/I/72 811172 
711170 811172 811/72 311171 311171 311171 311171 
1211169 8/I r72 8/I 172 7/I 170 8/I r72 8/I r72 8/I _72 8/I 172 8/I 172 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/I/72 
8/I/72 
8/I/72 

xxx (8/I/72)

Most Recent 
PAGESTATUSLOG Most Recent 
Most Recent 

Page No_. 
4.38-I 
4.38-2 
"4.39-I 
4.39 -2 
4.40-I 
4.40-2 
4.41 -I 
4.41-2 
4.41-3 
"4.41-4 
4.41-5 
4.41-6 
"4.41-7 
4.41-8 
4.41-9 
4.41-lO 
4.41-ll 
*4.41-12 
"4.41-13 
**4.41-l3a 4.41-14 
4.41-15 
4.41-16 
4,41-17 
4.41-18 
4.41-19 
4.41-20 
4.41-21 
4.41-22 
4.41-23 
4.41-24 
4.41-25 
4.41-26 
4.41 -27 
"4.41-28 
*'4.41-28a **4.41-28b **4.41-28c *4.41-29 
4.41-30 
4.42-I 
4.42-2 
4.42-3 
4.42-4 
4.43-1 
4.43-2 
4.43-3 
4.44-1 
4.44-2 
4.45-I 
4.45-2 
4.45-3 
4.45 -4 
4.45-5 
4.45-6 
4.46-I 
4.46-2 
4.46-3 
4.46-4 
4.46-5 
Date Changed 8/I/72 
8/I/72 
8/I/72 
12/I/69 
7/I/70 
911/70 
8/I/72 
8/I/72 
8/I/72 
7/1/70 
3/1/71 
3/1/71 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
8/1/72 
7/1/70 
3/1/71 
Page No. 
4.46-6 
4.46-7 
4.46-8 
4.46-9 
4.46-10 
4.46-I1 
4.46-12 
4.46-13 
4.46-14 
4.46-15 
4.46-16 
4.46-17 
4.46-18 
*4.46-19 
*'4.46-19a **4.46-I9b *4.46-20 
4.47-I 
4.47-2 
4.47-3 
4.47-4 
4.47-5 
4.47-6 
4.47-7 
4.47-8 
*4.48-I 
*4.48-2 
4.48-3 
4.48-4 
*4.48-5 
4.48-6 
4.48-7 
4.48-8 
4.48-9 
4.48-I0 
4.48-II 
*4.48-12 
4.48-13 
4.48-14 
4.48-15 
4.48-16 
4.48-17 
4.48-18 
4.48-19 
4.48-19a 
4.48-19b 
4.48-19c 
4.48-19d 
4.48-19e 
4.48-19f 
4.48-19g 
4.48-20 
4.48-21 
4.48-22 
4.48-23 
4.48-24 
4.48-25 
*4.48-26 
4.48-27 
Date Changed 
811172 
811172 
8/I/72 
811172 
1211/69 
811172 
811/72 
12/I/69 
8/I/72 
3/I/71 
7/I/70 
8/I/72 
12/I/69 
12/I/69 
12/I/69 
1211/69 
12/I/69 
1211169 
12/I/69 
3/I/71 
12/I/69 
8/I/72 
e_. PB 
4.49-I 
4.49-2 
"4.49-3 
4.49-4 
4.49-5 
*4.49-6 
*4.49-7 
**4.49-7a 4.49-8 
4.49-9 
4.50-I 
4.50-2 
4.51-I 
4.51-2 
4.51-3 
4.51-4 
"4.52-I 
*4.52-2 
*4.52-3 
*4.52-4 
4.53-I 
4.53-2 
4.54-I 
*4.54-2 
4.54-3 
4.54-4 
4.54-5 
4.54-6 
4.54-7 
4.54-8 
4.55-I 
4.55-2 
4.55-3 
4.55-4 
4.55-5 
4.55-6 
4.55-7 
4.55-8 
4.55-9 
4.56-I 
4.56-2 
4.56-3 
4.57-I 
4.57-2 
4.57-3 
4.57-4 
4.58-I 
4.58-2 
4.58-3 
4.58-4 
4.58-5 
4.58-6 
4.58-7 
4.59-I 
*4.59-2 
4.59-3 
4.59-4 
4.59-5 
4.59-6 
Date Changed 
12/I169 
811172 
1211169 
811172 
811172 
811172 
711170 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
3/I/71 
8/I/72 

xxxi (811172)

Most Recent 
PAGE STATUS LOG Most Recent 
Most Recent 

a_ag_e P No. 
4.59-7 
4.59-8 
4.59-9 
4.59-10 
*4.59-I 1 4.59-12 
4.59-13 
"4.59-14 
*'4.59-15 
4.60-I 
4.60-2 
4,60-3 
4.60-4 
4.60-5 
4.60-6 
4.60-7 
*4.61 -I 
"4.61-2 
*4.61 -3 
**4.61 - 3a 4.61-4 
"4.61-5 
4.61-6 
4.61-7 
4.61-8 
4.62-I 
4.62-2 
4.62-3 
4.62-4 
4.62-5 
4.62-6 
4.62-7 
4.62-8 
*4.62-9 
4.63-I 
4.63-2 
4.63-3 
4.63-4 
4.63-5 
4.63-6 
4.63-7 
4.63-8 
4,64-I 
4.64-2 
4.64-3 
4.64-4 
4.64-5 
*4.64-6 
*4.64-7 
4.64-8 
4.64-9 
4.64-10 
4.65-I 
4.65-2 
4.65-3 
4.65-4 
4.65-5 
4.65-6 
4,65-7 
*4.65-8 
Date Changed 
12/I/69 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
6/I/71 
6/I/71 
6/I/71 
8/I/72 
8/I/72 
8/I/72 
Page No. 
4.65-9 
4.65-10 
"4.65-11 
4.65-12 
4.65-13 
4.65-14 
4.65-15 
4.65-16 
4.65-17 
"4.65-18 
"4.65-19 
4.65-20 
4.65-21 
4.65-22 
4.66-I 
4.66-2 
4.66-3 
4.66-4 
4.66-5 
4.67-I 
4.68-I 
4.68-2 
4.68-3 
4.68-4 
4.68-5 
4.69-I 
4.69-2 
4.69-3 
4.69-4 
4.70-I 
4,70-2 
4.70-3 
4.70-4 
4.70-5 
4.70-6 
4.70-7 
4.71-I 
4.72-I 
4.72-2 
4.72-3 
4.73-I 
4.73-2 
4.73-3 
4.73-4 
4.74-I 
4.74-2 
4 74-3 
*z .74-4 
**z. 74-4a 4 74-5 
4 75-I 
4 76-I 
4 76-2 
4 76-3 
4 77-I 
4 77-2 
4 77-3 
*z .78-I 
*z .78-2 
.79-I 
Date Changed 
1211169 
12/I/69 
8/I172 
711170 
711170 
7/I170 
3/I171 
8/I/72 
8/I/72 
7/I/70 
7/I/70 
7/I/70 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
8/I/72 
8/I/72 
12/I/69 
8/I/72 
8/I/72 
xxxii (8/I/72)
Page No. 
4.79-2 
4.79-3 
4.80-I 
4.80-2 
4.81 -I 
4.81-2 
4.82-I 
4.82-2 
"4.83-I 
4.83-2 
*4.83-3 
**4.83-4 
"4.84-I 
*4.84-2 
4,85-I 
4.86-I 
4.86-2 
"4.87-I 
*4.87-2 
*4.87-3 
*4.87-4 
*4.87-5 
*4.87-6 
4.87-7 
4.87-8 
4.87-9 
4.87-10 
4.87-11 
4.87-12 
"4.87-13 
4.87-14 
4.87-15 
4.87-16 
4.87-16a 
*'4.87-16b 
4.87-17 
4.87-18 
4.87-19 
4.87-20 
4.87-21 
4.87-22 
4.87-23 
4.87-24 
4.87-25 
4.87-25a 
*4.87-26 
4.87-27 
4.87-28 
4.87-28a 
4.87-29 
4.87-30 
4.87-31 
4.87-32 
4.87-33 
4.87-34 
4.87-35 
4.87-36 
*4.87-37 
3.87-38 
4.87-39 
Date Changed 
811/72 
311/71 
811172 
811172 
8/I172 
811/72 
811172 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
12/I/69 
11/I/70 
3/I/71 
3/I/71 
8/I/72 
3/I/71 
12/I/69 
8/I/72 
3/I/71 
3/I/71 
9/I/70 
9/I/70 
8/I/72 
911170 
11/1/70 
9/I/70 
3/I/71 
3/I/71 
8/I/72 

Most Recent Date Changed 
PAGE STATUS LOG 
Most Recent 
Most Recent 
4.87-119 12/I/69 

4.87-40 
4.87-41 
4.87-42 
4.87-43 
4.87-44 
4.87-45 
4.87-46 
4.87-47 
4.87-48 
4.87-49 
4.87-50 
4.87-51 
4.87-52 
4.87-53 
4.87-54 
4.87-55 
4.87-56 
4.87-57 
4.87-58 
4.87-59 
4.87-60 
4.87-61 
4.87-62 
*4.87-63 
*4.87-64 
4.87-65 
*4.87-66 
**4.87-66a *4.87-67 
4.87-6 8 
4.87-69 
4.87-70 
4.87 -71 
4.87-72 
4.87-73 
4.87-74 
4.87-75 
4.87-76 
4.87-76a 
4.87-76b 
4.87-76c 
*4.87-76d 
**4.87-76e 4.87-77 
4.87-78 
4.87-79 
4.87-80 
4.87-81 
4.87-82 
*4.87-83 
4.87-84 
4.87-85 
4.87-86 
4.87-86a 
4.87-87 
4.87-88 
4.87-89 
4.87-90 
4.87-91 
311171 
3/1/71 
3/1/71 
811/72 
8/I/72 
II11170 
811172 
811172 
811172 
12/]/69 
12/I/69 
12/I/69 
8/1/72 
811/72 
8/I/72 
9/I/70 
9/I/70 
9/1/70 
*4.87-92 8/I/72 4.87-120 
4.87-93 4.87-I21 
4.87-94 4.87-I22 
4.87-95 12/1/69 *4.87-96 8/I/72 4.87-123 
4.87-97 9/I/70 -4.87-124 8/I/72 4.87-97a 9/I/70 ,4.87-125 8/1/72 *4.87-98 8/I/72 ,4.87-126 8/I/72 **4.87-126a 8/I172 4.87-99 4.87-127 
4.87-I00 4.87-127a 12/I/69 4.87-I01 4.87-127b 12/I/69 4.87-102 12/I/69 4.87-I03 ll/I/70 4.87-127c 
4.87-I04 ll/I/70 4.87-127d 12/I/69 4.87-I04a 12/I169 4.87-127e 12/I/69 4.87-104b 12/I/69 4.87-127f 12/I/69 4.87-104c 12/I/69 4.87-128 
4.87-104d 12/I/69 4.87-129 
4.87-104e 12/I/69 4.87-130 
4.87-104f 12/I/69 4.87-131 
4.87-I04g 12/I/69 a.87-132 
4.87-I04h 1211/69 4.87-133 
4.87-I04i 12/I/69 4.87-134 
4.87-I04j 12/I/69 4.87-135 
4.87-I04k 12/I/69 -4.87-136 8/I/72 4.87-I04_ 12/I/69 4.87-137 
4.87-I04m 12/I/69 4.87-138 
4.87-I04n 11/I/70 *-4.87-138a 8/I/72 4.87-104o 1111/70 4.87-139 
,4.87-105 8/I/72 4.87-140 3/I/71 4.87-141 3/I/71 4.87-106 4.87-142 3/I/71 4.87-107 3/I/71 4.87-108 9/I/70 4.87-143 
,4.87-109 8/1172 4.87-144 
,4.87-I09a 8/I/72 4.87-145 
4.87-I09b 12/I/69 4.87-146 
4.87-I09c 12/I/69 4.87-147 
.4.87-I09d 8/I/72 4.87-148 
*-4.87-I09e 8/I/72 4.87-149 
*-4.87-I09f 8/I/72 4.87-150 
*-4.87-I09g 8/I/72 -4.87-151 8/I/72 4.87-152 *,4.87-I09h 811/72 4.87-153 
*'4.87-I09i 811/72 
*'4.87-I09j 8/I/72 4.87-154 4.87-155 
*-4.87-I09k 8/I/72 4.87-156 
*-4.87-I09_ 8/I/72 
*-4.87-I09m 8/I/72 4.87-157 
**4.87-I09n 8/I/72 4.87-158 4.87-159 
.-4.87-109o 8/I/72 4.87-160 
.,4.87-I09p 8/I/72 4.87-161 
4.87-110 
-4.87-111 8/I/72 4.87-162 4.87-163 
4.87-112 4.87-164 
4.87-11 3 4.87-165 
4.87-114 4.87-166 
4.87-115 4.87-167 
4.87-116 4.87-168 
4.87-117 
,4.87-118 8/I/72 4.87-169 
xxxiii (8/I/72)

Most Recent 
PAGE STATUS LOG Most Recent 
Most Recent 

Page No. 
4.87-170 4.87-171 
Date Changed 
Page No. 
4.89-10 
4.89-I1 
Date Changed 
1111170 
1111170 
Page No. 
*5 3-8 
*5 3-9 
Date Chan_ed 
811172 
811172 
4.87-172 
4.87-173 
4.87-174 
4.87-175 
4.87-176 
4.87-177 
4.87-178 
4.87-I 79 4.87-180 
4.89-12 4.89-13 4.89-14 4.89-15 4.89-16 4.89-17 "4.90-I 
*4.90-2 *4.90-3 
1111170 1111170 1111170 11/I/70 1111170 1111170 811r72 
8/Ir72 8/I172 
*5 
*5 
*5 
*5 
**5 **5 **5 *'5 
**5 
3-10 3-11 3-12 3-13 3-14 3-15 3-16 3-17 3-18 
811172 8/1172 8/1172 8/1172 811172 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
4.87-181 4.87-182 "4.87-183 4.87-184 4.87-185 4.87-186 4.87-187 4,87-188 "4.87-189 
*'4.87-190 *'4.87-191 *'4.87-192 *'4.87-193 *'4.87-194 *'4.87-195 *'4.87-196 *'4.87-197 *'4.87-198 *'4.87-199 **4.87-200 *'4.87-201 **4.87-202 **4.87-203 **4.87-204 **4.87-205 **4.87-206 **4.87-207 **4.87-208 **4,87-209 *'4.87-210 4.88-I 
4.88-2 
4.88-3 
4.88-4 
4.88-5 
4.88-6 
4.88-7 
4.88-8 
4.88-9 
4.88-10 
4.89-I 
4.89-2 
4.89-3 
4.89-4 
4.89-5 
4.89-6 
4.89-7 
4.89-8 
4.89-9 
811172 
11/I170 
11/I170 
11/I/70 
11/I/70 
11/I/70 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
1111170 1111170 1111170 1111170 11/1170 1111170 11/I170 1111170 1I11170 
*4.90-4 *4.90-5 *4.90-6 *4.90-7 
**4.90-8 "4.91-I 
"4.91-2 *'4.91-3 *'4.91-4 *'4.91-5 *'4.91-6 *'4.91-7 "4.92-I 
*4.92-2 *'4.93-I **4.93-2 *'4.94-I **4.94-2 *'4.95-I **4.95-2 *'4.96-I **4.96-2 *'4.97-I **4.97-2 *'4.98-I **4.98-2 **4.98-3 *'4.99-I **4.99-2 **4.99-3 *'4.100-I *'4.100-2 *'4.100-3 *'4.101-I *'4.101-2 *'4.101-3 *'4.102-I *'4.102-2 *'4.103-I *'4.103-2 5.1-I 
"5.2-I 
"5.3-I 
*5,3-2 
*5.3-3 
*5.3-4 
*5.3-5 
*5.3-6 
*5.3-7 
811172 
811172 
811r72 
811172 
811172 
811172 
811172 
811r72 
811172 
811t72 
811172 
8/1172 
8/1172 
8/I172 
8/I172 
8/I172 
8/I172 
8/IZ72 
8/I172 
8/I172 
8/I172 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
12/I/69 
DELETED 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
xxxiv (8/I/72)
**5 3-19 **5 3-20 *'5.3-21 
**5.3-22 
**5.3-23 
**5.3-24 
**5.3-25 
**5.3-26 
**5.3-27 
**5.3-28 
**5.3-29 
**5.3-30 
*'5.3-31 
**5.3-32 
**5.3-33 
**5.3-34 
**5.3-35 
**5.3-36 
**5.3-37 
**5.3-38 
**5.3-39 
**5.3-40 
*'5.3-41 
**5.3-42 
**5.3-43 
**5.3-44 
**5.3-45 
**5.3-46 
**5.3-47 
**5.3-48 
**5.3-49 
**5,3-50 
**5 3-51 **5 3-52 **5 3-53 **5 3-54 *5 4-I 
*5 4-2 
*5 4-3 
*5.4-4 
*5.4-5 
*5,4-6 
*5.4-7 
*5.4-8 
*5.4-9 
"5,4-10 
"5.4-11 
"5.4-12 
"5.4-13 
8/I/72 
8/I/72 
8/It72 
8/Ir72 
8/I_72 
8/1172 
8/1172 
8/I 172 8/I 172 8/1172 
8/1172 
8/I172 
8/I172 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 

Most Recent 
PAGE STATUS LOG Most Recent 
Most Recent 
Page No. 
"5.4-14 
"5.4-15 
"5.4-16 
"5.4-17 
"5.4-18 
"5.4-19 
*5.4-20 
"5.4-21 
*5.4-22 
*5.4-23 
*5.4-24 
*5.4-25 
*5.4-26 
*5.4-27 
*5.4-28 
*5.4-29 
*5.4- 30 
*5.4-31 
*5.4-32 
*5.4-33 
*5.4-34 
*5.4-35 
*5.4-36 
*5,4-37 
*5.4-38 
*5.4-39 
**5.4-40 
*'5.4-41 
**5.4-42 
**5'.4-43 
*'5.4-44 
**5.4-45 
**5.4-46 
**5.4-47 
**5.4-48 
**5.4-49 
**5.4-50 
*'5.4-51 
**5.4-52 
**5.4-53 
**5.4-54 
**5.4-55 
**5.4-56 
**5.4-57 
**5.4-58 
**5.4-59 
**5.4-60 
*'5.4-61 
**5.4-62 
**5.4-63 
**5.4-64 
**5.4-65 
**5.4-66 
**5.4-67 
**5.4-68 
**5.4-69 
**5.4-70 
*'5.4-71 
**5.4-72 
**5.4-73 
Date Changed 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
Page No. 
**5.4-74 
**5.4- 75 **5.4-76 
**5.4-77 
"5.5-I 
*5.5-2 
*5.5-3 
5.5-4 
5.5-5 
*5.5-6 
*5.5-7 
*5.5-8 
*5.5-9 
"5.5-10 
"5.5-11 
"5.5-12 
"5.5-13 
*'5.5-14 
*'5.5-15 
**5.5-16 
*'5.5-17 
*'5.5-18 
*'5.5-19 
**5.5-20 
**5.5-21 
_'5.5-22 
**5.5-23 
**5.5-24 
**5.5-25 
**5.5-26 
**5.5-27 
**5.5-28 
**5.5-29 
**5.5-30 
*'5.5-31 
** 5.5- 32 **5.5-33 
**5.5-34 
**5.5- 35 **5.5- 36 **5.5-37 
**5.5- 38 **5.5-39 
**5.5-40 
*.5.5-41 **5.5-42 **5.5-43 **5.5-44 **5.5-45 **5.5-46 
**5.5-47 
**5.5-48 
5.6-I 
5.6-2 
5.6-3 
5.6-4 
5.6-5 
5.6-6 
5.6-7 
5.6-8 
Date Changed 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
12/I/69 
12/I/69 
8/I _72 
8/Ir72 
8/Iq2 
8/1172 
8/I 172 
8/I 172 
8/I172 
8/1172 
8/Ir72 
8/Ir72 
8/Ir72 
8/1172 
8/I/72 
8/I172 
8/1172 
8/1172 
8/Iq2 
8/1172 
8/Ir72 
8/Ir72 
8/1172 
8/Ir72 
8/Ir72 
8/Ir72 
8/I 172 
8/Ir72 
8/I/72 
8/1172 
8/I'72 
8/I 172 
8/Ir72 
8/Ir72 
8/1172 
8/I_72 
8/1172 
8/1172 
8/1172 
8/Ir72 
8/Iq2 
8/Ir72 
8/Iq2 
8/I_72 
8/I172 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
Page No. 
5.6-9 
5.6-10 
5.6-11 
5.6-12 
5.6-13 
5.6-14 
"5.6-15 
"5.6-16 
5;6-17 
5.6-18 
5.6-19 
5.6-20 
5.6-21 
5.6-22 
*5.6-23 
*5.6-24 
*5.6-25 
*5.6-26 
*5.6-27 
*'5.6-27a 
*5.6-28 
5.6-29 
"5.6-30 
*'5.6-30a 
5.6-31 
6 I-I 
*6 2-I 
*6 2-2 
*6 2-3 
*6 3-I 
*6 3-2 
**6 3-3 6 4-I 
6.5-1 
6.5-2 
*6.6-I 
6.6-2 
6.7-I 
6.7-2 
"6.8-I 
*6.8-2 
*6.8-3 
*6.8-4 
*6 8-5 
*6 8-6 
*6 8-7 
*6 8-8 
*6 8-9 
*6 8-10 
"6.8-11 
*6 8-12 
*6 8-13 
*6 8-14 
*6 8-15 
*6 8-16 
*6 8-17 
*6 8-18 
*6 8-19 
*6 8-20 
*6 8-21 
Date Changed 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
8/I/72 
8/I/72 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
12/I/69 
8/I/72 
8/I/72 
12/I/69 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
311171 
311171 
811172 
811172 
811172 
811/72 
811172 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/1/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
xxxv (8/I/72)
Most Recent 
PAGE STATUS LOG Most Recent 
Most Recent 
Page No. 
*6.8-22 
*6.8-23 
*6.8-24 
*6.8-25 
*6.8-26 
*6.8-27 
*6.8-28 
*6.8-29 
*6.8- 30 "6.8-31 
*6.8-32 
*6.8- 33 *6.8- 34 *6.8-35 
*6.8-36 
*6.8- 37 *6.8- 38 *6.8- 39 *6.8-40 
"6.8-41 
*6.8- 42 *6.8-43 
*6.8- 44 *6.8-45 
*6.8- 46 *6.8-47 
*6.8-48 
*6.8-49 
*6.8- 50 *6.8-51 
*6.8-52 
*6.8-53 
*6.8-54 
*6.8-55 
6.9-I 
6.9-2 6 I0-I 
6 10-2 
6 10-3 
6 10-4 6 10-5 
6 10-6 6 10-7 
6.10-8 
6.10-9 
6.10-10 
6.10-11 
6.10-12 
6.10-13 
6.10-14 
6.10-15 
"6.10-16 
6.10-17 
6.10-18 
6.11-I 
6.11-2 
6.11-3 
6.11-4 
Date Changed 
811172 
811172 
811172 
811172 
811172 
811172 
811172 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
12/I/69 
12/I/69 
12/I/69 
3/I/70 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
12/I/69 
8/I/72 
12/I/69 
12/I/69 
Page No. 
*'6.12-I 
**6.12-2 
**6.12-3 
**6.12-4 
**6.12-5 
**6.12-6 
**6.12-7 
**6.12-8 **6.12-9 
*'6.12-10 
*'6.12-11 
*'6.12-12 
*'6.12-13 
**6.12-14 
**6.12-15 
*'6.12-16 
*'6.12-17 
*'6.12-18 
7.1-I 
7.1-2 
7.2-I 
7.2-2 
7.2-3 
7.2-4 
7.2-4a 
7.2-5 
7.2-6 
7.2-7 
7.2-8 
7 2-9 7 2-9a 
7 2-10 
7 2-11 7 2-12 
7 2-12a 
7 2-I 2b 7 2-13 
7.2-14 
7.2-14a 
7.2-15 
7.2-16 
7.2-17 
7.2-18 
7.2-19 
7.2-20 
7.2-21 
7.2-22 
7.2-23 
7.2-24 
7.2-25 
7.2-26 
7.2-27 
7.2-28 
7.2-28a 
7.2-29 
7.2-30 
7.2-31 
7.2-32 
Date Changed 
811172 
811172 
811172 
8/I 172 
8/It72 
8/Ir72 
8/Ir72 
8/I172 
8/I172 
8/I172 
8/I172 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
8/I/72 
3/I/71 
3/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
No. 
7.2-33 
7.2-34 
7.2-35 
7.2-36 
7.2-37 
7.2-38 
7,2-39 
7.2-40 
7.2-41 
7.2-42 
7.2-43 
7.2-44 
7.2-45 
7.2-46 
7.2-47 
7.2-48 
7.2-49 
7.2-50 
7.2-51 
7.2-52 
7.2-53 
7.2-54 
7.2-55 
7.2-56 
7.2-57 
7.2-58 
7.2-59 
7.2-60 
7.2-61 
7.2-62 
7.2-63 
7.2-64 
7.2-65 
7.2-66 
7.2-67 
7.2-68 
7.2-69 
7.2-70 
7.2-71 
7.2-72 
7.2-73 
7.2-74 
7.2-75 
7.2-76 
7.2-77 
7.2-78 
7.2-79 
7.2-80 7 2-81 
7 2-82 7 2-83 
7 2-84 
7 2-85 7 2-86 
7 2-87 
7.2-88 
7.2-89 
7.2-90 
Date Changed 
6/I/71 
6/1171 
611/71 
611171 
611/71 
6/I/71 
611171 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
xxxvi (8/I/72)

Page No. 
7.2-91 
7.2-92 
7.2-93 
7.2-94 
7.2-95 
7.2-96 
7.2-97 
7.2-98 
7.2-99 
7.2-I00 7.2-I01 7.2-102 7.2-I03 7.2-I04 7.2-I05 7.2-I06 7.2-I07 7.2-I08 7.2-109 7.2-II0 7.2-III 7.2-I12 7.2-I13 7.2-I14 7.2-I15 7.2-I16 7.2-I17 7.2-I18 7.2-I19 7.2-120 7.2-121 7.2-122 7.2-123 7.2-124 7.2-125 7.2-126 7.2-127 7.2-128 7.2-129 7.2-I30 7.2-131 7.2-132 7.2-133 7.2-134 7.2-135 7.2-136 7.2-137 7.2-138 7.2-139 7.2-140 7.2-141 7.2-142 7.2-143 7.2-144 7.2-145 7.2-146 7.2-147 7.2-148 7.2-149 
Most Recent Date Changed 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
611171 
611171 
611171 
611171 
611171 
611171 
611171 
611171 
611171 
611171 
611171 
611171 
611171 
6/1171 
611171 
611171 
6/I171 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
PAGE STATUS LOG 
Page No. 
7.2-150 
7.2-151 
7.2-152 
7.2-153 
7.2-154 
7.2-155 
7.2-156 
7.2-157 
7.2-158 
7.2-159 
7.2-160 
7.2-161 
7.2-162 
7.2-163 
7.2-164 
7.2-165 
7.2-166 
7.2-167 
7.2-168 
7.2-169 
7.2-170 
7.2-171 
7.2-172 
7.2-173 
7.2-174 
7.2-175 
7.2-176 
7.2-177 
7.2-178 
7.2-179 
7.2-180 
7.2-181 
7.2-182 
7.2-183 
7.2-184 
7.2-185 
7.2-186 
7.2-187 
7.2-188 
7.2-189 
7.2-190 
7.2-191 
7.2-192 
7.2-193 
7.2-194 
7.2-195 
7.2-196 
7.2-197 
7.2-198 
7.2-199 
7.2-200 
7.2-201 7 2-202 
7 2-203 7 2-204 
7 2-205 
7 2-206 7 3-I 
7 3-2 
Most Recent Date Changed 
611171 
611171 
611171 
6/I171 
6/I171 
611/71 
611/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I/71 
6/I r71 
6/I r71 
6/I r71 
6/I r71 
6/I r71 
6/I r71 
6/I r71 
6/I 171 
6/I 171 
6/I _71 
3/I/71 
3/I/71 
Page No. 
7.3-3 7 3-4 
7 3-5 
7 3-6 7 3-7 
7 3-8 7 3-9 
7 3-10 
7 3-11 7 3-12 
7 3-13 
7 3-14 7 3-15 
7 3-16 
7 3-17 7 3-18 
7 3-19 
7 3-20 7 3-21 
7 3-22 7 3-23 
7 3-24 
7 3-25 7 3-26 
7 3-27 7 3-28 
7 3-29 
7 3-30 7 3-31 7 3-32 7 3-33 7 3-34 
Most Recent Date Changed 
311171 
311171 
311171 
3/I171 
3/I171 
3/I/71 
3/I/71 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 
311171 

xxxvii (8/I/72)

PROGRAM OVERVIEW 
I.I PROGRAMOVERVIEW 
l.l.l Objectives 
The NASTRAN program has been designed according to two classes of criteria. The first class relates to functional requirements for the solution of an extremely wide range of large and com plex problems in structural analysis with high accuracy and computational efficiency. These cri teria are achieved by developing and incorporating the most advanced mathematical models and com putational algorithms that have been proven in practice. In particular, they are achieved by providing such features as the bandwidth-with-active-column technique in matrix decomposition; packing routines to take maximum advantage of matrix sparsity so as to conserve input/output time; highly stable and efficient algorithms for the solution of problems in eigenvalue analysis and transient response; and an elegant approach to modeling the effects of control systems and other nonstructural components. 
The second class of criteria relates to the operational and organizational aspects of the program. These aspects are somewhat divorced from structural analysis itself; yet they are of equal importance in determining the usefulness and quality of the program. Chief among these criteria are: 
I. Simplicity of problem input deck preparation. 
2. Minimization of chances for human error in problem preparation. 
3. Minimization of need for manual intervention during program execution. 
4. Ease of program modification and extension to new functional capability. 
5. Ease of program extension to new computer configurations and operating systems, and generality in ability to operate efficiently under a wide set of configuration capabilities. 
6. Capability for step by step problem solution, without penalty of repeated problem set up. 
7. Capability for problem restart following unplanned interruptions or problem preparation error. 
8. Minimization of system overhead, in the three vital areas: 
a. Diversion of core storage from functional use in problem solution. 
l.l-I
NASTRAN PROGRAMMING FUNDAMENTALS 
b. Diversion of auxiliary storage units from functional to system usage. 
c. System housekeeping time for performing executive functions that do not directly further problem solution. 
These criteria are achieved in NASTRAN through modular separation of functional capabilities, organized under an efficient, problem-independent Executive System. 
This approach is absolutely essential for any complex multi-operation, multi-file application program such as NASTRAN. To see this, one must examine the implications of modularity in program organization. 
Any application computer program provides a selection of computational sequences. These are controlled by the user through externally provided options and parameter values. Since no user will wish to observe the result of each calculation, these options also provide for the selection of the data to be output. 
In addition to externally set options, internal switches whose setting depend upon tests performed during the calculations will control the computation sequences. There is, therefore, a natural separation of computations into functional blocks. The principal blocks are called functional modules; modules themselves of course may, and usually must, be further organized on a 
sub-modular basis. 
Despite this separation, however, it is clear that modules cannot be completely independent, since they are all directed toward solution of the same general problem. In particular, they must intercommunicate data among themselves. The principal problem in organizing any application program, large or small, is designing the data interfaces between modules. 
For small programs, the standard techniques are to communicate data via subroutine calling sequences and common data regions in core. For programs that handle larger amounts of data, auxiliary storage is used; however, strict specifications of the device_ used and of the data record formats are usually imposed. 
The penalty paid is that of "side effects". A change in a minor subroutine initiates a modification of the data interfaces that propagates through the entire program. When the program is small, these effects may not be serious. For a complex program like NASTRAN, however, they would be disastrous. 
1 ,I-2

PROGRAM OVERVIEW 
This problem has been solved in NASTRAN by a separation of system functions, performed by an Executive System, from problem solution functions, accomplished by modules separated strictly along functional lines. Each module is independent of all other modules in the sense that modification of a module, or addition of a new module, will not in general require modification of other modules. Even so, programming constraints on module development do exist but are minor. The essential restrictions are: 
I. Modules may interface with other modules only through auxiliary storage files, as opposed to passing information between each other while in core. 
2. Since the availability and allocation of auxiliary files for module execution interact with the execution of other modules, no module can specify or allocate files for its input or output data. All auxiliary storage allocation is reserved as an Executive function. 
3. Modules operate as independent subprograms, and may not call, or be called by, other modules. They may be entered only from the Executive System. 
4. Modules may interface with the Executive System through a parameter table that is maintained by the Executive System. User-specified options and parameters are communicated to modules in this way. The major line of communication is one-way, from user to Executive routine to module. However, in addition, an appreciable two way communication, from module back to executive routine (and therefore to other modules) is permitted via the parameter table. 
5. Intra-module parameter communication is format-free in the sense that each module defines and orders its own local parameter set internally. Thus each module is independent of common data formatting by any other module. 
No other constraints, except those imposed by the resident compilers and operating systems, are required for functional modules. 
l.l.2 ProBram Organization 
Because of the very large size of the NASTRAN program (more than 750 decks and 300 individual overlay segments), execution as one physical program was not possible. However, to meet the stated design objectives, it was required that NASTRA_ appear to the resident operating system as one program. 
1.1-3
NASTRAN PROGRAMMING FUNDAMENTALS 
A program structure evolved which is basically computer independent, although the way in which the code structure is supported varies across the computers. 
The NASTRAN program is divided into a series of logical pieces called links. Each link con tains its own root segment (the set of subprograms which is always core resident for that link) and its own complete overlay structure. Each link is capable of performing a predefined subset of NASTRAN operations. Communication between links occurs through computer files. Control of the sequence of execution of the links is performed entirely by the NASTRAN program and requires no operator intervention. As a result of this approach, a NASTRAN program execution appears to the resident operating system as a normal batch job to be processed in the batch stream. Detailed descriptions of the way in which the link structure is implemented on each computer are given in section 5. 
1 .I-4
NASTRANEXECUTIVE SYSTEM 
1.2 NASTRANEXECUTIVE SYSTEM 
1.2.1 Introduction 
The essential functions of the Executive System are: 
I. Establish and control the sequence of module executions according to options specified by the user. 
2. Establish, protect, and communicate values of parameters for each module. 
3. Allocate system files to all data blocks (a data block designates a set of data, matrix or table, occupying a file) generated during program execution. A file is "allocated" to a data block, and a data block is "assigned" to a file. The general data block I/_ routine 
(GIN_) and the data card conversion routines (XRCARD and RCARD) are considered Input/Output utilities and are discussed separately in section 1.6. 
4. Maintain a full restart capability for restoring a program execution after either a scheduled or unscheduled interruption. 
The Executive System is open-ended in the sense that it can accommodate an essentially unlimited number cf functional modules, files, and parameters. Modification of the Executive System necessary for change, addition, or extension of functional modules is restricted to changes in entries in control tables stored within the Executive routines. 
Program execution is divided into two phases: l) the Preface, in which modules XCSA, IFPI, XS_RT, IFP and XGPI are executed to: a) process the NASTRAN input data deck and b) perform general problem initialization; and 2) the program body itself, in which the sequence of program operations is controlled by the Operation Sequence Control Array (_SCAR) Executive table, which was developed in the XGPI module of the Preface. A diagram of a sample NASTRAN input data deck is shown in Figure I. Note that a NASTRAN input data deck consists of 3 separate decks: l) the Executive Control Deck, 2) the Case Control Deck and 3) the Bulk Data Deck. A detailed descrip tion of the contents of the NASTRAN data deck is given in section 2 of the User's Manual. The flow of operations during the Preface is presented in Figure 2. The numbers in the blocks in Figure 2 refer to section numbers where more detailed explanations of the subroutines and modules can be found. 
1.2-I
NASTRAN PROGRAMMING FUNDAMENTALS 
_'_ ' I ENDDATA 
< 
_C_.o"_ I DISPL = ALL 
\ 
,. j x) i OUTPUT 
\ 
>< I L(_AD= 2 
•_ _ \ ISPC : 5 ' 
\ 
_ _ _ I TITLE = SAMPLE PR_IBLEM 
_ o_"_ ICEND 
_J%_ I SeL l,O 
_x_ IAPP DISPLACEMENT ITIME 40 
I CHKPNT = YES 
ID JBBOOO,ABC 
Figure I. Sample NASTRAN input data deck. 
l.2-2

NASTRANEXECUTIVE SYSTEM 
C ENTRY) 
1 
I GenerateTables the Initial (GNFIAT-3.3L.4) File Allocation I 
I ReadControl and Analyze Deck the (XCSA-4.2) Executive 
Ip_cess t_ICasePl-,.3_ C°nt_1 _c_I 
I Sort the(XS@RT-4.4) Bulk Data Deck I 
Process the Bulk Data Deck 
(IFP-4.5) 
Conical Shell 
_ H_droelastic 
No 
Further Process Data Specific to 
the Conical Shell Problem (IFP3-4.6) 
Further Hydroelastic ProcessProblem Data SDecific (IFP4-4.89)to the or Acoustic Problem (IFP5-4.90) 
Perform General Problem 
Initialization (XGPI-4.7) 
Figure 2. Flow of operations during the Perface. 1.2-3 (8/I/72)
NASTRAN PROGRAMMING FUNDAMENTALS 
1.2.2 Executive Operations During the Preface 
The sequence of Preface operations shown in Figure 2 is controlled by the Sequence Monitor Initialization subroutine, SEMINT (see section 3.3.3). Each routine called by SEMINT is dis cussed in the following sections. The numbers in the section headings refer to section numbers where more detailed information on the subroutine or module can be found. 
1.2.2.1 Generation of the Initial File Allocation Tables (GNFIAT section 3.3.4) 
Two file allocation tables are maintained by the NASTRAN Executive System. One table, FIAT, (see section 2.4) defines the files to which data blocks generated during solution of the problem will be allocated. The second table, XFIAT, (see section 2.4) includes files to which permanent Executive data blocks, such as the New Problem Tape, the Old Problem Tape, plot tapes, and the User's Master File are assigned. 
The New Problem Tape will contain those data blocks generated during the solution that are necessary for restarting the problem at any point. The Old Problem Tape contains the data blocks saved from some previous execution that may serve to bypass steps in the solution of the new problem. The User's Master File is a permanent collection of useful information, such as material properties, that may be used to generate input data. 
The generation of the XFIAT and FIAT tables is a computer dependent operation since direct interface with the operating system of the computer must be made. The GNFIAT routine, which accomplishes this function, interrogates file tables in the nucleus of the operating system. Files which are available for use by the NASTRAN program are reserved, and the unit numbers for these files are stored in the NASTRAN file allocation tables. An indication of which units are physical tapes is also stored. If the number of files available is insufficient to run the pro blem, an error message is generated, and the run is aborted. 
1.2.2.2 Analysis of the Executive Control Deck (XCSA Section 4.2) 
The Executive Control Deck is processed and analyzed by the XCSA Executive Preface module. The Executive Control Deck includes cards which describe the nature and type of solution to be performed. This includes an identification of the problem, an estimated time for solution of the problem, the approach, a selection of the Rigid Format to be executed or an alternative sequence of NASTRAN operations (DMAP) to control the solution, a restart deck from a previous run if the 
1.2-4

NASTRAN EXECUTIVE SYSTEM 
solution is to be restarted, an indication of any diagnostic printout to be made, a specification of whether the problem is to be checkpointed or not, and, if a Rigid Format is selected, any desired alterations to that format. Section 2 of the User's Manual should be consulted for the formats of, and restrictions on, each of the cards in the Executive Control Deck. The approach 
(APP) card, and the solution (S_L) card, which selects a particular solution (Rigid Format) to be executed, are worthy of special note. However, firstsome introductory definitions are required. 
The sequence of operations to be executed during the program body is written in a data block oriented language called DMAP, an acronym for "Direct Matrix Abstraction Program". A DMAP instruc tion is a statement in the DMAP language, a DMAP sequence is a set of DMAP instructions, and a DMAP loop is a DMAP sequence to be repeated. A DMAP module is one which is "called" by means of a DMAP instruction. 
A Rigid Format consists of: a) a fixed pre-stored DMAP sequence and b) its associated restart tables. A Rigid Format performs a specific (structural) problem solution. Section 3 of the User's Manual presents the DMAP sequence and the associated restart tables for each Rigid Format. 
The APP card of the Executive Control Deck defines the problem solution approach. The APP card is required, and there are two options on the APP card: DISPLACEMENT or DMAP. The S@L card has the form 
S_L n,m 
where n = Rigid Format number, and m = a subset of the Rigid Format. The S_L card is required if the DISPLACEMENT option is chosen on the APP card. The S_L card must not be present in the deck if the DMAP option is chosen. 
In addition to using the Rigid Formats provided automatically by NASTRAN, the user may wish either to execute a series of modules in a manner different from that provided by the Rigid Format, or to perform a series of matrix operations which are not contained in any existing Rigid Format. If the modifications to an existing Rigid Format are minor, the ALTER feature described in Section 2 of the User's Manual may be employed. Otherwise, a user-written Direct Matrix Abstraction Program (D_P) should be used, in which case the card 
APP D_JAP 
must be used. Chapter 5 of the User's Manual discusses DMAP. 
1.2-5
NASTRAN PROGRAMMING FUNDAMENTALS 
Each of the cards comprising the Executive Control Deck is read via XRCARD (3.4.19) and analyzed. Depending on the card, information is either stored in various Executive tables main tained in core storage or written in the Executive Control Table (2.4.2.5) on the New Problem Tape for further processing during the general problem initialization phase (XGPI-4.7) of the Preface. Figure 3 presents the format of the Problem Tape. The formats of the New and the Old Problem Tapes are identical; only chronology defines their separate functions. 
1.2.2.3 Processing of the Case Control Deck (IFPI Section 4.3) 
The Case Control Deck includes the following classes of cards: selection of specific sets of data from the Bulk Data Deck, selection of printed or punched output, definition of subcases, definition of structural plots to be made, and definition of XY plots to be made. Section 2 of the User's Manual discusses in detail all cards of the Case Control Deck. 
This deck is read via XRCARD (3.4.19) and processed. Information defining set selection, output selection and subcase definition is written into the Case Control data block, CASECC. Information defining plot requests is written in the Plot Control (PCDB) and XY Control (XYCDB) data blocks. 
If the problem is a restart, a comparison with the Case Control Deck from the previous run is made. Differences are noted in an Executive restart table, which is used in the general pro blem initialization phase (XGPI-4.7) of the Preface. 
1.2.2.4 Sorting of the Bulk Data Deck (XS_RT Section 4.4) 
The function of the XS_RT routine is to prepare a file on the New Problem Tape (see section 1.2.2.1) which contains the sorted Bulk Data Deck (bulk data). Operation of the routine is influenced by the type of run. If the run is a cold start, the bulk'data is read from the system input file (e.g. card reader) or the User's Master File, sorted, and written on the New Problem Tape. If the run is an unmodified restart, (restarts are discussed in section I.I0), the bulk data is copied from the Old Problem Tape (see section 1.2.2.1) to the New Problem Tape. If the run is a modified restart, the bulk data is read from the Old Problem Tape, and cards are deleted and/or added in accordance with cards in the system input stream. The modified bulk data is sorted and written on the New Problem Tape. Additionally, any changes in the data are noted in the Executive restart table. 
A printed list of the unsorted bulk data is given if requested by an ECHO card in the Case Control Deck. Similarly, the sorted bulk data is echoed on request. 
1.2-6
NASTRAN EXECUTIVE SYSTEM 
All files begin with an 
eight character (2 word) 
BCD header record. 

PROBLEM ID FILE 
(always present) 
ALTER FILE 
(only if ALTER 
cards are present) 
EXECUTIVE C_NTROL TABLE FILE (always present) 
CASE C_NTR_L FILE 
(always present) 
B 
M_NTH -Is___l-- DAY __--LYEAR REEL # 
_ XALTER (header) _ AA 
_ XCSA (header) _ 
first and second fields from ID card (BCD) 
-_---problem date 
_reel sequence no. 
(see section 2.4.2.6) 
Note: ^denotes BCD blank (see section 2.4.2.5) 
(see section 2.3.1.I) 
BULK DATA CARD FILE 
(always present) 
are present) [ 
PARAMETER VALUE FILE 
(only if PARAM cards 
(only if CHKPi4Tor 
CHECKPBINT FILES { 
BULKDATA (header) -- 
_bulk data card images (see section 2.4.2.4) 
_all checkpointed data blocks separated by E_F's 
RESTART card is present){ 
PROB. TAPE DICT. FILE 
(only if CHECKPOINT 
FILES are present) 
XPTDIC (header) _ ^A 
_always the last file (see section 2.4.2.3) 

Figure 3. Problem tape format (same format for ;_ewProblem Tape and Old Problem Tape). 1.2-7
NASTRAN PROGRAMMING FUNDAMENTALS 
Since the collating sequence of alphanumeric characters varies from computer to computer, the sort routine converts all characters to an internal code prior to sorting. Following the sort, the characters are reconverted. In this way, the collating sequence is computer independent. 
The algorithm used by the sort routine is biased toward the case where the data in sort or nearly in sort. Consequently, Bulk Data Decks which are nearly in sort will be processed efficiently by the routine. 
1.2.2.5 Processing of the Bulk Data Deck (IFP Section 4.5) 
The sorted Bulk Data Deck is read card-by-card from the New Problem Tape by the Input File Processor (IFP) and converted to internal binary form by RCARD (3.4.20). Each of the cards is checked for correctness of format. If any data errors are detected, a message is written, and a switch is set to terminate the run at the conclusion of the Preface. Section 2 of the User's Manual presents a detailed description of all cards of the Bulk Data Deck. 
Processing of each bulk data card depends on the type of card. All bulk data cards of the same type are written into the logical record to which the card type has been assigned. These records are organized into data blocks classified according to general categories of use and written on prescribed preallocated files. 
1.2.2.6 Processing of Conical Shell Data (IFP3 Section 4.6) 
If the problem is a conical shell problem, further processing of the bulk data specific to the conical shell problem is accomplished. The nature of this processing is to convert data for the conical shell model into formats of a conventional statics problem. The result is that the conical shell problem can be described in a format convenient to the analyst a_d processed by NASTRAN in a format convenient to the program. 
1.2.2.7 Processing of Hydroelastic Data (IFP4 Section 4.89) 
If hydroelastic analysis data exists, this data must be converted to the data block formats and merged with existing data output from IFP. This module creates grid point, scalar point, element connection, and constraint data as well as producing a section in the MATP_L data block. 
1.2-8 (8/I/72)
NASTRAN EXECUTIVE SYSTEM 
1.2.2.8 Processing of Acoustic Data (IFP5 Section 4.91) 
If acoustic analysis data exists, the IFP5 module generates and merges grid points, scalar elements, and plotting elements with the existing data blocks. 
1.2.2.9 General Problem Initialization (XGPI Section 4.7) 
The Executive General Problem Initialization (XGPI) module is the heart of the Preface. Its principal function is to generate the Operation Sequence Control Array (_SCAR-2.4.2.1), which defines the problem solution sequence. The BSCAR consists of a sequence of entries, with each entry containing all of the information needed to execute one step of the problem solution. The _SCAR is generated from information supplied by the user through his entries in the Executive Control Deck. This information is supplied by the S_L card, which points to a Rigid Format, or by a user supplied DMAP sequence. 
The initial sequence of instructions was written in the Executive Control Table (2.4.2.5) on the New Problem Tape by the XCSA Preface module. This table is read to initiate assembly of the BSCAR. 
If the problem is a restart, the restart dictionary (contained in the Executive Control Table) and the Executive restart table are analyzed to determine which data blocks are needed to restart the solution and which operations in the _SCAR need to be executed to complete the solution. Entries in the BSCAR for operations not required for the current solution are flagged for no operation. 
To aid in efficient assignment of data blocks to files, two attributes are computed and included with each data block in each entry of the BSCAR. These attributes are: a) the BSCAR sequence nun_er when the data block is next used (NTU) and b) the _SCAR sequence nu_er when the data block is last used (LTU). Details of the file allocation are discussed in section 1.2.3.3. 
When generation of the _SCAR is complete, it is written on the Data Pool File (P_L). If the problem is restart, data blocks needed for the current solution are copied from the Old Problem Tape to the Data Pool File. 
1.2-9 (811172)
NASTRAN EXECUTIVE SYSTEM 
1.2.3 Executive Operations Durin 9 Problem Solution 
1.2.3.1 Sequence Monitor (XSEMi Section 3.3.7) 
When the Preface has been completed, solution of the problem is initiated. This solution is controlled by the sequence monitor. Figure 4 shows the flow for the sequence monitor. Note that there are i copies of XSEMi within NASTRAN, one controlling each link's operation. Section 1.1.2 defined the necessity for these divisions. 
The sequence monitor reads an entry from the _SCAR (2.4.2.1) which defines one step in the problem solution in terms of: the operation to be performed, data blocks required for input, data blocks to be output, scratch files required and parameters used. The File Status Table (FIST-2.4.1.3), which relates the internal data block reference numbers (see Section 1.6.4) to the file position in the File Allocation Table (FIAT-2.4°1.2), is created by the FIST generator, subroutine GNFIST. When the status table is complete, XSEMi moves the parameters required for the operation into blank common and calls the requested module (if within the current link) to begin the operation. If the requested module is not within the current link, ENDSYS (see Section 3.3.5) is called and the Sequence Monitor within the new link is executed. 
With the exception of XSFA, the seven routines described in the following subsections are Executive modules called directly by XSEMi to perform their specified functions. 
1.2-9a (8/I/72)

NASTRAN PROGRAMMING FUNDAMENTALS 
ENTER 
I (Preface Call SEMINT Only) 
__ OSCAR Readnext entry I_" 
_;o 
_Y_s 
Generate FIST for 
Input, _utput, 
Scratch Data Blocks 
from VPS 
Move Parameters I 
to Blank Common 
No 
Call EXEC Routine 
(XCEI, CHKPNT, PURGE EQUIV, SAVE) 
I Call module I 
_d 
ENDSYS 
Call 1 
Writer 
Call Message 1 MSGWRT 

Figure 4. Flow diagram for the sequence monitor, XSEMi. 1.2-I0
NASTRAN EXECUTIVE SYSTEM 
1.2.3.2 FIST Generator (GNFIST Section 3.3.9) 
The FIST generator, subroutine GNFIST, creates the File Status Table (FIST), which contains the linkage between the internal data block reference numbers and the actual system files listed in the File Allocation Table (FIAT). Each input, output and scratch data block required by the forthcoming module is assigned an internal reference number if found to be active in FIAT. A data block found to be inactive, that is purged or not generated, will not be assigned a reference number. This missing reference number will cause the accessing module to be signaled regarding the inactive status. If, during the generation of the FIST, a data block is not found in the FIAT, active or inactive, the Executive Segment File Allocator (XSFA) module is called by GNFIST to make a file available to the subject data block. 
1.2.3.3 Segment File Allocator (XSFA Section 4.9) 
The Executive Segment File Allocator (XSFA) module, which is called exclusively by GNFIST, is the administrative manager of data blocks for NASTRAN. Since, in general, the number of data blocks required for solution of a problem far exceeds the number of files available, assignment of data blocks to files is a critical operation for efficient execution of NASTRAN. 
The Executive Segment File Allocator module is called whenever a data block is required for execution of an operation but is not currently assigned to a file (i.e., does not appear in the FIAT). When the Segment File Allocator is called, it attempts to allocate not just for the data block initiating the call, but for as much of the remaining problem solution as possible. This allocation depends on the type of problem, the number of files available, and the range of use of the remaining data blocks. 
1.2-11 (8/I/72)
NASTRAN PROGRAMMING FUNDAMENTALS 
The Segment File Allocator reads entries from the _SCAR from the point of current operation to the end of the problem solution. The FIAT table entries are created in which attributes of the data blocks, including their next use (NTU) and last use (LTU), are stored. Data blocks which are currently assigned to files but are no longer required for problem solution are released. In certain cases, when the range of use of a data block is large, it may not be possible to allocate a file to the data block throughout its range of use. In this case, pooling of the data block is required so that the file to which the data block was assigned may be freed for another allocation. The next time used (NTU) attribute for a data block is used to efficiently pool data blocks. In general, the data block whose next use is the furthest from the current point is pooled, that is, copied onto the Data Pool File (P_L). The format of the Data Pool File is shown in Figure 5. 
One additional check is made with regard to pooling. The operation of the Segment File Allocator itself is less expensive than a pooling operation. Therefore, pooling occurs only when the module for which the allocation was required cannot be allocated without pooling. 
_hen the Segment File Allocator is complete, a new File Allocation Table (FIAT) has been generated. This table is used until the solution again reaches a point where a data block is required to execute an operation but is not assigned to a file. 
1.2.3.4 Interpretation of Executive Control Entries (XCEI Sections 4.11, 4.12, 4.13, 4.14) 
Executive control entries include the DMAP instructions: REPT, JUMP, C_ND and EXIT. Executive control entries in the _SCAR are processed by the Executive Control Entry Interpretor (XCEI). When such an entry is encountered in the _SCAR, the Control Entry Interpretor is called 
by XSEMi. If the operation is a jump, cor, ditional jump or repeat, the _SCAR is repositioned accordingly. If the operation is an exit, the NASTRAN termination routine PEXIT (3.4.22) is called. 
1.2.3.5 Checkpointing Data Blocks (CHKPNT Section 4.10) 
The checkpoint module (DNLAP name: CHKPI_T; entry point name: XCHK) copies specified data blocks required fcr problem restart onto the New Problem Tape and makes appropriate entries in the restart dictionary. This dictionary is also punched onto cards as each new entry is made. Thus, in the event of any unscheduled problem interruption, a restart from the last checkpoint 
1.2-12 (lllll70)

NASTRA;_EXECUTIVE SYSTEM 
All files begin with an 
eight character (2 word) 
BCD header record. 
FF 
-- XIBSCAR^^(header) - 
(always present) 
_SCAR FILE I 
_data blocks from DMI'sand DTI's (if present) separated by E_F's 
i4ote: ^denotes BCD blank 
(see section2.4.2.1) 
-_-data blocks pooled by XSFA (if necessary) separated by E_F's 

Figure 5. Format of the Data Pool File. 1.2-13
NASTRANPROGRAMMINGFUNDAMENTALS 
can be made using the Problem Tape and the restart dictionary from the interrupted run. 1.2.3.6 Purging a Data Block (PURGE Section 4.16) 
The purge routine (DMAP name: PURGE; entry point name: XPURGE) flags data blocks so that they will not be assigned to physical files. This special status provides a means for logically suppressing a segment of processing steps requiring the data block. Thus, if the function of a module is to multiply two matrices and add a third matrix to the product, the addition step might be deleted by purging the data block corresponding to the third matrix. 
1.2.3.7 Equivalencing Data Blocks (EQUIV Section 4.17) 
The equivalence routine (DFtAPname: EQUIV; entry point name: XEQUIV) attaches one or more equivalent data block names to an existing data block. This special status provides a means of logically removing a module function by making a data block input to the module equivalent to a data block output from the module. Thus an entire module could be skipped, and an input data block "copied" to an output data block without physically moving the data from one file to another. 
1.2.3.8 Saving Parameters (SAVE Section 4.15) 
The save routine (DMAP name: SAVE; entry point name: XSAVE) provides a protection feature for the parameters communicated between, and used by, the functional modules. All variable para meters are stored within the VPS Executive table (see section 2.4). Prior to each module's operation, the subset of parameters required by the module is moved to blank common. The module may use or modify this subset of parameters as desired. When the module terminates operation, only those parameters within the subset designated to be saved are restored to the Executive table. 
l.2-14 (ll/I/70)

WORDSIZE AND COMPUTERHARDWARECONSIDERATIONS 
1.3 WORDSIZE AND COMPUTERHARDWARECONSIDERATIONS 
1.3.1 Introduction 
Although NASTRAN is a F@RTFCANoriented system, considerable effort was required to develop programming and word handling techniques applicable to four separate computer configurations. llnesecomputers exhibit wide differences in their binary word sizes and integer representation method. The current computer configurations considered and their significant differences follow: 
I. Computer - IBM 7094/7040 DCS 
Word Size - 36 Bits 
Character Capacity - 6 bits/character and 6 characters/word 
Integer Representation - Sign and Magnitude 
2. Computer - IBM System/360 series 
Word Size - 32 Bits 
Character Capacity - 8 bits/character and 4 characters/word (character z byte) Integer Representation - Twos complement for negative integers 
3. Computer - UNIVAC If08 
Word Size - 36 Bits 
Character Capacity - 6 bits/character and 6 characters/word 
Integer Representation - Ones complement for negative integers 
4. Computer - CDC 6600 
Word Size - 60 Bits 
Character Capacity - 6 bits/character and lO characters/word. 
Integer Representation - Ones complement for negative integers 
Various Executive routines (e.g., XSORT (4.4), XRCARD (3.4.19)) that deal directly with character strings from the input stream require some method of obtaining the above computer dependent information. SJithinthe NASTRAN Preface, subroutine BTSTRP (3.3.2) solves an algorithm that determines which of the four computers is currently operating. This algorithm functions by inspecting the word length (by means of shifting and testing) and by checking the negative integer representation method. As a result of these tests, a word (MACH) withi_ the SYSTEM Executive table (see section 2.4) is set to indicate the computer type. Since data within BTSTRP defines the number of bits-per-word (NBPW), the nun_er cf characters-per-word (NCPW), and the nun_er of 
1.3-I
NASTRAN PROGP_AMMINGFUNDAMENTALS 
bits-per-character (NBPC) for each computer type, the correct values for these parameters are also stored into the SYSTEM table. This table resides within the NASTRAN root segment and is thus accessable to any module or subroutine. 
1.3.2 AIphanumeric _ata 
Data stored within a computer as binary-coded-decimal (BCD) characters must be represented by the proper hardware defined bit codes. These character codes (and in the case of the IBM System/360, the number of bits representing the code) vary among the NASTRAN computer types. Although the number of characters-per-word could have been obtained from the SYSTEM table, various data blocks and buffers within NASTRAN required firm entry sizes, regardless of computer type, to facilitate indexing. For these reasons, the minimum number ef characters-per-word (4) among the four computer types was chosen as a program design standard. Computer types with a word capacity of greater than four characters will have the unused low order character positions filled with BCD blanks. 
1.3.3 l_ord Packing 
Standard F_RTP_AN compilers do not provide the capability for storing or retrieving data that occupies less than a full computer word. Through the Machine Word Functions (MAPFNS, 3.4.1) routine some limited word packing (not to be confused with matrix packing) is performed within the Executive System and a few utility subroutines. Packing provides an efficient use of memory space at the expense of the additic.nal operating time needed to combine or separate the elements of the packed words. The Machine Word Function _RF is generally used for combining elements, while ANDF with a suitable mask is used for separating them. 
1.3.3.1 Examples of Machine Word Functions (MAPFNS) Usage 
Assume three lO-bit items of data occupy the low order I0 bits of three separate 30-bit computer words (A, B, and C). To pack these three items into a single 30-bit word (X), perform the following steps using the individual functions available within F_PFNS: a) Left shift (LSHIFT) word A, twenty bits 
b) Left shift (LSHIFT) word B, ten bits 
c) Logically add (_RF) words A and B; store into X 
1.3-2

WORD SIZE AND COMPUTER HARDWARE CONSIDERATIONS 
d) Logically add (_RF) words X and C; store into X. 
Assume two 8-bit items of data are packed into the left and right halves of a 16-bit word (X). To unpack these two items into the low order 8 bits of two separate 16-bit words (A and B), per form the following steps using the individual functions available within MAPFNS: 
a) Create )(ASKcontaining 8 low order bits equal to l and the 8 high order bits equal to 0 b) Right shift (RSHIFT) word X, eight bits; store into A 
c) Logically multiply (ANDF) word X by MASK; store into B. 
In the preceding example, the word X remains unchanged since the functions return the requested modified result in a computer register. 
1.3-3
SYSTEMBLOCKDATA SUBPROGRAM(SEMDBD) 
1.4 SYSTEMBLOCKDATA SUBPROGRAM(SEMDBD) 
NASTRAN contains a master block data program (SEMDBD) which is responsible for defining and initializing (root segment) common blocks. The common blocks referenced in SEMDBD are either Executive common blocks (XFIAT, XXFIAT, XFIST, etc.) which require initial values, or general information common blocks (SYSTEM, NAMES, TYPE, etc.) which are referenced by many modules. The source listing for SEMDBD identifies the common blocks, and it documents the data which are initialized, via comments. In aadition, the Executive common blocks are documented in section 2.4 and the non-Executive common blocks in section 2.5. Certain parameters in these common blocks contain machine dependent values such as word size, number of BCD characters per word, etc. These values are set by subroutine BTSTRP (section 3.3.2) by identifying the machine on which the NASTRAN program is currently operating and setting the values accordingly. 
1.4-I
THEOPENCORECONCEPT 
1.5 THEOPENCORECONCEPT 
1.5.1 Introduction 
The design philosophy of the NASTRAN system dictated a completely open ended design whenever possible. NASTRAN was to have the flexibility to operate on a second generation machine with a 32K core (the IBM 7094/7040 DC$) as well as the largest of the IBM S/360 series of computers, and take complete advantage of the additional core storage without major program changes. The use of a fixed dimension for large arrays was outlawed since this automatically restricted the size of a problem that could be solved. Instead, modules were to be programmed to allocate space as required and to use spill logic to transfer data to scratch files if complete core allocation was in,possible. In this manner, a problem might cause spill logic to be used on a computer with limited core storage, but not on a computer with a larger core storage capacity. 
1.5.2 Definition of Open Core 
The definition of open core is: a contiguous block of working storage defined by a labeled common block whose length is a variable determined by the NASTRAN Executive function C_RSZ. The implementation of this definition by the module writer consists of the origining of a labeled common block at the end of his overlay segment. This labeled common block contains a dimensioned variable of length I. C_RSZ returns the number of words of core available between his open core origin and the end of core. The module writer can now write his program as if he had dimensioned his array by that nun_ber. In actuality, he is extending beyond the area reserved for the array into an area reserved for the job but not currently used by the segment. When implementing this concept, care must be taken to assure that the system does not use this area. 
1.5.3 Example of an Application of Open Core 
Figure l demonstrates the use of open core by two subroutines, A and B. By some means, which are machine dependent and are discussed in section 5, an end point is established for open core. The length of open core is then the difference between this end point and the labeled common block. In the example shown, subroutine A will have more open core available to it than B does. 
l.5-I

SUBROUTINEA 
C@MM_N// XX 
COMMON/AX/ Z(1) INTEGER C_RSZ NZ = C_RSZ(Z(I),XX) D_ I0 1 : I, NZ 
NASTRANPROGRAMMINGFUNDAMENTALS 
SUBROUTINEB 
CBMM_N// XX 
C_MMON/BX/ Z(1) INTEGER C_RSZ NZ : CORSZ(Z(1),XX) D@I0 I = I,NZ 

I0 
Z(I) : I RETURN END 
SUB. A /AX/ 
SUB. B 
lO z(1) : I 
RETURN 
END 

Open core for SUB. A L 
1 
/BX/ 
//ix 
Open core for SUB. B 

Blank common 
establishes the end of open core for some 
machines (see section 5). Figure I. 
_End of open core 
available for this 
job. 
A example of the use of open core. 1.5-2

NASTRANINPUT/OUTPUT 
1.6 NASTRAN INPUT/OUTPUT 
1.6.1 Introduction 
The particular (IBM 7094, IBM S/360, Univac ll08, CDC 6600) operating system input and out put files provide the required data connection between NASTRAN, the input data decks and the printed output. Utility subroutines XRCARD (section 3.4.19) and RCARD (section 3.4.20) convert special NASTRAN input card formats to standard F_RTRAN data words easily handled by all NASTRAN input processors. Printed output is generated through F_RTRAN formatted write statements. All internal data block input/output is handled by GIN_, the system of NASTRAN general purpose input/ output routines. GIN_ provides the required manipulation to tailor the variable length logical data records needed by most NASTRAN modules to fixed length records available on all direct access mass storage hardware. 
1.6.2 Use of the Operatin9 System Input File 
The system input file is read only by the following routines within the NASTRAN Preface: 
I. SEMINT (see section 3.3.3) reads the first card and processes it using utility XRCARD if it is the NASTRAN card (see section 6.3.1). 
2. The Executive Control Deck containing free-field cards is read and processed by XCSA (section 4.2) using the XRCARD utility. 
3. The Case Control Deck containing free-field cards is read and processed by IFPI (section 4.3) using the XRCARD utility. 
4. The Bulk Data Deck containing fixed-field cards is read by XS_RT (section 4.4). This data is subsequently processed by IFP (section 4.5) using the RCARD utility. 
These card conversion utilities (XRCARD and RCARD) provide respectively all the free-field and fixed-field data card processing required by NASTRAN. 
1.6.2.1 Use of the Subroutine XRCARD (See Section 3.4.19) 
XRCARD interprets NASTRAN free-field data cards and processes the fields into a sequential buffer that can be easily handled by subsequent modules. Free-field data consist of series of data items separated by suitable delimiters and punched in non-specific card columns. Data items may include alphanumeric, integer, and various types of real variables. Field delimiters 
1.6-I (12-I-69)
NASTRAN PROGRAMMING FUNDAMENTALS 
may include the comma, slash, parenthesis, and blanks. For details regarding data and delimiter usage and the format of the sequential output buffer, see the XRCARD subroutine description in section 3.4.19. 
1.6.2.2 Use of the Subroutine RCARD (See Section 3.4.20) 
RCARD interprets NASTRAN fixed-field data cards and processes the fields into a sequential buffer that can be easily handled by subsequent modules. Fixed-field data consist of data items punched within specific card fields. Each eighty-column card is divi_ed into an eight-column ID field (for the card mnemonic) followed by either eight eight-column data fields or four sixteen-column data fields. A special character (asterisk or plus) within the ID field determines when the card is to be interpreted as containing sixteen-column fields. The last eight columns of the card are for continuation mnemonics used by XSORT and are not processed by RCARD. The data item within the ID field must be alphanumeric. The data items within all other fields may include alphanumeric, integer, and various types of real variables. For Vetails regarding data and the format of the sequential output buffer, see the RCARD subroutine description in section 3.4.20. 
1.6.3 Use of the Operatin_ Syster_ Output File 
Although NASTRAN printed output is formed and placed onto the system output file through use of standard FORTRAN formatted write statements, two basic NASTRAN design concepts prohibit every operating module from generating printed output. Firstly, since the FORTRAN I/0 package for output generation occupies a sizable block of computer memory, this package is generally positioned by loader directives within specific output oriented segments, rather than within the root segment of the overlay, to reduce the total memory requirement. Secondly, because many functional modules generate the same or similar diagnostic and information messages, a NASTRAN message writer (MSGWRT) was developed to centralize message text and thus prevent duplications within many separate modules. 
For the reasons previously discussed, NASTRAN output generation is restricted to a specific class of modules which can reside within an output oriented segment below the link root segment. These segments will contain the output producing modules such as the Output File Prc_cessor (OFP section 4.70), the Message Writer (MSGWRI - section 3.4.26), and the various table and matrix printers (TABPT - section 3.4.29, MATPRT - section 4.71, etc.) along with the output titling (PAGE - section 3.4.24) and necessary FORTRAN I/0 packages. 
1.6-2
NASTRAN INPUT/OUTPUT 
1.6.4 GIN_ 
GIN@ is a collection of subroutines which provide for all input and output operations within NASTRAN except reading data from the resident system input file and writing data on the resident system output and punch files. These latter operations are accomplished through F_RTRAN formatted read/write statements. NASTRAN programs perform input/output operations by making the following calls to GIN_ entry points: 
I. @PEN (see section 3.4.2) 
OPEN initiates activity for a file (unless the data block assigned to the file is purged, in which case an alternate return is given). A working storage area (GIN@ buffer), for use by GIN@, is assigned (allocated) by the calling program thus providing optimum allocation of storage by the calling program. This working storage area is reserved for use by GIN_ until activity on the file is terminated by a call to CLOSE (see paragraph 4 below). On each of the NASTRAN computers, the working storage area allocated by the calling program is separate from the actual physical I/_ buffer. 
2. WRITE (see section 3.4.3) 
WRITE writes a specified (by the calling program) number of words on a file. The block of words to be written may comprise an entire logical record or portion of a logical record. 3. READ (see section 3.4.5) 
READ returns to the calling program a specified (by the calling program) number of words from the logical record at which the file is currently positioned. READ may be used to trans mit an entire logical record or portion of a logical record. 
4. CLOSE (see section 3.4.4) 
CLOSE terminates activity for a file. The working storage area assigned at _PEN is released. The file is repositioned to the load point if requested. 
5. REWIND (see section 3.4.8) 
REWIND repositions the requested file tc the load point. The file must be "open", i.e. a REWIND operation is requested subsequent to a call to @PEN and prior to a call to CLOSE. 
6. FWDREC (see section 3.4.6) 
FWDREC repositions the requested file one logical record forward. 
1.6-3
NASTRAN PROGRAMMING FUNDAMENTALS 
7. BCKREC (see section 3.4.7) 
BCKREC repositions the requested file one logical record backwards. 
8. SKPFIL (see section 3.4.10) 
SKPFIL repositions the requested file forward or backward N logical files where N is specified by the calling program. 
9. E_F (see section 3.4.9) 
E_F writes a logical end-of-file on the requested file. 
The basic unit of I/0 in NASTRAN is a logical record. The length of a logical record is completely variable and may range from one word to an arbitrarily large number of words. For NASTRAN matrix data blocks, the convention was adopted that each column of the matrix would com prise one logical record. For NASTRAN data blocks containing tables, no rigid convention exists. Typically each logical record contains one table of a specific type. 
Tile logical record concept provides greatest ease in prcgramming. However, since these records must be stored on a physical device such as a drum, disk or tape, the characteristics of the device must be taken into consideration. The bulk of NASTRAN data is stored on drums or disks. For both these devices the common unit of organization is a track, which stores a fixed number of words. Thus, there is a conflict between the variable length GIN_ records and the fixed length tracks. 
This conflict is resolved by blocking. G!N@ acts as the interface between tile device and the NASTRAI_ program. Using this technique, the program itself need not be concerned with device considerations (which would create machine dependent code). GIN_ has been parameterized so that different devices may be easily accommodated. 
Basically, blocking provides for the reading and writing of fixed-length blocks. The length of a block is a function of the device. It may be one track, one-half track or other integral division of a track (Lut never more than one track). Because of the relatively large time to access a given position on a track (due to the rotational speed of the device and/or mechanical movement of the head to the track), a block size equal to one full track is the most desirable. However, limitations in the amount of storage available to hold the blocks in core is a second consideration. 
1.6-4

NASTRANINPUT/OUTPUT 
Since logical record lengths are variable but the length of records physically read or written is fixed, logic must be provided to accommodate this situation. This logic is provided in the GIN_ routine, which allows for the following cases: 
I. Multiple logical records per block 
2. Multiple blocks per logical record 
The method by which physical input and output of blocks is accomplished by GIN_ is machine dependent. On the IBM 7094, I_EX is used. On the IBM S/360, F_RTRANbinary read/write statements are used. On the Univac 1108, NTRAN is used. On the CDC 6600, SC_PE macros are used. These implementation differences are transparent to the NASTRANapplications programmer (functional module writer). The systems programmer who is interested in implementation details on the various machines is referred to section 5. 
1.6.4.1 GIN_ File Names 
The names of files input as arguments to the GIN_ routines listed above may be alphabetic (BCD, of the form 4HXXXX ) or integer. 
A GIN_ file name is BCD if the file contains permanent Executive tables or data blocks. A list of these files for a particular NASTRANrun resides in the permanent portion of the FIST Executive table. The following list presents all current Executive files with their BCD file names: 
File BCD File Name 
Data Pool File Pe_L 
New Problem Tape NPTP 
Old Problem Tape _PTP 
BCD Plot Tape PLTI 
Binary Plot Tape PLT2 
User's Master File UMF 
New User's Master File NUMF 
User Input File INPT. 
1.6-5
NASTRANPROGRAMMING FUNDAMENTALS 
Functional modules should not access thesE:permanent Executive files. Functional modules access the files on which their input, output and scratch data blocks reside by internal integer GIN_ file names. Prior to calling a functional module, the link driver routine, XSEMi, calls subroutine GNFIST (GNFIST is called exclusively by XSEMi) to generate the FIST Executive table. For each input, output or scratch data block required for operation of a module (this information being contained in the _SCAR entry), GNFIS1 searches the FIAT to find the data block. If the data block is in the FIAT and a file has been assigned to it, an internal GIN_ file number denoting the 
data block and a pointer (index) to the entry in the FIAT is placed in the FIST. The following convention is used for internal GIN_ file numbers: input data blocks -- lO0 + position in the _SCAR entry; output data blocks -- 200 + position in the _SCAR entry; scratch data blocks -- 301 through 300 + n where n = number of scratch data blocks as defined in the MPL. (The position in the _SCAR entry is the position in the DMAP instruction). If the data block is in the FIAT and is purged, no entry is placed in the FIST. For example, consider the following DMAP calling sequence for functional module XYZ: 
XYZ A,B,C/D,E,F,G/V,N,PARMI/V,N,PARM2 $ 
The data blocks input to the module are A, B and C; the data blocks output from tile module are D, E, F and G; the module's parameters are PARMI and PARM2. Note that internal scratch files are not mentioned in the DMAP calling sequence. The number of scratch files for a module is defined in the Module Property List (MPL) Executive table (see section 2.4) and is communicated to the Executive System via the OSCAR. Details on the syntactical rules of DMAPare given in section 5 of the User's Manual. 
In order to read the input data block B, the GINO file number internal to XYZ is 102; in order to write data block D, the GINO file number is 201. The third of, say, five scratch data blocks is referenced by XYZ through the GINO file number 303. 
l.6-6
NASTRAN MATRIXROUTINES 
1.7 NASTRANt._TRIXROUTINES 
1.7.1 Introduction 
The requirement that NASTRAN handle large structural analysis problems implies that NASTRAN should be able to manipulate and store large matrices efficiently and effectively. In general, the matrices generated in the displacement approach tend to be sparse (i.e., the number of non zero terms in any column of a matrix is small compared to the order of the matrix). The NASTRAN matrix routines, ADD, MPYAD, DECAMP, etc., which are described in section 3.5, are optimized as much as possible to take advantage of matrix sparsity and thus eliminate many unnecessary operation on zero elements. In order to aid in these operations and to make effective use of auxiliary storage, a packing scheme was devised to store only the non-zero terms in a column. 
1.7.2 Matrix Packin_ and Unpacking 
The need for a matrix packing routine can be seen by computing the auxiliary storage required to hold a lO,O00 order n_trix which is I% dense (i.e., the average nunlberof non-zero terms in a column is I00). With no packing technique, lO8 words of storage are required to hold the matrix. Using the NASTRAN packing routines, a maximum of 2 x lO6 words of storage are required if the terms are scattered, and lO6 words are required if the terms occur in a band. 
The subroutines BLDPK, INTPK, PACK, and UNPACK, along with their additional entry points, provide the matrix packing/unpacking capability of NASTRAi_. The user should refer to the des criptions of these subroutines in sections 3.5.1 through 3.5.4 for a detailed description of the packing logic. 
14atrices are stored by columns, and subroutines PACK/UIIPACKprovide the ability to pack/ unpack a complete column. The capability is also provided to pack/unpack a column from the first non-zero element to the last. 
An added feature of the packing routines is that subroutines BLDPK and INTPK provide the capability of packing/unpacking one element at a time. By use of INTPK, a matrix can be read element-by-element, such that an entire matrix can be processed without any appreciable core storage requirements. Likewise, by using BLDPK, a matrix can be built one element at a time. This is an extremely important feature to routines that must process matrices when storage is limited. 
1.7-I (12-I-69)
NASTRAN PROGRAMMING FUNDAMENTALS 
1.7.3 The Nested Vector Set Concept Used to Represent Components of Displacement 
In constructing the matrices used in the Displacement Approach, each row and/or column of a matrix is associated closely with a grid point, a scalar point or an extra point. Every grid point has 6 degrees of freedom associated with it, and hence 6 rows and/or columns of the matrix. Scalar and extra points only have one degree of freedom. At each point (grid, scalar, extra) these degrees of freedom can be further classified into subsets, depending on the constraints or handling required for particular degrees of freedom. (For example in a two-dimensional problem all "z" degrees of freedom are constrained and hence belongs to the s (single-point constraint) set). Each degree of freedom can be considered as a "point", and the entire model is the collection of these one-dimensional points. 
Nearly all of the matrix operations in displacement analysis are concerned with partitioning, merging, and transforming matrix arrays from one subset of displacement components to another. All the components of displacement of a given type (such as all points constrained by single-point constraints) form a vector set that is distinguished by a subscript from other sets. A given component of displacement can belor_g to several vector sets. The mutually exclusive vector sets, the sum of whose members are the set of all physical components of displacements, are as follows: 
um points eliminated by multipoint constraints, 
us points eliminated by single-point constraints, 
uo points omitted by structural matrix partitior;ing, 
u r points to which determinate reactions are applied in static analysis, 
the remaining structural points used in static analysis (points left over), u_ 
U eextra degrees of freedom intFoduced in dynamic analysis to describe control systems etc. The vector sets obtained by combining two or more of the above sets are (+ sign indicates the union of two sets): 
u a = ur + uL, the set used in real eigenvalue analysis, 
u d = u a + Ue, the set used in dynamic analysis by the direct method, 
uf = ua + uo, unconstrained (free) structural points, 
un = uf + us , all structural points not constrained by multipoint constraints, Ug = un + um, all structural (rgz_i_d) points including scalar points, 
1.7-2
NASTRANMATRIX ROUTINES 
Up = Ug + ue, all physical points. 
In dynamic analysis, additional vector sets are obtained by a modal transformation derived from real eigenvalue analysis of the set ua. These are: 
_o rigid body (zero frequency) modal coordinates, 
_f finite frequency modal coordinates, 
_i : _o + _f' the set of all modal coordinates. 
One vector set is defined that combines physical and modal coordinates. That set is Uh = _i + Ue' the set used in dynamic analysis by the modal method. 
The nesting of vector sets is depicted by the following diagram: 
us 
u o 

u r 
u_ ud u e 
_o 
Ci 
_f 
u a uh 
uf 
Un I Ug 
Up 

The data block USET (USETD in dynamics) is central to this set classification. Each word of USET corresponds to a degree of freedom in the problem. Each set is assigned a bit in the word. If a degree of freedom belongs to a given set, the corresponding bit is on. Every degree of free dom can then be classified by analysis of USET. The common block /BITP_S/ relates the sets to bit numbers. 
1.7-3
NASTRAN PROGRAMMING FUNDAMENTALS 

Two types of operations occur repeatedly. Examples are: 
and 
The first is the partitioning or sort operation. Unl(1) . 

JKnn ] =_ jI_i Kssj (2) 
The second is the recombining (or merge) operation: 
These operations can be completely described by a "partitioning" vector whose length corresponds 
to tile length of the major set (the Ug set in EQuation I) and whose elements are zeros or ones depending on whether a degree of freedom belongs to the upper (the u n set in Equation I) subset or the lower (the u m set in Equation I) subset. Such a partitioning vector can be constructed by subroutine CALCV, which is described in section 3.5.5. This operation is described throughout 
the documentation by the notation USET (UG,UN,UM) where UG (Ug) is the major set, UN (u n) is the zero set, and UM (u m) is the one set. The partitioning vector generated by subroutine CALCV is input to the matrix routine PARTN (section 3.5.6) to perform operations similar to those in Equations 1 and 2 and is input to the matrix routine MERGE (section 3.5.6) to perform operations similar to that in Equation 3. 
1.7.4 Processing of Matrices 
Matrices in NASTRAN can be divided in two general types: core held matrices such as the ;x6's generated by the element routines and data block held matrices such as those output by functional modules. There are many routines to assist the programmer in the processing of both types of matrices. Incore matrices can be processed by GMMATD (Section 3.4.32), GMMATS (Section 3.4.33), INVERD (Section 3.4.34) and INVERS (Section 3.4.35). Data block held matrices can be processed at several levels. The most general is through the matrix packing and unpacking 
1.7-4 (8/I/72)
NASTRAN MATRIXROUTINES 
routines(BLDPK, PACK,INTPKandUNPACK). Thenextlevel of generalityis providedby thematrix subroutinessuchasADD,PARTN, MERGE, TRNSP, MPYAD, SDC_MP, DECAMP, CDC_MP, FBS,GFBS,andINVTR. Thefunctionsprovidedbytheseroutinescanalsobeactivatedby a simplesubroutinecall through suchroutinesasSSG2A, SDRIB,SSG2C, SSG2B, SSG3A, S_LVER, FACTORandTRANPI.This third formis by far the mostconvenientanderror free methodfor the noviceNASTRAN applicationsprogrammer. 
1.7-5(8/I/72)
GENERATIONOF MATRICES 
1.8 GENERATION OF MATRICES 
The Structural Matrix Assembler (SMA) modules generate the stiffness, structural damping, mass and damping matrices for the structural model. SMAI generates the stiffness matrix exclusive of general elements, [Kxgg], and the structural damping matrix, [K_g]; SMA2 generates the mass matrix, [Mgg], and the damping matrix, [Bgg]; and SMA3 generates the final stiffness matrix, 
[Kgg], by generating a matrix for each general element in the model, and successively adding these matrices to FKx 1 Other matrix generation modules are: l) DS_IGI which generates the gg-. 
Kd 
differential stiffness matrix, [ gg], for use in the Static Analysis with Differential Stiffness Rigid Format and in the Buckling Analysis Rigid Format; 2) PLAI, which generates the stiffness 
KL 
matrix for linear elements, [ gg], for use in the Piecewise Linear Analysis Rigid Format; 3) rKn_l 
PLA4, which generates the stiffness matrix for nonlinear elements, L ggJ, for use in the Piecewise Linear Analysis Rigid Format; 4) MTRXIN, which provides a two-fold capability: a) to provide for direct input matrices such as control systems in the dynamics Rigid Formats, and b) to provide the DMAPuser a capability of converting matrices input on DM!G bulk data cards to NASTR_N matrix format; and 5) the IFP module which provides the user the capability of converting matrices input on DMI bulk data cards to NASTRANmatrix format. Detailed information on each of these modules can be found in section 4, Module Functional Descriptions. The central role that the ECPT data block plays in the formation of the structural matrices generated in modules SIIAI, SMA2, DSHGI, PLA! and PLA4 is explained in the following subsections. 
1.8.1 The ECPT Data Block 
NASTRAN embodies a lumped element approach, i.e., the distributed physical properties of a structure are represented by a model consisting of a finite number of idealized substructures or elements that are interconnected at a finite number of points. An element will affect terms in the matrices only in rows and columns related to its interconnected points. Hence each column of these matrices may be formed using only elements connected to the grid or scalar point associated with that column. 
The Table Assembler (TAI) module constructs the Element Connection and Properties Table (ECPT) data block for use in the generation of these structural matrices. Each record of the ECPT corresponds to a grid point or a scalar point of the model, and, conversely, every grid point or scalar point of the model corresponds to a record of the ECPT. The point to which a 
1.8-I
NASTRAN PROGRAMMING FUNDAMENTALS 
record of the ECPT corresponds is called the pivot point of the record. Each record contains the connection and properties data for all elements connected to the pivot point. Hence data for an element will appear n times, where n is the number of points defining the element. 
1.8.2 Structural Elements 
The basis for the structural matrices in NASTRAN are the finit_ structural and scalar elements. Each element generates matrix terms connecting and connected to the grid and scalar points given on its input connection card (e.g., CR_D). A structural element generates 6 by 6 matrix parti tions related to the six degrees of freedom of each connecting grid point. A scalar element generates one term for each connection. 
The stiffness matrix, [K], for a structural element consists of a 6 by 6 partition for each combination of the connected grid points. For example, a BAR or R_D element is connected to two grid points, "a" and "b". The stiffness matrix partitions are: [Kaa], [Kab], [Kba] and [Kbb]. A triangular element (e.g., TRMEM) is connected to three points. It will generate nine partitions: [Kaa], [Kab], [Kac], [Kba], [Kbb], [Kbc], [Kca], [Kcb] and [Kcc]. 
Although the actual equations for the element stiffness, mass and damping matrices are different for each element, the solutions follow a definite pattern. The element connection, orientation and property data are given in the ECPT data block. The coordinate system data for orienting the global coordinates at each grid point are given in the CSTM data block. The material properties are given in the MPT and DIT data blocks. A utility routine, PRETRD, is available to fetch coordinate system data, and a utility routine, PREMAT, is available to fetch material properties. 
I. An element coordinate system is calculated using the locations of the grid points. Using these data a matrix, [E], is formed, which transforms displacements from element coordinates to basic coordinates. 
2. The stiffness matrix may be formed in element coordinates using many methods. For the simple elements (e.g., R_D) the terms are direct functions of the geometry, properties and material coefficients of the element. For some elements the matrix is first formulated in terms of generalized coordinates, {q}, usually the coefficients of a power series. In 
general coordinates, the matrix is [Kq]. Transformation matrices, [Hi] , are generated to 1.8-2
GENERATION OF MATRICES 
transform the displacements at the grid points in element coordinates {u}, to the general coordinates {q}. 
3. The global coordinate system orientation matrix, [T], for each grid point is calculated. 4. The stiffness matrix partition for the columns related to point j and the rows related to point i is [Kij]. In general it is formed by the equation 
[Kij] = [Ti]T[E][Hi]T[Kq][Hj][E]T[Tj]. (I) 
In order to generate a particular partition, [Kij], it is often necessary to generate [K]. Only those partitions [Kij], where i is the pivot point and j = 1,2.....n (n being the number of grid points associated with the element), are useful for the current ECPT record being processed. The unused partitions are recalculated and used when j _ i appears as a pivot point in a sub sequent ECPT record. An alternate procedure for matrix generation, which is not used, would be to calculate all of the elementmatrices once and store them on an auxiliary file for future use ,.,h..... _ _- alternate procedure is i_ss efficient for large problems, where efficiency really counts, because the recalculation time is less than the time required to recover element matrices from the auxiliary file. 
1.8-3

TERMINATION PHILOSOPHY ANDDIAGNOSTIC MESSAGES 
1.9 TERMINATION PHILOSOPHY ANDDIAGNOSTIC MESSAGES 
Certainrestrictions areplaceduponthe functionalmodulewriter with regardto run terminationanderror diagnostics. This is necessaryin orderto completecertain functions uponterminatingandto maintainuniformitywith regardto diagnosticmessages. 
A functionalmodulewriter is requiredto utilize a messagewriter (MSGWRT, section3.4.26) to print all of his messages.In this mannersimilar message formats do not have to be dunlicated in each module. Also, in order to avoid placing the I/0 conversion routines and the lengthy format statements in the root segment, the message writer is restricted to its own overlay segment, Communication between the module and the message writer is via a queued message concept. Subroutine MESAGE (section 3.4.25) is called to store the message parameters. In the case of a fatal message, a dump is taken if a DIAG l card is present in the Executive Control Deck, and PEXIT (section 3.4.22) is called. For non-fatal messages, the message is queued and control given back to the user. The message queue is printed after each module is executed. 
,,,u_uer for any routine to terminate the current execution, a call to PEXIT must be made. PEXIT handles all the functionsmecessary to wrap up the run: flushing output buffers, printing queued messages, and punching the last card of the checkpoint dictionary. 
1.9-I

P_STARTS IN NASTRAN 
I.I0 RESTARTS IN NASTRAN 
NASTRAN is designed to run large problems with long running times. Even with the best of computer systems, a hardware, operator, or system failure is not uncommon for long running jobs. At the same time, the large volumes of data and the complexity of the structures that can be modeled and analyzed using NASTRAN make it highly likely that user input data errors will occur. Many of these errors are of a subtle type, meaning that they cannot be immediately detected in the NASTRAN Preface by the modules which process the data decks. To deal with these problems, and to save machine time on runs which abort because of data or system errors, NASTRAN has a sophisti cated checkpoint and restart capability (see section 3 of the User's Manual for a discussion of restarts from the user point of view). The overall design philosophy for restart is twofold. A restart selectively executes only the modules necessary to accomplish a user-input data change. The user is able to change any part of his problem including structural model changes, additional cases, or more output requests. At the same time restarts are automatic as far as user interference is concerned. The user need only checkpoint (see section 1.2.3.5) his original run and submit changes to the original run on subsequent runs. The user does not have to analyze the effect of his changes. In addition the selective nature of restart allows the program to proceed with implicit errors (errors present in the data but not yet identified) until no further valid progress can be made. The work accomplished to this point is not lost, but rather only the table or matrix data block in error must be corrected to allow the program to proceed. Much error checking can be deferred until the actual module using the data is in control. The remainder of this section will explain the program mechanics by which restart is accomplished. 
In NASTRAN there are four general types of restarts. Unmodified Restart (UMR), Psuedo Modified Restart (PMR), Modified Restart (MR), and Rigid Format Switch (RFS). Note that in the User's Manual UMR's and PMR's are described together as Unmodifed Restarts. These classifications are for des criptive and internal purposes. The user need not know anything about which type is which. The basic characteristics of each type will be described below. An Unmodified Restart results when the user simply resubmits a problem with no data changes. It is used to continue a solution from the point of interruption. Presumably the problem aborted previously due to time expiring, machine error, system error, etc. The restart dictionary (created while checkpointing) is processed, and the solution is started again at the last re-entry point (after the last successful checkpoint). A Psuedo Modified Restart occurs when the user requests additional output from the program which simply requires the re-execution of an output module such as the Structure Plotter, the Grid Point 
1.10-I
