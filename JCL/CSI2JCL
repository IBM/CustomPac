//CSI2JSON JOB (USERID),
//             'CSI2JSON',
//             USER=,                                         /*RACF*/
//             GROUP=,                                        /*RACF*/
//             PASSWORD=,                                     /*RACF*/
//             NOTIFY=&SYSUID,
//             CLASS=A,
//             MSGCLASS=A,
//             MSGLEVEL=(1,1),
//             REGION=0M
//********************************************************************/
//* COPYRIGHT 2022 IBM CORP.                                         */
//*                                                                  */
//* LICENSED UNDER THE APACHE LICENSE, VERSION 2.0 (THE "LICENSE");  */
//* YOU MAY NOT USE THIS FILE EXCEPT IN COMPLIANCE WITH THE LICENSE. */
//* YOU MAY OBTAIN A COPY OF THE LICENSE AT                          */
//*                                                                  */
//* HTTP://WWW.APACHE.ORG/LICENSES/LICENSE-2.0                       */
//*                                                                  */
//* UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN WRITING,       */
//* SOFTWARE DISTRIBUTED UNDER THE LICENSE IS DISTRIBUTED ON AN      */
//* "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,     */
//* EITHER EXPRESS OR IMPLIED. SEE THE LICENSE FOR THE SPECIFIC      */
//* LANGUAGE GOVERNING PERMISSIONS AND LIMITATIONS UNDER THE LICENSE.*/
//*                                                                  */
//********************************************************************/
//*                             CSI2JSON                             */
//********************************************************************/
//*                                                                  */
//* READS THE CONTENT OF SUPPLIED CSI VSAM DATASET AND EXPORTS SMP/E */
//* ENTRIES INTO THE JSON FILE WHICH IS COMPATIBLE WITH THE IBM      */
//* PROACTIVE MAINTENANCE SERVICE PORTAL.                            */
//*                                                                  */
//* SCRIPT ALLOCATES TEMPOPARY WORKING DATASETS UNDER THE            */
//* %USERID%.CSI2JSON HLQ AND SCRATCHES THEM AFTER THE PROCESSING.   */
//*                                                                  */
//* CONTROL CARDS FOLLOW:                                            */
//*                                                                  */
//*          JSON_DSN=DATASET_NAME                                   */
//*            ---------------------                                 */
//*            JSON DATASET IS ALLOCATED UNDER THE FOLLOWING HLQ:    */
//*              %USERID%.CSI2JSON.JSON (DEFAULT)                    */
//*            IT IS POSSIBLE TO CHANGE THE JSON DATASET NAME BY     */
//*            SPECIFYING THIS SCRIPT ARGUMENT                       */
//*                                                                  */
//*          DELETE_EXISTING_DSN=[YES | NO]                          */
//*            -------------------------------                       */
//*            CSI2JSON DOES NOT SCRATCH ANY EXISTED JSON OR         */
//*            TEMPORARY WORKING DATASETS. IT MIGHT HAPPEN THAT USER */
//*            HAD ALREADY RUN THE SCRIPT AGAINST THE SAME CSI VSAM  */
//*            WHERE THE JSON/WORKING DATASETS IS ALREADY EXISTED ON */
//*            THE DASD. THE SCRIPT WILL STOP IN THIS CASE WITH      */
//*            RETURN CODE > 0. THE SITUATION CAN BE EASILY          */
//*            ELIMINATED BY SPECIFYING  DELETE_EXISTING_DSN=YES     */
//*            WHICH FORCES CSI2JSON TO DELETE EXISTING JSON/WORKING */
//*            BEFORE PROCESSING.                                    */
//*                                                                  */
//*                                                                  */
//*          KEEP_TEMPORARY_DSN=[YES | NO]                           */
//*          -----------------------------                           */
//*            IT MIGHT BE USEFUL TO KEEP TEMPORAL WORKING DATASETS  */
//*            ON DASD WHICH CAN BE DONE BY CODING THIS ARGUMENT.    */
//*            EXAMPLE: KEEP_TEMPORARY_DSN=YES                       */
//*                                                                  */
//*          MAX_LIST_RC=NN                                          */
//*            ----------------                                      */
//*            USER CAN BYPASS A RETURN CODE GREATE THAN 0 BY        */
//*            THIS PARAMETER                                        */
//*            SOMTIMES THE SMP/E LIST UTILITY WILL RESULT IN A      */
//*            RETURN CODE GREATER THAN 0 BUT CAN BE SAFELY BYPASSED.*/
//*            THE PARAMETER ABOVE WILL PERMIT THE USER TO ENTER     */
//*            THE MAX RETURN CODE THEY WULL ACCEPY BY REPLACING THE */
//*            NN WITH A NUMERIC VALUE.                              */
//*            EXAMPLE:  MAX_LIST_RC=04                              */
//*                                                                  */
//*                                                                  */
//*          TRACE=[ON | OFF]                                        */
//*            -----------------                                     */
//*            USER CAN ALWAYS REQUEST THE SCRIPT TRACING BY SETTING */
//*            ARGUMENT. PLEASE TAKE NOTE THAT ENABLING THE TRACE    */
//*            WILL GENERATE A LOT OF OUTPUT AND REQUIRES SIGNIFICANT*/
//*            AMOUNT OF DASD SPACE FOR THE SYSTSPRT DATASET IF THE  */
//*            SCRIPT IS RUN IN BATCH MODE.                          */
//*                                                                  */
//*KNOWN ISSUES:                                                     */
//*                                                                  */
//* ISSUE    : THE FOLLOWING ERROR MESSAGE APPEARS IN THE SCRIPT     */
//*            OUTPUT:                                               */
//*                                                                  */
//*                                                                  */
//* ERROR: RETURN CODE 16 WHILE RUNNING GIMSMP APPLICATION.          */
//*        PROCESSING TERMINATED.                                    */
//*        REVIEW SMP/E LOG DATASET FOR MORE INFORMATION.            */
//*        CSI2JSON IS EXITING DUE TO ERROR.                         */
//*                                                                  */
//* CAUSE    : SMP/E GIMSMP APPLICATION FAILED WITH SPECIFIED RETURN */
//*            CODE.                                                 */
//*                                                                  */
//* SOLUTION : CHECK %USERID%.CSI2JSON.SMP* DATASETS FOR THE ERROR   */
//*            MESSAGE DESCRIPTION.                                  */
//*                                                                  */
//*                                                                  */
//*                                                                  */
//*INPUT PARAMETERS:                                                 */
//*                                                                  */
//*  NONE.                                                           */
//*                                                                  */
//*OUTPUT     :                                                      */
//*                                                                  */
//* RETURN CODE       MESSAGE                                        */
//*  -----------      ---------------------------------------------  */
//*            0      COMPLETE SUCCESSFUL                            */
//*          > 0      FAILURE, SEE TSO CONSOLE OR SYSTSPRT DATASET   */
//*                   FOR MORE INFO.                                 */
//*                   REVIEW SMP/E LOG DATASETS FOR MORE INFORMATION.*/
//*                                                                  */
//*                                                                  */
//********************************************************************/
//RUNPROG  EXEC PGM=IKJEFT01,DYNAMNBR=20
//SYSEXEC  DD DISP=SHR,DSN=%CSI2REXX_DATASET_NAME%
//SYSTSPRT DD SYSOUT=*
//*SYSTSPRT DD DSN=%SYSTSPRT_DATADSET_NAME%,
//*            DISP=(NEW,CATLG),
//*            SPACE=(CYL,(10,10),RLSE),
//*            RECFM=VB,LRECL=240,BLKSIZE=24000,UNIT=3390
//SYSTSIN  DD *
  CSI2JSON %CSI_VSAM_DATASET%                     -
           DELETE_EXISTING_DSN=[YES | NO]         -
           KEEP_TEMPORARY_DSN=[YES | NO]          -
           MAX_LIST_RC=04                         -
           JSON_DSN=%JSON_DATASET_NAME%
  CSI2JSON %CSI_VSAM_DATASET%                     -
           DELETE_EXISTING_DSN=[YES | NO]         -
           KEEP_TEMPORARY_DSN=[YES | NO]          -
           JSON_DSN=%JSON_DATASET_NAME%
/*
