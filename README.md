# Dot notation accessor & dot notation access array

Simple dot notation access for PHP arrays

## Example

```
<?php

use Gorka\DotNotationAccess\DotNotationAccessArray;

$mongoConnection = [
    'mongo' => [
        'default' => [
            'user' => 'username',
            'password' => 's3cr3t'
        ]
    ]
];
$config = new DotNotationAccessArray($mongoConnection);

// Get plain value

$user = $config->get('mongo.default.user');
/*
    $user = 'username';
*/ 

// Get array value

$mongoDefault = $config->get('mongo.default'); 
/* 
    $mongoDefault = ['user' => 'username', 'password' => 's3cr3t'];
*/

// Overwrite values

$overwrite = [
    'mongo' => [
        'default' => [
            'user' => 'myuser',
            'server' => 'localhost'
        ],
        'numbers' => [1, 1, 2, 3, 5, 8, 13]
    ],
    'title' => 'Dot Notation'
];

$config = $config->merge($overwrite);
$configDump = $config->getAll();
/*
    $configDump = [
        'mongo' => [
            'default' => [
                'user' => 'myuser',
                'password' => 's3cr3t',
                'server' => 'localhost',
            ],
            'numbers' => [1, 1, 2, 3, 5, 8, 13]
        ],
        'title' => 'Dot Notation'
    ];
*/

// Remove value

$config = $config->remove('mongo.default');
$configDump = $config->getAll();
/*
    $configDump = [
        'mongo' => [
            'numbers' => [1, 1, 2, 3, 5, 8, 13]
        ],
        'title' => 'Dot Notation'
    ];
*/


// Set values

$config = $config->set('mongo.numbers', [2, 3, 5, 7, 11]);
$configDump = $config->getAll();
/*
    $configDump = [
        'mongo' => [
            'numbers' => [2, 3, 5, 7, 11]
        ],
        'title' => 'Dot Notation'
    ];
*/
```
