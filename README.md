# utl-avoiding-klingon-macro-triggers-at-macro-execution-time
Avoiding klingon macro triggers at macro execution time 
    Avoiding klingon macro triggers at macro execution time                                                                        
                                                                                                                                   
    github                                                                                                                         
    https://tinyurl.com/y7ohzwux                                                                                                   
    https://github.com/rogerjdeangelis/utl-avoiding-klingon-macro-triggers-at-macro-execution-time                                 
                                                                                                                                   
    SAS Forum                                                                                                                      
    https://tinyurl.com/yc9h4p4p                                                                                                   
    https://communities.sas.com/t5/SAS-Programming/TRANSTR-works-in-a-datastep-but-does-not-inside-SYSFUNC/m-p/658400              
                                                                                                                                   
    Patrick                                                                                                                        
    https://communities.sas.com/t5/user/viewprofilepage/user-id/12447                                                              
                                                                                                                                   
    Avoiding klingon macro triggers at macro execution time                                                                        
                                                                                                                                   
       a. Klingon solution                                                                                                         
       b. dosubl solution                                                                                                          
      
       Nice recent imlification  by Bart                            
                                                
      %symdel s / nowarn;                             
                                                
      %let a=A,B,C;                                   
                                                
      %let s=%sysfunc(transtrn("&a",%str(,)," "));    
                                                
      %put &=s;                                       
                                                
      Bartosz Jablonski                               
      yabwon@gmail.com                                
                                                
                                                                                                                             
    You need this macro                                                                                                            
                                                                                                                                   
    %macro dosubl(arg);                                                                                                            
      %let rc=%qsysfunc(dosubl(&arg));                                                                                             
    %mend dosubl;                                                                                                                  
                                                                                                                                   
    *_                   _                                                                                                         
    (_)_ __  _ __  _   _| |_                                                                                                       
    | | '_ \| '_ \| | | | __|                                                                                                      
    | | | | | |_) | |_| | |_                                                                                                       
    |_|_| |_| .__/ \__,_|\__|                                                                                                      
            |_|                                                                                                                    
    ;                                                                                                                              
                                                                                                                                   
    %let a=A,B,C;                                                                                                                  
                                                                                                                                   
    *            _               _                                                                                                 
      ___  _   _| |_ _ __  _   _| |_                                                                                               
     / _ \| | | | __| '_ \| | | | __|                                                                                              
    | (_) | |_| | |_| |_) | |_| | |_                                                                                               
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                              
                    |_|                                                                                                            
    ;                                                                                                                              
                                                                                                                                   
    Macro variable s                                                                                                               
                                                                                                                                   
    %put &=s;                                                                                                                      
                                                                                                                                   
    S="A" "B" "C"                                                                                                                  
                                                                                                                                   
    *                                                                                                                              
     _ __  _ __ ___   ___ ___  ___ ___                                                                                             
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                            
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                            
    | .__/|_|  \___/ \___\___||___/___/                                                                                            
    |_|                                                                                                                            
               _    _ _ _                                                                                                          
      __ _    | | _(_) (_) __ _  ___  _ __                                                                                         
     / _` |   | |/ / | | |/ _` |/ _ \| '_ \                                                                                        
    | (_| |_  |   <| | | | (_| | (_) | | | |                                                                                       
     \__,_(_) |_|\_\_|_|_|\__, |\___/|_| |_|                                                                                       
                          |___/                                                                                                    
    ;                                                                                                                              
                                                                                                                                   
    %symdel s / nowarn;                                                                                                            
                                                                                                                                   
    %let a=A,B,C;                                                                                                                  
                                                                                                                                   
    %let s="%sysfunc(transtrn(%nrbquote(&a),%nrbquote(,)," "))";                                                                   
    %put &=s;                                                                                                                      
                                                                                                                                   
    *_            _                 _     _                                                                                        
    | |__      __| | ___  ___ _   _| |__ | |                                                                                       
    | '_ \    / _` |/ _ \/ __| | | | '_ \| |                                                                                       
    | |_) |  | (_| | (_) \__ \ |_| | |_) | |                                                                                       
    |_.__(_)  \__,_|\___/|___/\__,_|_.__/|_|                                                                                       
                                                                                                                                   
    ;                                                                                                                              
                                                                                                                                   
    * more easily enhanced and maintained?;                                                                                        
                                                                                                                                   
    %symdel s / nowarn;                                                                                                            
                                                                                                                                   
    %let a=A,B,C;                                                                                                                  
                                                                                                                                   
    %dosubl(%nrstr(                                                                                                                
     data _null_;                                                                                                                  
       s=TRANSTRN("&a",',',quote(' '));                                                                                            
       call symputx('s',s);                                                                                                        
     run;quit;                                                                                                                     
     ));                                                                                                                           
                                                                                                                                   
     %let s="&s";                                                                                                                  
                                                                                                                                   
     %put &=s;                                                                                                                     
                                                                                                                                   
    *                       __                                                                                                     
     _ __  _ __ ___   ___  / _|                                                                                                    
    | '_ \| '__/ _ \ / _ \| |_                                                                                                     
    | |_) | | | (_) | (_) |  _|                                                                                                    
    | .__/|_|  \___/ \___/|_|                                                                                                      
    |_|                                                                                                                            
    ;                                                                                                                              
                                                                                                                                   
    * this proces that dosubl executes at macro execution time;                                                                    
                                                                                                                                   
    %symdel s / nowarn;                                                                                                            
                                                                                                                                   
    %let a=A,B,C;                                                                                                                  
                                                                                                                                   
    data macrotime;                                                                                                                
                                                                                                                                   
       %dosubl(%nrstr(                                                                                                             
         %symdel s / nowarn;                                                                                                       
         data _null_;                                                                                                              
           s=TRANSTRN("&a",',',quote(' '));                                                                                        
           call symputx('s',s);                                                                                                    
         run;quit;                                                                                                                 
                                                                                                                                   
         ));                                                                                                                       
                                                                                                                                   
         %let  s="&s";                                                                                                             
                                                                                                                                   
         result=resolve('&s');                                                                                                     
                                                                                                                                   
         output;                                                                                                                   
                                                                                                                                   
    run;quit;                                                                                                                      
                                                                                                                                   
    Up to 40 obs from MACROTIME total obs=1                                                                                        
                                                                                                                                   
    Obs      RESULT                                                                                                                
                                                                                                                                   
                                                                                                                                   
