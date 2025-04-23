Usage example:
```
$ ./table_stat -h ../heavy.serialized -l ../light.serialized -s ../place_stats.serialized
INFO: 2022-02-14 17:51:18.502 +0300 query_handler.cpp:10 Entries in heavy table: 1000                                                                
INFO: 2022-02-14 17:51:18.503 +0300 query_handler.cpp:11 Entries in light table: 1000                                                                
INFO: 2022-02-14 17:51:18.503 +0300 query_handler.cpp:12 Entries in stats table: 94                                                                  
>> Nth HEAVY 228                                                                                                                                     
{ FullElapsed: 89222 HeavyPlace: "model_bids_recommender" }                                                                                          
>> Nth LIGHT 42                                                                                                                                      
{ FullElapsed: 0 LightPlace: "consistency_check" }                                                                                                   
>> Stat consistency_check                                                                                                                            
{ Place: "consistency_check" MinElapsed: 0 MaxElapsed: 126606 P50: 0 P70: 1 P90: 4 P95: 5 P99: 6.7065311829377618 P9999: 107.76005263174028 }        
>> Stat nonexistent_place                                                                                                                            
no such place                                                                                                                                        
>> Nth Heavy 100500                                                                                                                                  
Invalid query, enter 'h' for help                                                                                                                    
>> Nth HEAVY 100500                                                                                                                                  
n is too big                                                                                                                                         
>> h                                                                                                                                                 
h                       print this help message                                                                                                      
q                       quit                                                                                                                         
Nth (HEAVY | LIGHT)     get n-th heavy/light place                                                                                                   
Stat place              print place's statistics                                                                                                     
                                                                                                                                                     
>> q                                                                                                                                                 
INFO: 2022-02-14 17:52:34.578 +0300 main.cpp:82 Answered to 7 queries
```

