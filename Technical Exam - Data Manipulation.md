# Technical Exam

Using the initial data below create a function that will achieve the expected result data show it to console:

### Initial data:

```json
[
  {
    "id": 1,
    "name": "John Doe",
    "status": 1
  },
  {
    "id": 2,
    "name": "Jane Doe",
    "status": 2
  },
  {
    "id": 3,
    "name": "Adam Rocket",
    "status": 2
  },
  {
    "id": 4,
    "name": "Luis Rocket",
    "status": 1
  }
]
```

### Expected Result Data:

```json
{
  "status-1": [
    {
      "id": 1,
      "name": "John Doe",
      "status": 1
    },
    {
      "id": 4,
      "name": "Luis Rocket",
      "status": 1
    }
  ],
  "status-2": [
    {
      "id": 2,
      "name": "Jane Doe",
      "status": 2
    },
    {
      "id": 3,
      "name": "Adam Rocket",
      "status": 2
    }
  ]
}
```

### My Answer

Created a function called **groupByStatus** that takes intial data(object) that can groups the items base on their status. The function should create an object with keys like **`"status-1"`**, **`"status-2"`**, etc., and the corresponding values are arrays containing the items with the respective status.

```js
const initialData = [
  {
    id: 1,
    name: 'John Doe',
    status: 1,
  },
  {
    id: 2,
    name: 'Jane Doe',
    status: 2,
  },
  {
    id: 3,
    name: 'Adam Rocket',
    status: 2,
  },
  {
    id: 4,
    name: 'Luis Rocket',
    status: 1,
  },
];

function groupByStatus(data) {
  const newData = {};

  data.forEach((item) => {
    const { status } = item;
    if (!resultData[`status-${status}`]) {
      resultData[`status-${status}`] = [];
    }
    newData[`status-${status}`].push(item);
  });

  return newData;
}

const groupedData = groupByStatus(initialData);
console.log(groupedData);
```
