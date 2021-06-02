# jq-JSON

```
[root@k8s-mas01 jnr]# cat fruit.json
{
  "fruit": {
    "name": "apple",
    "color": "green",
    "price": 1.2
  }
}

[root@k8s-mas01 jnr]# cat fruit.json | jq '.fruit.color'
"green"
[root@k8s-mas01 jnr]#

[root@k8s-mas01 jnr]# cat fruit.json | jq '.fruit.color,.fruit.name'
"green"
"apple"

[root@k8s-mas01 jnr]# cat fruit.json | jq '.fruit'
{
  "name": "apple",
  "color": "green",
  "price": 1.2
}

[root@k8s-mas01 jnr]# cat fruit.json | jq '.fruit | keys'
[
  "color",
  "name",
  "price"
]

Returning the Length
Another handy function for arrays and objects is the length function. We can use this function to return the array’s length or the number of properties on an object:
[root@k8s-mas01 jnr]# jq '.fruit | length' fruit.json
3

[root@k8s-mas01 jnr]# jq '.fruit.name | length' fruit.json
5




##############################################
#JSON Arrays
[root@k8s-mas01 jnr]# echo '["x","y","z"]' | jq '.[]'
"x"
"y"
"z"

[root@k8s-mas01 jnr]# cat array.json
[
  {
    "name": "apple",
    "color": "green",
    "price": 1.2
  },
  {
    "name": "banana",
    "color": "yellow",
    "price": 0.5
  },
  {
    "name": "kiwi",
    "color": "green",
    "price": 1.25
  }
]


[root@k8s-mas01 jnr]# cat array.json | jq .[0].name
"apple"
[root@k8s-mas01 jnr]# cat array.json | jq .[1].name
"banana"
[root@k8s-mas01 jnr]# cat array.json | jq .[2].name
"kiwi"

The map function is a powerful function we can use to apply a filter or function to an array:
[root@k8s-mas01 jnr]# jq 'map(has("name"))' array.json
[
  true,
  true,
  true
]

[root@k8s-mas01 jnr]# jq 'map(.price+2)' array.json
[
  3.2,
  2.5,
  3.24
]

{
  "name": "banana",
  "color": "yellow",
  "price": 0.5
}

[root@k8s-mas01 jnr]# jq '.[] | select(.color=="green")' array.json
{
  "name": "apple",
  "color": "green",
  "price": 1.2
}
{
  "name": "kiwi",
  "color": "green",
  "price": 1.24
}

Next up, we’re going to look at the test function which enables us to test if an input matches against a given regular expression:

[root@k8s-mas01 jnr]# jq '.[] | select(.name|test("^a.")) | .price' array.json
1.2
[root@k8s-mas01 jnr]# jq '.[] | select(.name|test("^b.")) | .price' array.json
0.5
[root@k8s-mas01 jnr]# jq '.[] | select(.name|test("^k.")) | .price' array.json
1.24


One common use case is to be able to see unique occurrences of a particular value within an array or remove duplicates
[root@k8s-mas01 jnr]# jq 'map(.color) | unique' array.json
[
  "green",
  "yellow"
]

```

```
[root@k8s-mas01 jnr]# cat niru.json
{
  "id": {
    "guide": "E00012345",
    "hello": "02283",
    "fec": [
      "S12345"
    ],
    "govtrack": 124421,
    "opensecrets": "NirU000",
    "lists": "S376"
  },
  "name": {
    "first": "Niranjan",
    "last": "Reddy",
    "official_full": ""
  },
  "bio": {
    "gender": "F",
    "birthday": "1977-07-01"
  },
  "terms": [
    {
      "type": "sen",
      "start": "2015-01-06",
      "end": "2021-01-03",
      "state": "IA",
      "class": 2,
      "state_rank": "junior",
      "party": "own party",
      "url": "http://www.example.com",
      "address": "Hyderabad",
      "office": "manikonda",
      "phone": "9989000880"
    }
  ]
}

[root@k8s-mas01 jnr]# cat niru.json | jq '.terms'
[
  {
    "type": "sen",
    "start": "2015-01-06",
    "end": "2021-01-03",
    "state": "IA",
    "class": 2,
    "state_rank": "junior",
    "party": "own party",
    "url": "http://www.example.com",
    "address": "Hyderabad",
    "office": "manikonda",
    "phone": "9989000880"
  }
]

[root@k8s-mas01 jnr]# cat niru.json | jq '.terms[].phone'
"9989000880"

[root@k8s-mas01 jnr]# cat niru.json | jq '.name'
{
  "first": "Niranjan",
  "last": "Reddy",
  "official_full": ""
}

[root@k8s-mas01 jnr]# cat niru.json | jq '.id'
{
  "guide": "E00012345",
  "hello": "02283",
  "fec": [
    "S12345"
  ],
  "govtrack": 124421,
  "opensecrets": "NirU000",
  "lists": "S376"
}

[root@k8s-mas01 jnr]# cat niru.json | jq '.name.first'
"Niranjan"

[root@k8s-mas01 jnr]# cat niru.json | jq '.bio .birthday'
"1985-07-01"

[root@k8s-mas01 jnr]#


```

