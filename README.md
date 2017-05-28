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
3. Modify Dusty Lemmond's documents([query result][3rd]):
```javascript
db.philippLypniakov.aggregate(
	// Pipeline
	[
		// Stage 1
		{
			$match: {
			name : "Dusti Lemmond"
			}
		},

		// Stage 2
		{
			$addFields: {
			    "accepted": true
			}
		},

	]

);
```

[Studio 3T]: <https://studio3t.com/>
[1st]: <https://github.com/RAYDENFilipp/MongoDB/blob/4552062f5a6ac1baf3279a4bf5ac655456cd2200/dataSample.json>
[2nd]:<https://github.com/RAYDENFilipp/MongoDB/blob/05c2cfef17de6ffc4fde533c4b46cff97250fe67/dataSample.json>
[3rd]:<https://github.com/RAYDENFilipp/MongoDB/blob/468c57b9c3937102417fc3bd3321ba1d24511b21/dataSample.json>
