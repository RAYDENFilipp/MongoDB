# MongoDB
BSA Lection - 3: MongoDB

## This lesson was completed with use of [Studio 3T].

1. A query to search for all students who's score > 87% and < 93% for any of the types of completed assignments([query result][1st]):
```javascript
db.philippLypniakov.find({
    "scores": {
        $elemMatch: {
            "score": {
                $gt: 87,
                $lt: 93
            }
        }
    }
});
```
2. Write an aggregation query to select all students who have a test result (type: "exam") of more than 90% (use unwind)([query result][2nd]):
```javascript
db.philippLypniakov.aggregate(
	// Pipeline
	[
		// Stage 1
		{
			$unwind: {
			    path : "$scores"
			}
		},

		// Stage 2
		{
			$match: {
			 "scores.type" : "exam",
			 "scores.score" : { $gt : 90 }
			}
		},

	]
);
```
3. Modify Dusty Lemmond's documents([query result][3rd]; [acknowledgement result][4th]):
```javascript
//Update Dusty Lemmond documents
db.philippLypniakov.updateMany(
   {name : "Dusti Lemmond"},
   {$set : { "accepted" : true } }
);

//Return Dusty's documents
db.philippLypniakov.find({
    "name": "Dusti Lemmond"
});
```

[Studio 3T]: <https://studio3t.com/>
[1st]: <https://github.com/RAYDENFilipp/MongoDB/blob/master/firstSearch.json>
[2nd]:<https://github.com/RAYDENFilipp/MongoDB/blob/master/secondSearch.json>
[3rd]:<https://github.com/RAYDENFilipp/MongoDB/blob/master/thirdSearch.json>
[4th]: <https://github.com/RAYDENFilipp/MongoDB/blob/master/thirdSearchAcknowledgement.json>
