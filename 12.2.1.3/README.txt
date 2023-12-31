Oracle� WLS Patch Set Update 12.2.1.3.230402 README 


Patch Set Update (PSU) for Bug : 35247514


Date : 02-Apr-23

 Platform Patch for : Generic Platform

 Product Patched : Oracle WebLogic Server

 Product Version : 12.2.1.3.0


This document describes how to install patch # 35247514.


It includes the following sections:


     - Section 1: Zero Downtime Patching 


     - Section 2: Prerequisites 


     - Section 3: Pre-Installation Instructions 


     - Section 4: Installation Instructions 


     - Section 5: Post-Installation Instructions 


     - Section 6: Deinstallation Instructions 


     - Section 7: Post Deinstallation Instructions 


     - Section 8: Bugs Fixed by This Patch 


Section 1: Zero Downtime Patching
------------------------------------------
 This patch has been marked as eligible for Zero Downtime Patching.

 The type of Zero Downtime Patching supported by this patch is FMW_ROLLING_ORACLE_HOME.


With Zero Downtime Patching, a Patch can be applied to a system in a manner that does not incur any downtime.


This ensures that the system can remain available and functioning during the patching process.


Certain pre-requisites, however, must be met before the patch can be applied.


For more information, see the following:

 Doc ID 1942159.1 Introduction to Zero Downtime (ZDT) Patching for Oracle Fusion Middleware / WebLogic Server

 https://support.oracle.com/epmos/faces/DocumentDisplay?id=1942159.1


Section 2: Prerequisites
------------------------------------


Ensure that you meet the following requirements before you install or deinstall the patch:


1. Understand the PSU program:


Review the following before applying PSUs for the first time:


Doc ID 1306505.1 Patch Set Update (PSU) Administration Guide for Oracle WebLogic Server (WLS)

 https://support.oracle.com/rs?type=doc&id=1306505.1


2. Update Java SE (JDK/JRE):


In order to maintain security, users of Oracle JDKs and JVMs, we strongly recommend applying the latest


Java Critical Patch Updates (CPUs) as soon as they are released.


Doc ID 2917310.1 Oracle Critical Patch Update (CPU) January 2023 for Oracle Java SE


https://support.oracle.com/epmos/faces/DocumentDisplay?id=2917310.1


Refer to the following for further information:

 Doc ID 1506916.1 Obtaining Java SE (JDK/JRE) for Oracle Fusion Middleware Products

 https://support.oracle.com/rs?type=doc&id=1506916.1


Certain fixes in this WebLogic Server Patch Set Update for deserialization vulnerabilities depend on JEP 290 filtering

 and JEP 290 global scope filtering features provided in July 2018 JDK Updates and later JDK updates.

 These fixes for deserialization vulnerabilities are not effective without these JDK updates.

 Users applying this Patch Set Update without these JDK updates will receive warnings in the WebLogic Server console

 and in WebLogic Server logs. Refer to the following document for details. 


Doc ID 2421487.1 Restricting Incoming Serialized Java Objects to Oracle WebLogic Server


https://support.oracle.com/rs?type=doc&id=2421487.1


3. Update OPatch:


The ORACLE_HOME should be installed with OPatch version 13.9.4.2.11 or higher.


The latest OPatch version can be obtained from the following link:

 https://support.oracle.com/rs?type=patch&id=28186730


To verify the OPatch version, run the following command: 


<ORACLE_HOME>/OPatch/opatch version


To upgrade OPatch, follow the below steps:


Refer to this OPatch README.txt for most up to date instructions on upgrading OPatch in the ORACLE_HOME.


4. Validate the OUI inventory with the following commands:


$ ORACLE_HOME/OPatch/opatch lsinventory 


Section 3: Pre-Installation Instructions
------------------------------------------------


1. Stop all WebLogic servers (AdminServer and all Managed server(s)). 


2. Its recommended to create a complete backup of DOMAIN_HOME, ORACLE_HOME and CENTRAL INVENTORY 

 Refer the following Backing Up Your Environment for Oracle recommended backup strategies.


3. AntiVirus software may need to be temporarily stopped, if installed before applying patches.

 Note: Only if if there are problems copying files during patching.


4. Ensure that the same user who installed WLS is used for applying patches via the OPatch tool.


5. Set the ORACLE_HOME environment variable to the directory where you have installed Oracle WebLogic Server.


Section 4: Installation Instructions
---------------------------------------------


1. Unzip p35247514_122130_Generic.zip into PATCH_TOP 


Notes: You must make sure that the target directory for unzip has required write and executable permissions for "user" with which the component being patched is installed.

 On some platforms, the zip/unzip utility may not be able to extract the jar files in the zip correctly.

 On Windows, the native zip utility will show a 'path too long' error. Java provides the jar utility which will avoid this problem, e.g., jar -xvf p35247514_122130_Generic.zip.


2. Set your current directory to the directory where the patch is located.


$ cd PATCH_TOP/35247514


3. Run OPatch to apply the patch.


$ opatch apply


Microsoft Windows:

 When applying patches for Microsoft Windows platform


<ORACLE_HOME>\OPatch\opatch.bat apply PATCH_TOP/35247514


Note:

 -----

 When OPatch starts, it validates the patch and makes sure that there are no

 conflicts with the software already installed in the ORACLE_HOME.


In case of opatch conflict, you will see a warning message similar to the one mentioned below:


Interim Patch XXXX has Conflict with patch(es) [ YYYY ] in OH ...

 Conflict patches: YYYY

 Patch(es) YYYY conflict with the patch currently being installed (XXXX).

 If you continue, patch(es) YYYY will be rolled back and the new patch (XXXX) will be installed.


If a merge of the new patch (XXXX) and the conflicting patch(es) ( YYYY) is required, contact Oracle Support Services and request a Merged patch.


Do you want to proceed? [y|n]

 n


You must stop the patch installation and the following should be reviewed:


Doc ID 1329952.1 Oracle Fusion Middleware Patch Conflict Resolution

 https://support.oracle.com/rs?type=doc&id=1329952.1


Contact Oracle Support if the conflict cannot be resolved or you need a Merge Request.


Section 5: Post-Installation Instructions
------------------------------------------------


1. Verify the WebLogic Server PSU patch is in the ORACLE_HOME inventory: 


<ORACLE_HOME>/OPatch/opatch lspatches


or


Login to console -> monitoring tab and confirm that the patch is applied successfully.


Refer Obtaining a List of Applied Patches


2. Refer to the following document for any further Post-Install advice:


Doc ID 2764668.1 Security Advice and Post-Install Information for Oracle WebLogic Server PSUs

 https://support.oracle.com/rs?type=doc&id=2764668.1


3. Start all Weblogic Servers.


Section 6: Deinstallation Instructions
-----------------------------------------------


If you experience any problems after installing this patch, remove the patch as follows:
 
 1. Make sure to follow the same Prerequisites or pre-install steps (if any) when deinstalling a patch.
 This includes setting up any environment variables like ORACLE_HOME and verifying the OUI inventory before deinstalling.
 
 2. Change to the directory where the patch was unzipped.
 
 $ cd PATCH_TOP/35247514
 
 3. Run OPatch to deinstall the patch.
 
 $ opatch rollback -id 35247514
 
Note: If you roll back a PSU after October 2022 to January 2023, a warning message
 will appear that the rollback is unable to restore a doc directory. This is expected behavior and can be
 safely ignored.


Section 7: Post Deinstallation Instructions
--------------------------------------------------
 Restart all servers (AdminServer and all Managed server(s)).


This is necessary to redeploy the original applications and bring the environment back to it's original state. 
NOTE: A PSU fix may add support for new configuration attributes for the new console security warnings feature. In normal cases if you roll back the PSU there would be no issues. If you specify a non-default value for these new attributes and activate the change, then it is persisted to config.xml. If you subsequently roll back the PSU to a prior version that has not supported these values, then WebLogic Server will not boot due to the presence of the new configuration attribute in config.xml. If you have configured non-default values for the console security warnings, then you must revert these changes to their default values before rolling back the PSU.
 
 For more information about the console security warnings, see the following:
 
- Security Warnings Report - Version 12.2.1.3
 
 - WebLogic Server Security Warnings Displayed Through the Admin Console (Doc ID 2788605.1)


Section 8: Bugs Fixed by This Patch
--------------------------------------------


Bug fixes in this patch are shown in the following list: 
 Issues Resolved in WLS Patch Set Update 12.2.1.3.230402
    35219161 : Fix for Bug 35219161
    35170938 : CVE-2023-24998
    35170849 : CVE-2023-24998
    35136876 : Fix for Bug 35136876
    35118583 : CVE-2023-24998
    35039991 : CVE-2023-21979
    35038260 : CVE-2023-21996
    34992651 : JAN PSU IS MISSING WLST OFFLINE VERSIONS OF NEW WLST ONLINE ATTRIBUTES
    34945769 : CVE-2022-45685
    34918591 : CVE-2021-23926
    34881912 : CVE-2023-21960
    34858275 : CVE-2023-21964
    34817386 : CVE-2020-6950
    34806277 : Fix for Bug 34806277
    34805433 : Fix for Bug 34805433
    34779739 : CVE-2021-23926
    34520786 : CVE-2023-21931
    33287555 : CVE-2021-29425

 Issues Resolved in WLS Patch Set Update 12.2.1.3.221210
    34791059 : CVE-2022-42920
    34778989 : CVE-2022-40153
    34677232 : SECURITY WARNING NO COHERENCE CPU PATCH IS APPLIED TO THE ORACLE HOME
    34647286 : CVE-2022-40150
    34522036 : CVE-2023-21842
    34515267 : Fix for Bug 34515267
    34494177 : Fix for Bug 34494177
    34489481 : CVE-2023-21841
    34470569 : Fix for Bug 34470569
    34469121 : CVE-2018-7489
    34465980 : CVE-2023-21839
    34373063 : CVE-2023-21838
    34315592 : CVE-2023-21837

 Issues Resolved in WLS Patch Set Update 12.2.1.3.221013
    34513377 : TRACKING BUG TO REVERT THE PRINT PATCH LIST IN SERVER LOG FILE FOR THE PSU
    34469162 : CVE-2020-17521
    34469147 : CVE-2020-28052
    34469106 : CVE-2020-8908
    34469090 : CVE-2022-23437
    34429695 : OCT CPU - LOG4J JARS DELETION
    34394700 : Fix for Bug 34394700
    34362971 : CVE-2022-22971
    34361462 : Fix for Bug 34361462
    34339878 : WLS PSU DOESN'T PATCH ORACLE.OWASP/COM-BEA-CORE-APACHE-LOG4J.JAR IN NON WLS HOMES
    34082912 : CVE-2022-21616
    34031093 : Fix for Bug 34031093
    33019953 : WORKMANAGER IS UNABLE TO SCHEDULE ONCE GETSTUCKTHREADS GETS HUNG BY APPLICATION
    32937538 : CIE TRACKING BUG TO SUPPORT WLS FIX OF 32883876 IN OFFLINE MODE
    32560780 : IOEXCEPTION: CONNECTION CLOSED, EOF DETECTED; AFTER CONNECT FAILURE WITH INVALID PROTOCOL/PORT
    32228507 : PERFORMANCE DEGRADATION DUE TO METHOD SUBJECTCONVERTERFACTORY$1.GETIDDNAMEATTRIB
    30467554 : USE CONFIGURED CREDENTIALS W/ PROXY AUTH, REMOVE INTERNAL DRIVER PROP WEBLOGIC.JDBC.USECONFIGUREDCREDENTIALSASPROXYUSERDEFAULT
    29940841 : SECURITY PRINCIPAL DOES NOT GET SET WITH IIOP IN WLS 12.2.1.3
    29274025 : DEPLOYER ROLE - DATA SOURCE "CONTROL" TAB DOES NOT SHOW SHRINK, RESET, ETC...
    28967247 : SOA/BPM_NON-ZDT_UPG:Deployment "frevvo" failed after 11gPS7 to 19c Upgrade
    28105820 : REDEPLOYING DATASOURCE FROM WEBLOGIC CONSOLE FAILS WITH CLASSCASTEXCEPTION
    27804544 : JMS CONNECTION FACTORIES GETTING DEFAULT TARGETING AFTER UPGRADE TO 12.2.1.3
    27724050 : MULTIPLE EXECUTETHREADS DEVOTED TO ONE TX ABANDONMENT
    27062127 : JMS MESSAGES NOT HONORING REDELIVERY LIMIT SET ON THE QUEUE

 Issues Resolved in WLS Patch Set Update 12.2.1.3.220620
    34289705 : TRACKING BUG TO UPGRADE COMMONS FILEUPLOAD FOR WLS
    34197839 : CVE-2022-24839
    34185325 : CVE-2022-23457
    34181077 : WEBLOGIC.VERSION HANGS IF OPATCH UNABLE TO GET THE LOCK TO CENTRAL INVENTORY
    34172370 : CVE-2022-29577
    34166452 : CVE-2020-36518
    34132210 : CVE-2022-21564
    34102404 : CVE-2022-21560
    34096039 : CVE-2022-21557
    34092344 : UPGRADE LOG4J USED IN CONSOLE FROM V1 TO V2
    34069324 : REMOVAL OF LOG4J V1 JARS
    34055705 : CVE-2021-26291
    34044945 : CVE-2022-22965
    34026019 : Fix for Bug 34026019
    33964662 : CVE-2022-21548
    33895645 : Fix for Bug 33895645
    33825902 : Fix for Bug 33825902
    33767326 : <ERROR> <J2EE> <BEA-160248> <UNABLE TO PARSE CLASS FILE: FILE:/XXX/XXX.CLASS. >
    33676277 : CLIENT TO CLIENT ROUTING NOT ABLE TO RECONNECT WITH RJVM FORWARDING CHANGE
    33015183 : WLS1412 HTTP TUNNELING AND STAND-ALONE CLIENT SUPPORT IN RJVM FORWARDING
    32875564 : CVE-2020-11987
    32408938 : RJVM FORWARDING SUPPORT FOR WEBLOGIC KUBERNETES OPERATOR
    32230661 : WEBLOGIC CAT FAILED DUE TO CONFLICT WITH MODULE-INFO
    32153389 : ONLINE WLST CD FAILS WHEN OBJECT NAMES WITH SLASHES OVERLAP
    31483446 : :WLS THE JFR RECORDING __WLDF_DEBUG_EVENTS SHOULD START WITH BOUNDS ON SIZE
    30998532 : CLUSTERED EJB 2.X APP. IN WEBLOGIC 12.2.1.3 THROWS REMOTEEJBINVOKEEXCEPTION
    30874677 : OFFLINE WLST NOT ENCRYPTING CREDENTIAL AFTER UPDATEDOMAIN()
    30739376 : RESOURCE LEAK IN COM.ORACLE.WEBLOGIC.RJVM.JAR
    30543380 : TX ROLLBACK WITH ILLEGAL STATE (EXPECTED: PREPREPARED)
    29906301 : <BEA-320188> <LONG RID VALUE WITH XXXX COMPONENTS WAS CREATED.>
    28294508 : UNABLE TO VIEW MONITORING TAB IN 12.2.1.3.0
    27291550 : HOGGING THREAD IN WC_PORTAL MANAGED SERVER

 Issues Resolved in WLS Patch Set Update 12.2.1.3.220329
    33890487 : Fix for Bug 33890487
    33890469 : CVE-2020-28491
    33876615 : CVE-2022-23437
    33798087 : CVE-2021-41184
    33792809 : Fix for Bug 33792809
    33791665 : CVE-2022-23305
    33735326 : CVE-2021-44832
    33670829 : INCLUDE PATCH INFO IN WLS LOGS SAME AS BSU
    33666033 : Fix for Bug 33666033
    33617787 : CVE-2022-21453
    33613719 : Fix for Bug 33613719
    33580024 : WEBLOGIC CONSOLE SHOWS 090979 SECURITY WARNIN WHEN USING WINDOWS SERVICE.
    33562620 : Fix for Bug 33562620
    33560637 : Fix for Bug 33560637
    33422662 : CVE-2022-21441
    33235201 : UPDATE ANTISAMY (OWASP) TO VERSION 1.5.7
    32649503 : Fix for Bug 32649503
    31470145 : CVE-2020-10683
    29449188 : ADMIN CONSOLE TAKES ABOUT 2 MINUTES TO RESPOND WHEN CLICKING ON DEPLOYMENT
    27144719 : MQ CHANNEL ABENDED DUE TO INCORRECT OSB XA SEQUENCE
    27103380 : THE DEPLOYER ROLE CANNOT CREATE JMSSERVER BY JMX POLICY EDITOR
    26785585 : SHOULD NOT SET CONTENT-LENGTH HEADER FOR CHUNK CONTENT TYPE

 Issues Resolved in WLS Patch Set Update 12.2.1.3.211222
    33691226 : CVE-2021-45105
    33671996 : CVE-2021-45046
    33660731 : CVE-2021-44228
    33560373 : Fix for Bug 33560373
    33542139 : ADD MISSING REPORTED SECURITY WARNING INFORMATION LINK  TO ONLINE HELP.
    33446922 : CVE-2022-21371
    33380581 : PROVIDE ABILITY TO DISABLE WARNING FOR SAMPLES IN PRODUCTION MODE
    33379618 : CVE-2022-21386
    33355727 : CVE-2021-27568
    33349324 : CVE-2019-10219
    33329852 : Fix for Bug 33329852
    33328978 : PROVIDE ABILITY TO DISABLE WARNING FOR SAMPLES IN PRODUCTION MODE
    33293539 : CVE-2022-21353
    33287665 : CVE-2021-29425
    33277149 : CVE-2022-21350
    33270388 : Fix for Bug 33270388
    33270137 : Fix for Bug 33270137
    33261059 : CVE-2022-21347
    33145710 : CVE-2022-21306
    32118304 : FMW12C:20.07 OPC:PROVISIONED POD: BI_SERVERHA, ESSBASE_SERVER1, ESS_SOASERVER_1 ARE NOT COMING UP
    32077694 : CALENDARTIMER RETURN INCORRECT "NEXT TIMEOUT" TIME WHEN DST FALLBACK TO NORMAL
    31207149 : CVE-2020-2934
    30597194 : PSR:OIC:Diag - Admin server keep restarting every hour on oicphx1i242hd6087fic, oicfrk3i175h71ec98ic.

 Issues Resolved in WLS Patch Set Update 12.2.1.3.210929
    33245345 : CVE-2021-35620
    33207639 : CONSOLE SUPPORT FOR SECURITY CHECKING ONLINE HELP
    33171421 : CVE-2021-35617
    33170754 : CVE-2021-29425
    33166329 : JAVA PROPERTIES TO DISABLE ANONYMOUS REQUESTS STILL DISPLAY WARNING
    33164116 : CVE-2019-17195
    33152312 : KSS KEYSTORE FAILS TO LOAD AFTER JULY2021 PSU APPLICATION
    33114718 : CHECK FOR UNAUTHENTICATED DOT NET JMS CLIENT
    33063225 : WARNING MESSAGE TO BE FIXED FOR UNENCRYPTED PASSWORD USED IN COMMAND LINE IN UPCOMING PSU
    32976692 : REMOVE SYSTEM PROPERTY FOR DISABLING USE OF WRAPPER CLASS
    32962304 : ANONYMOUS .NET JMS CLIENT HUNG ON CREATING INITIAL CONTEXT TO A 14.1.2 SERVER
    32893667 : WLS PATCH 32697734 CAUSES ODI TO UNABLE TO LOGIN
    32593893 : CVE-2021-35552
    32519960 : CVE-2020-11022
    29200882 : Error processing the XML requests: Maximum attribute size limit exceeded in SOA
    27703270 : WEBSERVICES CLIENT NOT WORKING WITH TWO PARAMETERS
    25900775 : SECURE MODE V2 WARNINGS TO ADD TO SECURE MODE VALIDATION

 Issues Resolved in WLS Patch Set Update 12.2.1.3.210630
    32920991 : SUPPORT FOR SECURITY CHECKUP TOOL
    32883876 : ADD SECURITY CHECKUP TOOL
    32697451 : CVE-2021-2403
    32651810 : CVE-2021-2397
    32639821 : CVE-2021-2394
    32520971 : CVE-2021-2382
    32519937 : CVE-2020-11022
    32503912 : CVE-2021-2378
    32497814 : CVE-2021-2376
    32064362 : PROVIDE ABILITY TO DETECT EXPIRING CERTIFICATE AND ALERT CUSTOMER THRU CONSOLE AND LOG MESSAGE
    30965440 : HOGGING THREADS CAUSE MANAGED SERVER WARNING AND USERS NOT ABLE TO LOG INTO APP
    30912052 : DI: MESSAGE WHEN WEBSERVICEREF POINTS TO A NOT EXISTING HOST

 Issues Resolved in WLS Patch Set Update 12.2.1.3.210329
    32528774 : MISLEADING ERROR MESSAGE IN RECONFIGURATION WIZARD WITH DATASOURCE TEST CONNECTION.
    32425607 : CVE-2021-2136
    32415913 : CVE-2021-2135
    32373306 : CVE-2021-2294
    32371861 : REMOVE <FINEST> ENTRIES FROM .OUT LOG FILES
    32312961 : STRESS OICNG ICS - OWNERSHIPEXCEPTION - STUCK THREADS FROM SERVERTRANSACTIONIMPL.GLOBALRETRYROLLBACK - SERVER RESTARTED AFTER ~ 4HOURS
    32307656 : DYNAMIC BLOCKLIST CHANGES
    32248716 : CVE-2021-2214
    32244262 : PROVIDE MORE INFO WHEN GIVING 'USER NOT AUTHENTICATED' ERROR MESSAGE
    32235275 : CVE-2021-2211
    32228228 : WLS SERVER FAILED TO START WHEN MULTIDATASOURCE FAILOVER DB INSTANCE IS NOT REACHABLE
    32214441 : CVE-2021-2204
    32047972 : CVE-2018-10237
    32016868 : 17 FAILURES FROM R3 CORE-WORK-OVERLOAD ON STAGE WLS12.2.1.5.0
    31498405 : PERFORM EXTRA DESERIALIZATION VALIDATION WHEN ANONYMOUS RMI T3 AND IIOP REQUESTS ARE DISABLED
    31401659 : CVE-2019-3740
    30718589 : CVE-2021-2157
    29016742 : PSR:PERF:WLS JMS 19.1.0.0.0: ~10-15%  REGRESSION IN QUEUES PERSISTENT BENCHMRKS
    28625889 : REVERSE DEFAULT FOR DISABLERESOURCECHECKS
    28447848 : WLS 12.2.1.1.0 - JMS UOO UNABLE TO RECOVER TEMPORARY MEMBER DISCONNECTION FROM C
    28286720 : CFGFWK-64062: INVALID TEMPLATE - PARSING THE CONFIG-NODEMANAGER.XML FAILED!
    27944520 : JAVA.RMI.NOSUCHOBJECTEXCEPTION IN WEBLOGIC 12.2.1.3
    27388772 : STUCK THREAD ON WEBLOGIC.EJB.CONTAINER.INTERNAL.JMSCONNECTIONPOLLER
    26809939 : APPLICATION SCOPED SINGLETON SERVICE FAILS WITH ERROR
    26755797 : NOT ABLE TO DEPLOY SEVERAL IMPLEMENTATION VERSIONS OF A LIBRARY
    24964951 : STUCK THREAD ON CONSUMER PEER GONE

 Issues Resolved in WLS Patch Set Update 12.2.1.3.201217
    32108759 : CVE-2021-2109
    32069620 : CVE-2021-2075
    32068710 : JMS BRIDGE WITH XA THROWS ERROR WHEN RUNNING IN A CLUSTERED ENVIRONMENT
    32054481 : CVE-2020-14750
    31975423 : CVE-2019-10086
    31735728 : CVE-2021-2047
    31564423 : CVE-2021-2033
    31118905 : STRESS OIC ICS - PENGING REQUESTS AT MINTHREADSCONSTRAINT-ICS_ASYNC_MEP_WM NOT CLEANED UP WHEN REACHED THE MAX CONSTRIANT - HAVE TO RESTART SERVERS
    30866037 : NON-DESTRUCTIVE LEAK REPORTING FILES FALSE POSITIVES.
    30469341 : CVE-2019-17195
    30017325 : UNABLE TO EXTEND THE DOMAIN IN 12.2.1.3
    28913315 : PUMA: Reconfiguration wizard doesn't take JDBC URL to validate "User Messaging Service" schemas
    28475852 : 12.2.1.3.0 Reconfiguration Wizard - Gridlink Oracle RAC Data LDAP protocol issue
    28022064 : Fix for Bug 28022064
    26397072 : Fix for Bug 26397072
    26397061 : Fix for Bug 26397061
    18183882 : ONE WAY CALL TO WEB SERVICE RETURNING 200 CAUSES ERROR TO BE THROWN IN SOA

 Issues Resolved in WLS Patch Set Update 12.2.1.3.201001
    31913015 : CONSOLEHELP/EN-US INCORRECT IN JULY PSU
    31770512 : JAVA:* URL LOOKUPS ARE BLOCKED IN IIOP
    31765567 : CVE-2020-14883
    31765550 : CVE-2020-14882
    31657139 : MANAGED WLS FAIL TO STARTAFTER APPLYING JULY PSU 12.2.1.4.200624,WITH CONNECTION
    31567049 : CVE-2020-14859
    31510290 : LIMIT DISABLE OF EXTERNAL ENTITIES TO SERVER CODE
    31489815 : CVE-2019-17267
    31441174 : CVE-2020-14841
    31380363 : CVE-2020-14825
    31332264 : CVE-2020-14820
    31232471 : CVE-2020-11022
    31142740 : RFA: coherence.web:DistributedSessions service is not joining back the cluster after network outage
    30155056 : SERVICE MIGRATION GOES INTO A LOOP OR FAILS
    30110718 : NPE IN JDBCSTORE ON SERVICE RESTART
    29386864 : CVE-2020-14757
    28742863 : REPEATED FAILURES TO OPEN A STORE LEAKS POOL CONNECTIONS
    28728728 : LLR INITIALIZATION FAILS WHEN SERVER RESTARTS AFTER CRASH AND JDBC TLOG ENABLED
    27920427 : JMSSESSION HOLDING MESSAGE EVEN AFTER BEING CONSUMED BY MDB
    26018823 : STRESS:FA:FIN:MEM:MEMORY LEAK OF REPLICATEDSESSIONDATA FROM WLSMBEANSERVER

 Issues Resolved in WLS Patch Set Update 12.2.1.3.200624
    31380262 : DISPLAY WARNING IN CONSOLE IF JDK IS NOT SUPPORTED
    31353368 : CVE-2017-5645
    31332368 : CVE-2020-14687
    31316252 : CVE-2017-5645
    31297042 : CVE-2020-9546
    31247235 : CVE-2020-14652
    31234666 : CVE-2020-14645
    31234573 : CVE-2020-14644
    31157988 : CVE-2020-14625
    31113242 : CVE-2020-14622
    31047981 : STAGE 24 - 12.2.1.5.0 - BAM COMPOSER REPORTS DOESN'T SHOW DATA - ISSUE IN QUERYING DATABASE
    30964331 : CVE-2020-2967
    30961904 : CONNECTION FILTER DOES NOT WORK AFTER APPLYING PSU 12.2.1.3.191217
    30958807 : CVE-2020-2966
    30885128 : CVE-2020-14589
    30885114 : CVE-2020-14588
    30838007 : UPGRADE 12.2.1.3JAN2020 XAER_PROTO:ROUTINE WAS INVOKED IN AN IMPROPER CONTEXT
    30771358 : THE PATCH 29971088 IS CAUSING INITIALCONTEXT TO BE NULL
    30692988 : CVE-2020-14572
    30478451 : IIOP WTC TESTS FAIL WHEN TRYING TO GET AN INITIALCONTEXT
    30326976 : FIX THE QUOTE MARKS IN IDCS PROVIDER MESSAGE CATALOG
    30295025 : NOSUCHMETHODEXCEPTION WHEN CUSTOM EJB IS INVOKED AFTER APPLYING 12.2.1.3.190522
    30285053 : CVE-2020-14557
    29971088 : JAVA.IO.INVALIDOBJECTEXCEPTION: CAN'T DESERIALIZE ENUM IN WLS12.2.1.3
    29895972 : [WLS 12.2.1.3] PATCH 27086845 LEAVES LOT MANY CLOSE_WAIT CONNECTIONS
    28975384 : SYNCHRONIZATION NEEDED IN INITIALIZE METHOD OF SINGLETONMONITORSERVICETRACKER
    27191988 : MDBS FAIL TO RECONNECT TO REMOTE DT WHEN DT MEMBER IS RESTARTED
    26923558 : < HTTP-METHOD-OMISSION> IS NOT HONORED  WHEN WE EMBEDDED IN SECURITY CONSTARINT
    26444950 : NEWLY-ADDED FILES ON THE WEBLOGIC 12.2.1 CLASSPATH NOT VISIBLE TO WEB APPS
    25219796 : WLS 12.2.1 FAILS TO FETCH JAX-WS WEB SERVICES

 Issues Resolved in WLS Patch Set Update 12.2.1.3.200227
    30885237 : CVE-2020-2884
    30885217 : CVE-2020-2883
    30814590 : EMBEDDED LDAP CORRUPTED WHEN MGD SERVER IS KILLED
    30801769 : CVE-2020-2869
    30740009 : CVE-2020-2867
    30734182 : WEBLOGIC SSLCIPHERUTIL NEEDS TO SUPPORT NEW CIPHER SUITES ADDED IN TLS 1.3
    30670689 : CVE-2019-16943
    30633620 : SUPPORT FOR HTTP CORS IN WEBLOGIC REST API
    30624882 : CVE-2020-2811
    30563848 : CVE-2020-2801
    30558254 : CVE-2020-2798
    30459026 : BLOCKER: DEPLOYMENTPROGRESSOBJECTS RETURNING 502 ON JCS RECENTLY CREATED
    30068341 : CVE-2020-2766
    29464735 : [EJB]MANY FAILURES IN EJB IIOP TESTS
    29247835 : WEBLOGIC IS FAILING TO INJECT ENTITYMANAGER INTERMITTENTLY
    28593702 : MEMORY LEAK ON THE JAX-RPC CLIENT
    28482069 : CVE-2019-17571
    10206721 : MISSING USERNAME IN EXTENDED HTTP LOGS

 Issues Resolved in WLS Patch Set Update 12.2.1.3.191217
    30576401 : REGRESSION BUG FOR THIRD PARTY UPDATES IN PSU 12.2.1.3.191004
    30568713 : CVE-2019-17359
    30362086 : CVE-2020-2551
    30362026 : CVE-2020-2550
    30342923 : CVE-2020-2519
    30341541 : CVE-2020-2547
    30230430 : WLS WON'T START AT ALL IF THE IP V6 /64 LISTED ON THE CONNECTION FILTER
    30067299 : CVE-2020-6950
    29769772 : DEADLOCK ON WEBLOGIC.SERVLET.INTERNAL.ATTRIBUTEWRAPPER
    29671344 : CVE-2020-2519
    29425867 : PSR:PERF: WLS DOESN'T DETECT DEADLOCKS INVOLVING RE-RENTRANT LOCKS
    27158972 : FORMS LAUNCH FAILS WITH THE ERROR FRM-92101 AFTER APPLYING JULY'17 WEBLOGIC PSU
    26444945 : CVE-2020-2544

 Issues Resolved in WLS Patch Set Update 12.2.1.3.191004
    30180712 : CVE-2019-17091
    30153412 : CVE-2019-2888
    30088758 : JSCA CLUSTER RELATED TESTS FAILURE
    29957539 : CVE-2019-11358
    29921455 : TRACKING BUG FOR WLS ISSUE IN 29726561
    29913898 : CVE-2019-2907
    29752735 : MODIFY BODYCONTENTIMPL ON WRITE BUFFER
    29750025 : CVE-2019-2890
    29643116 : SESSION LEAK IN WEBLOGIC DURING LOGOUT
    29585355 : CVE-2019-2887
    29356775 : CVE-2019-2891
    29181056 : NEW TRANSACTIONS STARTED AFTER GRACEFUL SHUTDOWN STARTED (PART II)
    29158881 : CVE-2015-9251
    28973782 : Fix for Bug 28973782
    28879029 : TRACKING BUG TO CREATE WLS OVERLAY OF BUG 27332409 FIX FOR BLRS
    28867938 : STRESS:WLS:XA:TRANSACTION TIMING OUT DURING COMMIT IN XA TEST
    28794044 : STRESS:WLS:NULLPOINTER EXCEPTION IN ASYNC WEBSERVICES TEST CASE
    27817138 : ERROR WHILE TRYING TO DISABLE WADL GENERATION AND APPLICATION FAILED STATE
    27456095 : C9QA:INT:JCS Prov fails during sm-provisioning-check-operation-rex : OTD VM
    27228370 : SCHEMALOCATION IN GENERATED WSDL HAS // AFTER ?WSDL GENERATED WITH RELATIVE PATH
    27179313 : JTA SPAWNING ROLLBACK THREADS AFTER REMOTE SERVER IS DEAD OR DISCONNECTED
    26877609 : <MENTORING BUG> WEBLOGIC: INTERNAL RESPONSE TIMES INCREASES
    26593955 : NMAP SCANNING CAUSED WLS CRASH WHEN ENABLE SNMP WITH DEFAULT SETTING
    26199271 : XA RESOURCES SHOULD NOT CONTAIN THE SERVER NAME FOR MDBS.
    25830131 : OWSM POLICY ATTACHEMENT IS NOT SAVED AFTER RESTART
    24931180 : Fix for Bug 24931180

 Issues Resolved in WLS Patch Set Update 12.2.1.3.190522
    29789769 : FIXED AN ISSUE WITH XMLDECODER
    29726561 : CVE-2019-2729
    29701537 : CVE-2019-2827
    29667975 : CVE-2019-2824
    29448643 : JAVA.IO.INVALIDCLASSEXCEPTION: FILTER STATUS: REJECTED
    29411629 : CVE-2019-2856
    29338121 : Fix for Bug 29338121
    29312272 : WSDL ERROR MUST ATTRIBUTE 'NAME' NOTFOUND IN ELEMENT  'BINDING
    28278427 : VERSION ADDED TWICE WHEN SAVING A SECURITY POLICY
    27823500 : REGRESSION BUG WHICH INTRODUCED BY THE BUG FIXING OF 27678101
    27659077 : JSPS ARE GETTING RECOMPILED ON EVERY REQUEST
    27248932 : TRACKING BUG FOR 26941603 FOR WLS
    27010571 : <BEA-000503> <INCOMING MESSAGE HEADER OR ABBREVIATION PROCESSING FAILED
    26987594 : ALLOW SUPRESSING CROSS COMPONENT WIRING PROCESSING DURING PROVISIONING
    26403575 : CVE-2016-7103
    26131085 : IMPROVE CORRUPT STORE RECOVERY
    26075541 : .APPMERGEGEN_$DIGIT DIR REMAIN EVERY TIME BY DEPLOYING A EAR ON WLS 12.2.1
    25369207 : JAVA.LANG.OUTOFMEMORY ERROR HAPPENS WHEN INITIALIZING AN APPLICATION
    25294832 : WLS 12.2.1.2 DEPLOYMENT ERRORSMETHOD _JSPSERVICE EXCEEDS 65535 BYTES LIMIT

 Issues Resolved in WLS Patch Set Update 12.2.1.3.190416
    29140555 : CVE-2019-2650
    29140551 : CVE-2019-2649
    29140549 : CVE-2019-2648
    29140540 : CVE-2019-2647
    29140516 : CVE-2019-2646
    29140508 : CVE-2019-2645
    28984617 : UNABLE TO SET PRE-EMPTIVE AUTHENTICATION FOR WSDL PARSING.
    28958819 : FIXED AN ISSUE WHERE RECONFIGURE TEMPLATE CANNOT HANDLE DBCS DATA GUARD JDBC URL
    28895280 : CVE-2018-1258
    28891448 : CVE-2019-2618
    28874066 : CVE-2019-2615
    28774974 : FIXED NPE IN OUI WIZARD FOR DATABASE SCRIPTS PAGE
    28748179 : MAA - WLSSCHEMADATASOURCE SHOULD HAVE SECONDS-TO-TRUST-AN-IDLE-POOL-CONNECTION TO 0
    28651365 : TRANSACTION SUB-COORDINATOR CREATES A NEW RJVM CONNECTION TO SEND ACK
    28550962 : PSR:PERF:WLS WLS IDCSINTEGRATOR NEEDS TO HANDLE 429 RESPONSES FROM IDCS
    27397287 : ESS WSDL localizer ignoring HTTP non proxy host list
    27086845 : BPEL THROWS ENDPOINT PARSING EXCEPTION WHILE CALLING WEB BASED ONE WAY OSB PROXY
    27033250 : DEADLOCK AT WEBLOGIC.UTILS.CLASSLOADERS.CHANGEAWARECLASSLOADER.LOADCLASS
    26943614 : USING REST API CLIENT APP DEPLOYMENT FAILS IN K8S WLS DOMAIN
    26791760 : CVE-2019-2568

 Issues Resolved in WLS Patch Set Update 12.2.1.3.190115
    28632521 : CVE-2018-1000180
    28626991 : CVE-2019-2452
    28594324 : PERF PROD HUGE TIME SPENT IN WEBLOGIC.SECURITY.ACL.INTERNAL.AUTHENTICATEDSUBJECT
    28559579 : CVE-2019-2441
    28503638 : CTS J2EETOOLS TEST FAILED WITH FIX FOR BUG 26268190
    28319690 : BASIC AUTH DOES NOT WORK WITH PASSWORDS CONTAINING BACKSLASH CHARACTER
    28313163 : HTTP SESSION OBJECTS DOESN'T ADHER SESSION TIMEOUT WHEN CLIENT TERMINATES REQUES
    28166483 : TRACKING BUG TO CREATE WLS OVERLAY OF BUG 26001165 FIX FOR BLRS.
    28149607 : CVE-2015-1832
    28142116 : FIXED AN ISSUE WHERE REFERENCES TO VERSIONED INVENTORY ARTIFACTS WAS BREAKING BI ZDT
    28138954 : 12.2.1.3.1 OHS  FAILED TO START OHS POST INSTALL DUE TO NEW REQ FOR MKTEMP PKG
    28110087 : CVE-2019-2418
    28103938 : SECURITY ERROR CALLING EJB FROM WEBSTART APPLICATION USING THIN CLIENT
    27927071 : STRESS OIC ICS- NOSUCHELEMENTEXCEPTION DURING STRESS RUN
    27912485 : WLS IDCS CLOUD INTEGRATOR TO SUPPORT 429 RESPONSE CODES FROM OPC (THROTTLING)
    27561226 : STRESS-OSB-STUCK THREADS DURING ALERT TESTING WHEN JMS QUEUE IS DOWN
    27213775 : NPE ON COM.ORACLE.INJECTION.INTEGRATION.MODULECONTAINERINTEGRATIONSERVICE
    26624375 : NODEMANAGER MEMORY LEAK ON SSL HANDSHAKE FAILURES
    26353793 : CVE-2019-2398
    26267487 : ADFBC SERVER   DETECT QUIESCE MODE API

 Issues Resolved in WLS Patch Set Update 12.2.1.3.181016
    28409586 : CVE-2018-3252
    28375702 : CVE-2018-3246
    28375173 : CVE-2018-3245
    28360225 : FIXED NPE WHEN JMS DISTRIBUTED DESTINATION DOES NOT HAVE AN ACTIVE MEMBER DURING AN INTERNAL SEARCH OPERATION.
    28311332 : FIX TO REMOVE DUPLICATED CALL TO POLICYFEATUREUTILS.GETCLIENTEFFECTIVEPOLICYSET(CONTEXT)
    28172380 : FIX FOR 25800186 REVISED
    28171852 : FIXED A CLASSNOTFOUNDEXCEPTION WHILE DEPLOYING GAR THAT REFERENCES A SHARED LIBRARY.
    28140800 : BYPASS VERSION STRING CHECKS WHEN NON-ORACLE JDK IS USED.
    28071913 : CVE-2018-3201
    27988175 : CVE-2018-3191
    27928833 : FIXED A SERVER START ISSUE WHERE SERVER BOOT WILL HANG INDEFINITELY WHEN THE JDBC TLOG FEATURE IS CONFIGURED FOR THE SERVER AND AN EMPTY STRING VALUE IS SPECIFIED FOR THE DOMAINMBEAN SITENAME ATTRIBUTE.
    27486993 : FIXED A FAILURE TO UNDEPLOY APPLICATIONS FROM A DYNAMIC CLUSTER.
    27469756 : FIXED A MEMORY LEAK IN MBEANCICINTERCEPTOR THAT CAUSED ADMIN SERVER TO RUN OUT OF MEMORY.
    25580220 : FIXED AN ISSUE THAT PREVENTED TARGETING MULTIDATASOURCE TO A PERSISTENT STORE.

 Issues Resolved in WLS Patch Set Update 12.2.1.3.180717
    27948303 : CVE-2018-2893
    27947832 : FIXED AN ISSUE WHERE JAVAX.XML.XMLCONSTANTS.FEATURE_SECURE_PROCESSING WASN'T BEING PROPERLY PROPAGATED IN WSDLREADER.
    27934864 : CVE-2018-2998
    27819370 : CVE-2018-2987
    27803728 : CVE-2018-7489
    27693510 : FIXED DEFAULT VALUE FOR JAX-RS-MONITORING-DEFAULT-BEHAVIOR IN WEBAPP CONTAINER
    27617877 : FIXED FAILURE IN RECOVERY OF ALL CONFIGURED DETERMINERS CAUSED BY CONCURRENT ACCESS OF NOTLOG RESOURCE STATE
    27603087 : FIXED AN ISSUE WITH AN RCU CLEANUP SCRIPT
    27516977 : FIXED ACCESSCONTROLEXCEPTION THROWN WHILE NAVIGATING ADMIN CONSOLE WHILE JAVA SECURITY MANAGER IS ENABLED.
    27445260 : CVE-2018-2935
    27417245 : CVE-2018-2894
    27411153 : FIXED AUTHENTICATION FOR IDCS USERNAMES WITH MULTI-BYTE CHARACTERS
    27284496 : FIXED EXTREMELY SLOW WEBLOGIC START WHEN THERE ARE LARGE NUMBER OF OSB PROJECTS
    27234961 : IMPROVE PERFORMANCE OF BEAN CREATION TO REDUCE STUCK THREADS WHEN DATABASE IS SLOW OR DOWN
    27187631 : REDUCE IDCSINTEGRATOR DEFAULT VALUE FOR CONNECTION TIMEOUT TO 60S
    26626528 : FIXED FAILURE TO START COMPONENTS SIMULTANEOUSLY ON THE SAME HOST
    26502060 : FIXED JTA DETERMINERS ARRAY PROCESSING TO MAKE IT THREADSAFE
    26499391 : FIXED FAILURE TO SCALE DOWN BPM AFTER IT IS REGISTERED WITH OTD
    26268190 : FIXED AN ISSUE WHERE VARIOUS MANAGEMENT RMI CALLS ARE DISPATCHED USING DEFAULT WORK MANAGER INSTEAD OF WEBLOGIC.ADMIN.RMI WORK MANAGER.
    26145911 : ADDED DETECTION FOR LONG RUNNING WORK REQUESTS AND EXCLUDE THEM IN THREAD COUNT DECISION IN ENHANCED INCREMENT ADVISOR.
    26098043 : PROVIDE APP ROLES INFORMATION IN IDCS CLIENT FOR END-TO-END AUTHENTICATION FLOW
    26026959 : FIXED ERROR 404 WHILE LOADING DEPLOYED SOA COMPOSITES AFTER SCALE UP OF A DYNAMIC CLUSTER
    25488428 : FIXED ADDITION OF WSS USERNAME TOKEN SECURITY HEADER TO JAXWS DISPATCH CLIENT WITH CUSTOM POLICY ID
    23076695 : ENSURE USE OF FACTORY METHODS WHEN INSTANTIATING XMLINPUTFACTORY

 Issues Resolved in WLS Patch Set Update 12.2.1.3.180417
    27272911 : FIXED AN ISSUE WITH JAVAURLCONTEXTFACTORY
    27131483 : FIX METHOD NAME IN DEBUG MESSAGE WHEN DEBUGSECURITYATN IS ENABLED
    27118731 : FIX TYPO IN DEBUG MESSAGE WHEN DEBUGSECURITYATN IS ENABLED
    26929163 : FIXED AN ISSUE WITH WLS SCHEMA OWNER PERMISSIONS
    26806438 : FIXED A NULLPOINTEREXCEPTION CONDITION THAT MAY OCCUR WHEN TRYING TO ACTIVATE AN APPLICATION
    26731253 : FIX NOSUCHMETHODEXCEPTION THAT MAY OCCUR FOR IDENTITYASSERTER WHEN DEBUGSECURITYATN IS ENABLED
    26608537 : CVE-2018-2628
    26473149 : FIX NULLPOINTEREXCEPTION THAT OCCURRED IF A WEBAPP IS DEPLOYED FROM A WINDOWS SHARED FOLDER
    26439373 : CVE-2017-5645
    26080417 : FIXED AN ISSUE WHERE AN HTTP RESPONSE 204 WAS INCORRECTLY INCLUDING A RESPONSE BODY OF 0000
    25993295 : CVE-2013-1768
    25987400 : FIXED AN ISSUE WHERE IT WASN'T POSSIBLE TO PROVIDE INDIRECT TRANSACTION PROPAGATION BETWEEN SERVERS THAT ARE ON DIFFERENT NETWORKS
    25800186 : FIXED AN ISSUE WHERE A REDIRECT FROM WLS DID NOT ADD CONTENT-LENGTH OR CHUNKED-TRANSFER IN THE RESPONSE
    25665727 : FIXED AN ISSUE WHERE THE ADMIN SERVER WAS CONSUMING AN INORDINATE AMOUNT OF NATIVE MEMORY

 Issues Resolved in WLS Patch Set Update 12.2.1.3.180116
    27117282 : FIXED AN ISSUE WHERE CERTGEN WAS FAILING WITH JDK8 CPU (180161, B04, B05, B06)
    27111664 : FIXED AN ISSUE WITH THE WSDLREADER
    27055227 : PROVIDED ADDITIONAL DIAGNOSTIC INFORMATION FOR IDCS INTEGRATION
    26985581 : FIXED AN ISSUE WHERE A JAVA.LANG.STRINGINDEXOUTOFBOUNDSEXCEPTION CAN OCCUR
    26936500 : FIXED AN ISSUE IN THE WEBLOGICDEPLOYMENTMANAGER THAT CAUSED THE LIBRARY DEPLOYMENTS TO NOT BE RETURNED
    26835012 : FIXED A DEADLOCK CONDITION WITH MBEANSERVERCONNECTIONMANAGER
    26828499 : FIXED AN ISSUE WHERE THE HOST HEADER WAS BEING INCORRECTLY OVERRITTEN WHEN CLUSTER FRONTEND ADDRESS IS SET
    26589850 : FIXED AN ISSUE WHEREIN DOMAINRUNTIME.GETSERVERRUNTIME()WOULD TIME OUT ON A SLOW NETWORK
    26547016 : CVE-2018-2625
    26248394 : Fix for Bug 26248394
    26144830 : CVE-2017-10352
    25750303 : FIXED AN ISSUE WHERE FLUCTUATION IN THE NETWORK CONNECTION BETWEEN THE ADMIN AND MANAGED SERVER COULD CAUSE A PERMANENT DISCONNECT BETWEEN THE TWO
    23103220 : CVE-2016-5535

 


------------------


DISCLAIMER: 
Oracle recommends this Patch Set Update (PSU) for development and production systems in accordance with Doc ID 1306505.1.
 
This PSU may conflict with an interim patch(es) that has been applied to customer systems.
 If the interim patch is included in the PSU, the interim patch does not need to be applied to systems where the PSU is applied.
 If the interim patch is not included in the PSU, the conflict probably arises because the PSU modifies the same module as the interim patch.
 In such cases, customers should contact Oracle Support, provide information about all patches applied to the system, and request
 an overlay patch(es) that will resolve the conflict.
 
Copyright � 2023, Oracle and/or its affiliates. All rights reserved.
