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
                 |-------------|         |---------|
                 |  Offer      |         | Offer   |
                 |  Pending    |-------->| Matched |
                 |  (SF5)      |         | (SF35)  |
                 |-------------|         |---------|
                   /          \
                  /            \
                 /              \
                v                v
          |----------|        |---------|
          | Shopper  |        | Offer   |
          | Rejected |        | pulled  |
          | (SF20)   |        | (SF15)  |
          |----------|        |---------|
```

### Match and Order Stage
```
|---------------|     |----------|      |---------|
| Order Created |---->| Item     |----->| Order   |
| (Paid)        |     | Shipped  |      | Done    |
|---------------|     |----------|      |---------|
```

