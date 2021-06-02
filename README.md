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


```

