# পিএইচপি Array ভিত্তিক প্রয়োজনীয় কিছু ফাংশন

_পড়া এবং বোঝার সুবিধার্থে ফাংশনগুলো **A to Z** বা **Ascending Order** এ দেয়া হল। যদিও ক্লাস ভিডিওতে **Most Used** অর্ডারে দেখানো হয়েছে।_

## array_chunk

তালিকায় প্রথমেই আসে [`array_chunk()`](https://www.php.net/manual/en/function.array-chunk.php) ফাংশন।

একটি অ্যারেকে নির্দিষ্ট একটি দৈর্ঘ্য _(given length)_ অনুযায়ী খণ্ডে খণ্ডে ভাগ করার প্রয়োজন হলে আমরা `array_chunk()` এই ফাংশনটি ব্যবহার করতে পারি। **দ্রষ্টব্যঃ** শেষ খণ্ডটির দৈর্ঘ্য গিভেন লেংথের থেকে কম হতে পারে।

### ফাংশন প্যারামিটার

এই ফাংশনে ৩টি প্যারামিটার সেট করা আছে। ফলে আমরা ৩টিই আর্গুমেন্ট পাঠাতে পারব।

1. প্রথম আর্গুমেন্টে ভাগ করতে চাওয়া অ্যারে দিতে হবে
2. দ্বিতীয় আর্গুমেন্টে কাঙ্খিত দৈর্ঘ্য বা লেংথটি দিতে হবে, যার উপর ভিত্তি করে অ্যারেটির বিভাজন ঘটবে।
3. এই প্যারামিটারটি ঐচ্ছিক। ২টি আর্গুমেন্ট পাঠাতে পারব, `true` এবং `false`। ডিফল্টভাবে `false` সেট করা থাকে। যার দরুণ, প্রতিটা _chunk_ বা খণ্ডের ইনডেক্স 0 থেকে শুরু হয়। যদি `true` সেট করা হয় তাহলে **Associative Array** হিসেবে _key_ গুলো সংরক্ষণ করে। ফলে ইনডেক্স 0 থেকে শুরু না হয়ে যেখান থেকে অ্যারেটা বিভক্ত হয়েছে সেই ইনডেক্স ভ্যালু বা _key_ টা বিভাজিত নতুন অ্যারেতে বিদ্যমান থাকে।

#### ফাংশন কি রিটার্ন করে?

এই ফাংশনটি মাল্টিডাইমেনশনাল অ্যারে রিটার্ন করে, যার ইনডেক্সিং গণনা শূণ্য থেকে শুরু হয়। যেখানে প্রতিটা ডাইমেনশন (খণ্ডিত অ্যারে) লেংথে দেয়া সংখ্যার ভ্যালু ধারণ করে।

উদাহরণঃ

```php
<?php
$fruits = array('banana', 'apple', 'orange', 'plum', 'dates');

$someFruits = array_chunk($fruits, 2);
$fruitsKeyPreserved = array_chunk($fruits, 2, true);

print_r($someFruits);

print_r($fruitsKeyPreserved);
```

আউটপুটঃ

```
Array
(
    [0] => Array
        (
            [0] => banana
            [1] => apple
        )

    [1] => Array
        (
            [0] => orange
            [1] => plum
        )

    [2] => Array
        (
            [0] => dates
        )
)

Array
(
    [0] => Array
        (
            [0] => banana
            [1] => apple
        )

    [1] => Array
        (
            [2] => orange
            [3] => plum
        )

    [2] => Array
        (
            [4] => dates
        )
)
```

**Note:** ২য় আর্গুমেন্ট তথা লেংথ যদি 1 এর কম হয় তাহলে **পিএইচপি 8.0.0** থেকে [**ValueError**](https://www.php.net/manual/en/class.valueerror.php) জাতীয় _Error_ থ্রো করে থাকে।

## array_filter

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের সব এলিমেন্ট গুলোকে একটি ফাংশনের মধ্যে পাঠাতে পারি এবং সেই ফাংশনের মধ্যে যেই কন্ডিশন থাকবে সেই কন্ডিশন অনুযায়ী ফিল্টার করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যারে এবং দ্বিতীয় প্যারামিটার হচ্ছে একটি ফাংশন। এই ফাংশন সব এলিমেন্ট গুলোকে সেই ফাংশনের মধ্যে পাঠায় এবং সেই ফাংশনের মধ্যে যেই কন্ডিশন থাকবে সেই কন্ডিশন অনুযায়ী ফিল্টার করে ফেলে।

```php
<?php
$numbers = array(1, 2, 3, 4, 5);

$evenNumbers = array_filter($numbers, function ($number) {
    return $number % 2 == 0;
});

print_r($evenNumbers);
```

আউটপুট:

```php
Array
(
    [1] => 2
    [3] => 4
)
```

আরেকটা উদাহরণ

```php
<?php

$users = [
    ['username' => 'john', 'score' => 0],
    ['username' => 'jane', 'score' => 1],
    ['username' => 'doe', 'score' => 2],
];

$activeUsers = array_filter($users, function ($user) {
    return $user['score'] > 0;
});

print_r($activeUsers);
```

আউটপুট:

```php
Array
(
    [1] => Array
        (
            [username] => jane
            [score] => 1
        )

    [2] => Array
        (
            [username] => doe
            [score] => 2
        )

)
```

## array_flip

এই ফাংশনের মাধ্যমে আমরা কোন অ্যাসোসিয়েটিভ অ্যারের key এবং ভ্যালু একইসাথে এক্সচেঞ্জ করতে পারি অর্থাৎ ভ্যালুকে key এবং key গুলোকে ভ্যালুতে পরিনত করতে পারি।

```php
<?php
$fruits = array(
    'a' => 'banana',
    'b' => 'apple',
    'c' => 'orange'
);

$flippedFruits = array_flip($fruits);

print_r($flippedFruits);
```

আউটপুট:

```php
Array
(
    [banana] => a
    [apple] => b
    [orange] => c
)
```

## array_key_exists

এই ফাংশনের মাধ্যমে আমরা কোন একটি key আছে কিনা তা চেক করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে চেক করতে চাওয়া key এবং দ্বিতীয় প্যারামিটার হচ্ছে অ্যারে।

```php
<?php
$fruits = array(
    'a' => 'banana',
    'b' => 'apple',
    'c' => 'orange'
);

if (array_key_exists('a', $fruits)) {
    echo 'Key exists';
} else {
    echo 'Key does not exist';
}
```

আউটপুট:

```php
Key exists
```

## array_key_first

এই ফাংশনের মাধ্যমে আমরা কোন অ্যাসোসিয়েটিভ অ্যারের প্রথম key পেতে পারি।

```php
<?php
$fruits = array(
    'a' => 'banana',
    'b' => 'apple',
    'c' => 'orange'
);

$firstKey = array_key_first($fruits);

echo $firstKey;
```

আউটপুট:

```php
a
```

## array_key_last

এই ফাংশনের মাধ্যমে আমরা কোন অ্যাসোসিয়েটিভ অ্যারের শেষ key পেতে পারি।

```php
<?php
$fruits = array(
    'a' => 'banana',
    'b' => 'apple',
    'c' => 'orange'
);

$lastKey = array_key_last($fruits);

echo $lastKey;
```

আউটপুট:

```php
c
```

## array_keys

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের সব key গুলো পেতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যারে এবং দ্বিতীয় প্যারামিটার হচ্ছে অপশনাল। যদি আমরা দ্বিতীয় প্যারামিটার দেই তাহলে এই ফাংশন সেই অ্যারের মধ্যে সেই ভ্যালু গুলোর key গুলো দেখাবে।

```php
<?php
$fruits = array('apple', 'banana', 'orange');

$keys = array_keys($fruits);

print_r($keys);
```

আউটপুট:

```php
Array
(
    [0] => 0
    [1] => 1
    [2] => 2
)
```

## array_map

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের সব এলিমেন্ট গুলোকে একটি ফাংশনের মধ্যে পাঠাতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে একটি ফাংশন এবং দ্বিতীয় প্যারামিটার হচ্ছে অ্যারে। এই ফাংশন সব এলিমেন্ট গুলোকে সেই ফাংশনের মধ্যে পাঠায়।

```php
<?php
$fruits = array('apple', 'banana', 'orange');

$upperCaseFruits = array_map('strtoupper', $fruits);

print_r($upperCaseFruits);
```

আউটপুট:

```php
Array
(
    [0] => APPLE
    [1] => BANANA
    [2] => ORANGE
)
```

আরেকটা উদাহরণ

```php
<?php

$persons = [
    [
        'name' => 'John Doe',
        'age' => 32,
    ],
    [
        'name' => 'Jane Doe',
        'age' => 28,
    ],
    [
        'name' => 'James Doe',
        'age' => 30,
    ],
];

$names = array_map(function ($person) {
    return $person['name'];
}, $persons);

print_r($names);
```

আউটপুট:

```php
Array
(
    [0] => John Doe
    [1] => Jane Doe
    [2] => James Doe
)
```

## array_merge_recursive

এই ফাংশনের মাধ্যমে আমরা একাধিক অ্যারেকে একটি অ্যারেতে মার্জ করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে মার্জ করতে চাওয়া অ্যারে এবং দ্বিতীয় প্যারামিটার হচ্ছে মার্জ করার অ্যারে।

```php
<?php
$fruits = array('banana', 'apple', 'orange');
$vegetables = array('carrot', 'collard', 'pea');

$foods = array_merge_recursive($fruits, $vegetables);

print_r($foods);
```

আউটপুট:

```php
Array
(
    [0] => banana
    [1] => apple
    [2] => orange
    [3] => carrot
    [4] => collard
    [5] => pea
)
```

## array_merge

এই ফাংশনের মাধ্যমে আমরা একাধিক অ্যারেকে একটি অ্যারেতে মার্জ করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে মার্জ করতে চাওয়া অ্যারে এবং দ্বিতীয় প্যারামিটার হচ্ছে মার্জ করার অ্যারে।

```php
<?php
$fruits = array('banana', 'apple', 'orange');
$vegetables = array('carrot', 'collard', 'pea');

$foods = array_merge($fruits, $vegetables);

print_r($foods);
```

আউটপুট:

```php
Array
(
    [0] => banana
    [1] => apple
    [2] => orange
    [3] => carrot
    [4] => collard
    [5] => pea
)
```

## array_multisort

এই ফাংশনের মাধ্যমে আমরা একাধিক অ্যারেকে sort করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে sort করতে চাওয়া অ্যারে এবং দ্বিতীয় প্যারামিটার হচ্ছে sort করার ধরন।

```php
<?php
$fruits = array('banana', 'apple', 'orange');
$numbers = array(2, 1, 3);

array_multisort($fruits, $numbers);

print_r($fruits);
print_r($numbers);
```

আউটপুট:

```php
Array
(
    [0] => apple
    [1] => banana
    [2] => orange
)
Array
(
    [0] => 1
    [1] => 2
    [2] => 3
)
```

## array_pop

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের শেষ এলিমেন্ট কে রিমুভ করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যারে।

```php
<?php
$fruits = array('banana', 'apple', 'orange');

$lastElement = array_pop($fruits);

print_r($fruits);
echo $lastElement;
```

আউটপুট:

```php
Array
(
    [0] => banana
    [1] => apple
)
orange
```

## array_push

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের শেষে একটি এলিমেন্ট যোগ করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যারে এবং দ্বিতীয় প্যারামিটার হচ্ছে যে এলিমেন্টটি যোগ করতে চাই।

```php
<?php
$fruits = array('banana', 'apple', 'orange');

array_push($fruits, 'plum');

print_r($fruits);
```

আউটপুট:

```php
Array
(
    [0] => banana
    [1] => apple
    [2] => orange
    [3] => plum
)
```

## array_reduce

```php
<?php
$numbers = array(1, 2, 3, 4, 5);

$total = array_reduce($numbers, function ($carry, $number) {
    $carry += $number;
    return $carry;
});

echo $total;
```

আউটপুট:

```php
15
```

## array_reverse

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারেকে reverse করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে reverse করতে চাওয়া অ্যারে।

```php
<?php
$fruits = array('banana', 'apple', 'orange', 'plum', 'dates');

$reversedFruits = array_reverse($fruits);

print_r($reversedFruits);
```

আউটপুট:

```php
Array
(
    [0] => dates
    [1] => plum
    [2] => orange
    [3] => apple
    [4] => banana
)
```

## in_array()

এই ফাংশন দিয়ে আমরা যদি কোন একটি এলিমেন্ট একটি অ্যারের মধ্যে আছে কিনা তা চেক করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে এলিমেন্ট এবং দ্বিতীয় প্যারামিটার হচ্ছে অ্যারে। এই ফাংশন যদি এলিমেন্ট অ্যারের মধ্যে পাই তাহলে এটি true রিটার্ন করবে আর না পাইলে ফলাফল হবে false।

```php
<?php
$fruits = array('apple', 'banana', 'orange');

if (in_array('apple', $fruits)) {
    echo 'Apple exists';
} else {
    echo 'Apple does not exist';
}
```

আউটপুট:

```php
Apple exists
```

আরেকটা উদাহরন

```php
<?php

$allowedFileExtensions = ['jpg', 'jpeg', 'png', 'gif'];

$filename = 'image.png';

$fileParts = explode('.', $filename);

$fileExtension = strtolower(end($fileParts));

if (in_array($fileExtension, $allowedFileExtensions)) {
    echo 'File is allowed';
} else {
    echo 'File is not allowed';
}
```

আউটপুট:

```php
File is allowed
```

## array_sum ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের সব এলিমেন্ট গুলোর যোগফল বের করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যারে।

```php
<?php
$numbers = array(1, 2, 3, 4, 5);

$total = array_sum($numbers);

echo $total;
```

আউটপুট:

```php
15
```

আরেকটা উদাহরণ

```php
<?php

function add() {
    return array_sum(func_get_args());
}

echo add(1, 2, 3, 4, 5);
```

আউটপুট:

```php
15
```

## array_walk ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের সব এলিমেন্ট গুলোকে একটি ফাংশনের মধ্যে পাঠাতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যারে এবং দ্বিতীয় প্যারামিটার হচ্ছে একটি ফাংশন। এই ফাংশন সব এলিমেন্ট গুলোকে সেই ফাংশনের মধ্যে পাঠায়।

```php
<?php
$fruits = array('apple', 'banana', 'orange');

array_walk($fruits, function (&$fruit) {
    $fruit = strtoupper($fruit);
});

print_r($fruits);
```

আউটপুট:

```php
Array
(
    [0] => APPLE
    [1] => BANANA
    [2] => ORANGE
)
```

## sort ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের সব এলিমেন্ট গুলোকে উর্দ্ধক্রমানুসারে sort করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যারে।

```php
<?php
$fruits = array('banana', 'apple', 'orange');

sort($fruits);

print_r($fruits);
```

আউটপুট:

```php
Array
(
    [0] => apple
    [1] => banana
    [2] => orange
)
```

## rsort ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের সব এলিমেন্ট গুলোকে অধঃক্রমানুসারে rsort করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যারে।

```php
<?php
$fruits = array('banana', 'apple', 'orange');

rsort($fruits);

print_r($fruits);
```

আউটপুট:

```php
Array
(
    [0] => orange
    [1] => banana
    [2] => apple
)
```

## asort ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যাসোসিয়েটিভ অ্যারের সব এলিমেন্ট গুলোকে অ্যারের ভ্যালুর উর্দ্ধক্রমানুসারে asort করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যাসোসিয়েটিভ অ্যারে।

```php
<?php
$fruits = array(
    'a' => 'banana',
    'b' => 'apple',
    'c' => 'orange'
);

asort($fruits);

print_r($fruits);
```

আউটপুট:

```php
Array
(
    [b] => apple
    [a] => banana
    [c] => orange
)
```

## ksort ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যাসোসিয়েটিভ অ্যারের সব এলিমেন্ট গুলোকে অ্যারের key গুলোর উর্দ্ধক্রমানুসারে sort করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যাসোসিয়েটিভ অ্যারে।

```php
<?php
$fruits = array(
    'a' => 'banana',
    'b' => 'apple',
    'c' => 'orange'
);

ksort($fruits);

print_r($fruits);
```

আউটপুট:

```php
Array
(
    [a] => banana
    [b] => apple
    [c] => orange
)
```

## natsort ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যাসোসিয়েটিভ অ্যারের সব এলিমেন্ট গুলোকে sort করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যাসোসিয়েটিভ অ্যারে।

```php
<?php
$fruits = array('orange2', 'orange10', 'orange1');

natsort($fruits);

print_r($fruits);
```

আউটপুট:

```php
Array
(
    [2] => orange1
    [0] => orange2
    [1] => orange10
)
```

## usort ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যাসোসিয়েটিভ অ্যারের সব এলিমেন্ট গুলোকে sort করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যাসোসিয়েটিভ অ্যারে এবং দ্বিতীয় প্যারামিটার হচ্ছে একটি ফাংশন। এই ফাংশন সব এলিমেন্ট গুলোকে সেই ফাংশনের মধ্যে পাঠায় এবং সেই ফাংশনের মধ্যে যেই কন্ডিশন থাকবে সেই কন্ডিশন অনুযায়ী sort করে ফেলে।

```php
<?php
$fruits = array(
    'a' => 'banana',
    'b' => 'apple',
    'c' => 'orange'
);

usort($fruits, function ($a, $b) {
    return $a > $b;
});

print_r($fruits);
```

আউটপুট:

```php
Array
(
    [0] => apple
    [1] => banana
    [2] => orange
)
```

## rand ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি random নাম্বার পেতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে শুরুর random নাম্বার এবং দ্বিতীয় প্যারামিটার হচ্ছে শেষের random নাম্বার।

```php
<?php
$randomNumber = rand(1, 10);

echo $randomNumber;
```

আউটপুট:

```php
7
```

## array_slice ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের একটি range কে return করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যারে এবং দ্বিতীয় প্যারামিটার হচ্ছে range এর শুরুর index এবং তৃতীয় প্যারামিটার হচ্ছে range এর শেষের index।

```php
<?php
$fruits = array('banana', 'apple', 'orange', 'plum', 'dates');

$someFruits = array_slice($fruits, 1, 3);

print_r($someFruits);
```

আউটপুট:

```php
Array
(
    [0] => apple
    [1] => orange
    [2] => plum
)
```

## array_splice ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের একটি range কে রিমুভ করতে পারি এবং সেই রিমুভ করা এলিমেন্ট গুলোকে আমরা অন্য কোন অ্যারেতে রাখতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে অ্যারে এবং দ্বিতীয় প্যারামিটার হচ্ছে range এর শুরুর index এবং তৃতীয় প্যারামিটার হচ্ছে range এর শেষের index।

```php
<?php
$fruits = array('banana', 'apple', 'orange', 'plum', 'dates');

$someFruits = array_splice($fruits, 1, 3);

print_r($fruits);
print_r($someFruits);
```

আউটপুট:

```php
Array
(
    [0] => banana
    [1] => dates
)
Array
(
    [0] => apple
    [1] => orange
    [2] => plum
)
```

## array_unique ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি অ্যারের ডুপ্লিকেট এলিমেন্ট গুলো রিমুভ করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে রিমুভ করতে চাওয়া অ্যারে।

```php
<?php
$fruits = array('banana', 'apple', 'orange', 'plum', 'dates', 'banana', 'apple');

$uniqueFruits = array_unique($fruits);

print_r($uniqueFruits);
```

আউটপুট:

```php
Array
(
    [0] => banana
    [1] => apple
    [2] => orange
    [3] => plum
    [4] => dates
)
```

## array_search ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন একটি এলিমেন্ট এর index খুঁজে বের করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে খুঁজে বের করতে চাওয়া এলিমেন্ট এবং দ্বিতীয় প্যারামিটার হচ্ছে অ্যারে।

```php
<?php
$fruits = array('banana', 'apple', 'orange', 'plum', 'dates');

$index = array_search('orange', $fruits);

echo $index;
```

আউটপুট:

```php
2
```

## implode ফাংশন{#implode-array-function}

এই ফাংশনের মাধ্যমে আমরা কোন অ্যারেকে স্ট্রিং এ কনভার্ট করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে ডেলিমিটার এবং দ্বিতীয় প্যারামিটার হচ্ছে স্ট্রিং এ কনভার্ট করতে চাওয়া অ্যারে।

```php
<?php
$fruits = array('banana', 'apple', 'orange');

$string = implode(', ', $fruits);

echo $string;
```

আউটপুট:

```php
banana, apple, orange
```

## explode ফাংশন

এই ফাংশনের মাধ্যমে আমরা কোন স্ট্রিং কে অ্যারেতে কনভার্ট করতে পারি। এই ফাংশনের প্রথম প্যারামিটার হচ্ছে ডেলিমিটার এবং দ্বিতীয় প্যারামিটার হচ্ছে স্ট্রিং ধারনকৃত ভেরিএবল নাম।

```php
<?php
$string = 'banana, apple, orange';

$fruits = explode(', ', $string);

print_r($fruits);
```

আউটপুট:

```php
Array
(
    [0] => banana
    [1] => apple
    [2] => orange
)
```

**ডেভলপমেন্ট প্রক্রিয়াধীন...............**