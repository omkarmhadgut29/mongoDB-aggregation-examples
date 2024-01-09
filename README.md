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
>     -   $avg : (accumulator)
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
> -   $group:
>     -   This is used for creating groups of somthing
>     -   $avg : (accumulator)
>     -   This is used for getting average.
