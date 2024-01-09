## [ $match, $count ]

### Q1. How many users are active?

```
[
  {
    $match: {
      isActive: true,
    },
  },
  {
    $count: "activeUsers",
  },
]
```

##### Output

```
[
    {
        "activeUsers": 516
    }
]
```

> [!NOTE]
>
> -   $match:
>     -   This is used for searching in DB.
>     -   It's like where clause in RDB.

## [ $group, $avg, $sum, $sort, $limit ]

### Q2. What is average age of all users?

```
[
  {
    $group: {
      _id: null,
      averageAge: {
        $avg: "$age",
      }
    }
  }
]
```

##### Output

```
[
    {
        "_id": null,
        "averageAge": 29.835
    }
]
```

> [!NOTE]
>
> -   $group:
>     -   This is used for creating groups of somthing
> -   $avg : (accumulator)
>     -   This is used for getting average.

### Q3. List top 2 most common favorite fruits among users.

```
[
  {
    $group: {
      _id: "$favoriteFruit",
      count: {
        $sum: 1,
      },
    },
  },
  {
    $sort: {
      count: -1
    }
  },
  {
    $limit: 2
  }
]
```

##### Output

```
[
    {
        "count": 339,
        "_id": "banana"
    },
    {
        "_id": "apple",
        "count": 338
    }
]
```

> [!NOTE]
>
> -   $sum:
>     -   It accepts number by which it will be adding if there is new entry found.
> -   $sort:
>     -   sorting data in ascending (1) or in descending order.
> -   $limit:
>     -   limit the documents passing from above pipeline.

### Q4. Find total numbers of males and females.

```
[
  {
    $group: {
      _id: "$gender",
      count: {
        $sum: 1,
      }
    }
  }
]
```

#### Output:

```
[
  {
    "_id": "female",
    "count": 507
  },
  {
    "_id": "male",
    "count": 493
  }
]
```

### Q5. Which contry has highest number of registered users?

```
[
  {
    $group: {
      _id: "$company.location.country",
      count: {
        $sum: 1,
      }
    }
  },
  {
    $sort: {
      count: -1
    }
  },
  {
    $limit: 1
  }
]
```

#### Output:

```
[
  {
    "_id": "Germany",
    "count": 261
  }
]
```

### Q6. List all unique eye colors present in the collection.

```
[
  {
    $group: {
      _id: "$eyeColor",
    }
  }
]
```

#### Output:

```
[
  {
    _id: "blue",
  },
  {
    "_id": "green"
  },
  {
    "_id": "brown"
  }
]
```

## [ $unwind ]

### Q7. What is average numbers of tags per user?

**_Methode 1_**

```
[
  {
    $unwind: {
      path: "$tags",
    }
  },
  {
    $group: {
      _id: "$_id",
      numOfTags: {
        $sum: 1,
      }
    }
  },
  {
    $group: {
      _id: null,
      average: {
        $avg: "$numOfTags"
      }
    }
  }
]
```

#### Output:

```
[
  {
    "_id": null,
    "average": 3.556
  }
]
```
