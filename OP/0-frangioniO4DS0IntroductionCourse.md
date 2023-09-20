[O4DS-0-Introduction to the course](zotero://select/library/items/TM2PVGZU)

NOTES
*Imported on 2023-09-20 11:31*

# The model

> [!cite|#ffd400]+ Highlight [(p.17)](zotero://open-pdf/library/items/8DX7Y4LA?page=17&annotation=HYRMIXUS))
> *" How a mathematical model should be: 1. accurate (describes well the process at hand) 2. computationally inexpensive (gives answers rapidly) 3. general (can be applied to many different processes) Typically impossible to have all three! "*
> 
>


> [!cite|#ffd400]+ Highlight [(p.17)](zotero://open-pdf/library/items/8DX7Y4LA?page=17&annotation=PIUHYVC8))
> *" the map is not the world "*
> 
>
# Analytic and Synthetic models

> [!cite|#ffd400]+ Highlight [(p.17)](zotero://open-pdf/library/items/8DX7Y4LA?page=17&annotation=PBHY6IUB))
> *" Analytic models: flexible shape, (relatively) few “hand-chosen” parameters "*
> Quite accurate but hard to construct
>


> [!cite|#ffd400]+ Highlight [(p.17)](zotero://open-pdf/library/items/8DX7Y4LA?page=17&annotation=K77NCXFF))
> *" Synthetic models: rigid shape, (very) many automatically chosen parameters "*
> Simple and reproduce the observed behaviour
>

# Fitting

> [!cite|#ffd400]+ Highlight [(p.17)](zotero://open-pdf/library/items/8DX7Y4LA?page=17&annotation=TG6X2F6T))
> *" Fitting: find the parameters of the model that best represents the phenomenon "*
> This is an optimization problem. This is the problem where you should invest. So in the choice of parameters.
>


> [!cite|#ffd400]+ Highlight [(p.20)](zotero://open-pdf/library/items/8DX7Y4LA?page=20&annotation=DV3YYS5U))
> *" Noisy measurement but (hopefully) simple/smooth underlying physical process "*
> We don't need noisy data, what we're looking for is a smooth function.
>


> [!cite|#ffd400]+ Highlight [(p.21)](zotero://open-pdf/library/items/8DX7Y4LA?page=21&annotation=9KDBMP5B))
> *" Polynomial interpolation "*
> 
>

> [!cite|#ffd400]+ Image [(p. 8)](zotero://open-pdf/library/items/8DX7Y4LA?page=8&annotation=763W8D9K)
> ![[_Media/image-21-x8-y89.png]]
> Finding the c is a very simple task. In Matlab is just c=y/X.
> This is the Loss Function to minimize, so is the Linear Least Square. How much the model fails to capture reality. So we want to minimize this function.

>


%% Import Date: 2023-09-20T11:31:45.420+02:00 %%
