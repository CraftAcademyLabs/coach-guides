## Final assessment

The goal of this is to assess your skills in programming and associated tasks (version control, DevOps, agile, etc). You will be given 2 programming challenges and ssome programming related questions. 

1. Comments Challenge
2. Viaplay Challenge
3. Questions Written submission

#### Time & Format
4 hours during withch you need to be online in a coach supervisioned conference call (Google Meet). You need to share your the screen/monitor where your IDE is displayed. 

#### Delivery:

All code must be delivered in the form of a **Pull Request** against the repositories that the examiner will provide to you (onefor each challenge).

## Comments Challenge


## Viaplay Challenge

You are challenged with the task of replicating a UI. It is a desktop only web application listing TV series from Viaplay. 

The pesented UI looks like this:


You need to fetch the data from the Viaplay API andd find the appropoite attributes that hold the information you need. 

The API is located at:

```
https://content.viaplay.se/pc-se/serier/samtliga
```

The TV series listings can be found at: 
```js
yourDataObject._embedded['viaplay:blocks'][0]._embedded['viaplay:products']
```

