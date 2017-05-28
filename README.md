# MongoDB
BSA Lection - 3: MongoDB

## This lesson was completed with use of Studio 3T.

1. A query to search for all students who's score > 87% and < 93% for any of the types of completed assignments:
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
2. Write an aggregation query to select all students who have a test result (type: "exam") of more than 90% (use unwind):
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
