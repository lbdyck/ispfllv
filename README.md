# ispfllv
ISPF ISPLIST/ISPLOG Sysout Viewer                                            
                                                                             
This exec provides the ISPF user, who has allocated both ISPLIST and ISPLOG to SYSOUT, with the ability to view the active contents of these DD's.       
                                                                             
Why Allocate ISPLIST/ISPLOG to SYSOUT?                                       
--------------------------------------                                       
                                                                             
There are many reasons, the primary being the desire to prevent the ISPLIST and ISPLOG datasets from being allocated to DASD where they have to be managed.           

Installation                                                                    
------------                                                                    
                                                                                
 1. Copy member ISPFLLV into a PDS in your SYSEXEC, or SYSPROC, allocation.     
                                                                                
 2. Update your ISPF Command table with these entries:                          
                                                                                
          Verb  Trunc  Action                                                   
                       Description                                              
          VLIST     3  SELECT CMD(%ISPFLLV &ZPARM LIST)                         
                       Display ISPLIST SYSOUT using SDSF REXX API               
          VLOG      3  SELECT CMD(%ISPFLLV &ZPARM LOG)                          
                       Display ISPLOG SYSOUT using SDSF REXX API                
                                                                                
 3. Update your TSO/ISPF Logon Procedure JCL so that both ISPLIST and ISPLOG are allocated to SYSOUT.                                                    
                                                                                
    //ISPLIST  DD SYSOUT=*,DCB=(LRECL=121,BLKSIZE=1210,RECFM=FBA)               
    //ISPLOG   DD SYSOUT=*,DCB=(LRECL=125,BLKSIZE=129,DSORG=PS,RECFM=VA)        
                                                                                
or                                                                              
                                                                           
 4. Update your TSO/ISPF Logon Clist/Exec so that both ISPLIST and ISPLOG are allocated to SYSOUT thus:                                          
                                                                           
    alloc f(isplist) sysout(h) hold lrecl(121) blksize(1210) recfm(f b a)  
    alloc f(isplog)  sysout(h) hold lrecl(125) blksize(129) recfm(v a)     
                                                                           
 5. Install STEMEDIT from CBTTape File 895 into a load library in your ISPLLIB set of allocated libraries, or into your Link list.            
                                                                           
 6. Verify that the intended users have access to use the SDSF REXX API. If using (E)JES then validate that the SDSF REXX API equivalent has been configured.                                                       
                                                                           
Usage                                                                      
-----                                                                      
                                                                           
Once the above installation steps have been completed then just enter VLIST (abbreviation of VLI) on the ISPF command line to view the contents of the active ISPLIST DD, or VLOG (abbreviation VLO) to view the active ISPLOG DD contents.                                                        
                                                                        
Optionally, enter VLOG ?, or VLIST ?, to display the ISPF Tutorial panel for ISPFLLV.                                                            