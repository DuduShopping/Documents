### Request State
```
                                                                     
                  |------------------|                              
                  |   Request        |
                  |   Pending (SR5)  |                                  
                  |------------------|                                  
                    /               \                                   
                   /                 \                                       
                  /                   \                                 
                 v                     v
          |-------------|        |-------------|        |----------|       
          |  Request    |        |   Request   |        | Request  |        
          |  Cancelled  |<-------|   Accepted  |------->| Matched  |                                                
          |  (SR10)     |        |   (SR15)    |        | (SR30)   |      
          |-------------|        |-------------|        |----------|
```

### Offer State
```
                 |-------------|
                 |  Offer      |
                 |  Pending    |
                 |  (SF5)      |
                 |-------------|
                   /          \
                  /            \
                 /              \
                v                v
          |----------|        |---------|         |---------|
          | Shopper  |        | Offer   |         | Offer   |
          | Rejected |        | pulled  |-------->| Matched |
          | (SF20)   |        | (SF15)  |         | (SF35)  |
          |----------|        |---------|         |---------|
```

### Match and Order Stage
```
|---------------|     |----------|      |---------|
| Order Created |---->| Item     |----->| Order   |
| (Paid)        |     | Shipped  |      | Done    |
|---------------|     |----------|      |---------|
```

