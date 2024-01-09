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
{
  "activeUsers": 516
}
```

## [ $group ]

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
{
  "_id": null,
  "averageAge": 29.835
}
```

### Q3. List top 5 most common favorite fruits among users.
