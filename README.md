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
