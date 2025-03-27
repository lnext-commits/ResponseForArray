# Salvatory output array

## _The capabilities of our storage_



Let's create a method with an array

``` php
use ResponseForArray

public function getData ($option, $key): array|string
    {
         $arr = [
            'upper1' => [
                'attachments1' => [
                    'internal1' => [
                        'value1',
                        'value2',
                        'value3',
                    ]
                ],
                'attachments2' => [
                    'internal2' => [
                        'value4',
                        'value5',
                        'value6',
                    ]
                ],
            ],
            'upper2' => [
                'attachments3' => 'value1',
                'attachments4' => 'value2',
                'attachments5' => 'value1',
                'attachments6' => 'value2',
            ],
            'upper3' => [
                'attachments7' => 'value10',
                'attachments8' => 'value11',
                'attachments9' => 'value12',
                'attachments10' => 'value13',
            ],
        ];

        return $this->returnArray($arr, $option, $key, __FUNCTION__);
    }

```

Access to the array from anywhere in the application

Code:

``` php 
getData (); 
```

Result

```
array:3 [
  "upper1" => array:2 [
    "attachments1" => array:1 [
      "internal1" => array:3 [
        0 => "value1"
        1 => "value2"
        2 => "value3"
      ]
    ]
    "attachments2" => array:1 [
      "internal2" => array:3 [
        0 => "value4"
        1 => "value5"
        2 => "value6"
      ]
    ]
  ]
  "upper2" => array:4 [
    "attachments3" => "value1"
    "attachments4" => "value2"
    "attachments5" => "value1"
    "attachments6" => "value2"
  ]
  "upper3" => array:4 [
    "attachments7" => "value10"
    "attachments8" => "value11"
    "attachments9" => "value12"
    "attachments10" => "value13"
  ]
]
```

---
Transmitted  __options__

- key

Code:

``` php 
getData ('key'); 
```

Result

```
array:3 [
  0 => "upper1"
  1 => "upper2"
  2 => "upper3"
]
```

- value

Code:

``` php 
getData('value');
```

Result

```
array:3 [
  0 => array:2 [
    "attachments1" => array:1 [
      "internal1" => array:3 [
        0 => "value1"
        1 => "value2"
        2 => "value3"
      ]
    ]
    "attachments2" => array:1 [
      "internal2" => array:3 [
        0 => "value4"
        1 => "value5"
        2 => "value6"
      ]
    ]
  ]
  1 => array:4 [
    "attachments3" => "value1"
    "attachments4" => "value2"
    "attachments5" => "value1"
    "attachments6" => "value2"
  ]
  2 => array:4 [
    "attachments7" => "value10"
    "attachments8" => "value11"
    "attachments9" => "value12"
    "attachments10" => "value13"
  ]
]
```

- dot

Code:

``` php 
getData('dot');
```

Result

```
array:14 [
  "upper1.attachments1.internal1.0" => "value1"
  "upper1.attachments1.internal1.1" => "value2"
  "upper1.attachments1.internal1.2" => "value3"
  "upper1.attachments2.internal2.0" => "value4"
  "upper1.attachments2.internal2.1" => "value5"
  "upper1.attachments2.internal2.2" => "value6"
  "upper2.attachments3" => "value1"
  "upper2.attachments4" => "value2"
  "upper2.attachments5" => "value1"
  "upper2.attachments6" => "value2"
  "upper3.attachments7" => "value10"
  "upper3.attachments8" => "value11"
  "upper3.attachments9" => "value12"
  "upper3.attachments10" => "value13"
]
```

---
Transmitted  __key__

Code:

``` php
getData( key: 'upper1');
```

Result

```
array:2 [
  "attachments1" => array:1 [
    "internal1" => array:3 [
      0 => "value1"
      1 => "value2"
      2 => "value3"
    ]
  ]
  "attachments2" => array:1 [
    "internal2" => array:3 [
      0 => "value4"
      1 => "value5"
      2 => "value6"
    ]
  ]
]
```

Code:

``` php 
getData( key: 'upper1.attachments1.internal1');
```

Result

```
array:3 [
  0 => "value1"
  1 => "value2"
  2 => "value3"
]
```

---

Combining

Code:

``` php 
getData('key', 'upper1.attachments1');
```

Result

```
array:1 [
  0 => "internal1"
]
```

Code:

``` php 
getData('value', 'upper1.attachments1');
```

Result

```
array:1 [
  0 => array:3 [
    0 => "value1"
    1 => "value2"
    2 => "value3"
  ]
]
```

Code:

``` php 
getData('dot', 'upper1.attachments1');
```

Result

```
array:3 [
  "internal1.0" => "value1"
  "internal1.1" => "value2"
  "internal1.2" => "value3"
]
```

---

Expansion __option__

Code:

``` php 
getData('key.value1', 'upper2');
```

Result

```
array:2 [
  0 => "attachments3"
  1 => "attachments5"
]
```

Code:

``` php 
getData('value.value12', 'upper3');
```

Result

```
"attachments9"
```

---

Error if there is no requested key

Code:

``` php 
getData(key: 'upper1.qwr'); 
```

Result

```
"the required key (upper1.qwr) is not in the array (getData) signature:%^$*!@$!"
```
