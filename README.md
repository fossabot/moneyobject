# moneyobject

[![Travis](https://img.shields.io/travis/fortis/moneyobject.svg?branch=master)](https://travis-ci.org/fortis/moneyobject)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/fortis/moneyobject/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/fortis/moneyobject/?branch=master)
[![Coveralls](https://img.shields.io/coveralls/fortis/moneyobject/master.svg)](https://coveralls.io/github/fortis/moneyobject?branch=master)
[![Packagist](https://img.shields.io/packagist/l/fortis/moneyobject.svg)](https://packagist.org/packages/fortis/moneyobject)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Ffortis%2Fmoneyobject.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Ffortis%2Fmoneyobject?ref=badge_shield)

A PHP library providing immutable Money value object with arbitrary-precision and solution for floating point rounding errors.

What do you think will be printed in the example below?
``` php
print (36 - 35.99) === 0.01 ? '✅ equals' : 'not equals 😈';
```
Actually `not equals 😈` . You can try [https://ideone.com/2UQlBF](https://ideone.com/2UQlBF). 

> Squeezing infinitely many real numbers into a finite number of bits requires an approximate representation. Although there are infinitely many integers, in most programs the result of integer computations can be stored in 32 bits. In contrast, given any fixed number of bits, most calculations with real numbers will produce quantities that cannot be exactly represented using that many bits. Therefore the result of a floating-point calculation must often be rounded in order to fit back into its finite representation. This rounding error is the characteristic feature of floating-point computation.
>
> *-- [Oracle](https://docs.oracle.com/cd/E19957-01/806-3568/ncg_goldberg.html)*

## Install

Install directly from command line using Composer
``` bash
composer require fortis/moneyobject
```

## QuickStart

#### Currency code validation
``` php
$money = new Money(100, 'USF'); // throws InvalidCurrencyException
```

#### Create Money instance
``` php
$money = Money::USD(100.20);                       // 100.20 USD. Short syntax with autocomplete.
$money = new Money(100.20, CurrencyCode::USD);     // 100.20 USD  
$money = Money::create(100.20, CurrencyCode::USD); // 100.20 USD
```

#### Get currency
``` php
$money->getCurrency()->getCode(); // USD
```

#### Get amount
``` php
$money->getAmount()->toFloat();   // 100.20
```

#### Multiply: 100.20 * 2
``` php
$money->multiply(2)
      ->getAmount()->toFloat(); // 200.40
```

#### Divide: 100.20 / 2
``` php
$money->divide(Money::USD(2))
      ->getAmount()->toFloat(); // 50.10
```

#### Plus: 100.20 + 2.5
``` php
$money->plus(Money::USD(2.5))
      ->getAmount()->toFloat(); // 102.70
```

#### Minus: 100.20 - 0.5
``` php
$money->minus(Money::USD(0.5))
      ->getAmount()->toFloat(); // 99.70
```

#### Minus: 36 - 35.99      
``` php
Money::USD(36)->minus(Money::USD(35.99))
              ->getAmount()->toFloat(); // 0.01
```

#### Minus: 36 - 35.99        
``` php
Money::USD(36)->minus(35.99)
              ->getAmount()->toFloat(); // 0.01
```

#### Convert USD to EUR
```bash
$ composer require florianv/swap php-http/message php-http/guzzle6-adapter
```

``` php
$swap = (new SwapBuilder())
    ->add('fixer')
    ->build();
$converter = new Converter($swap);
$usd50 = Money::USD(50);
$result = $converter->convert($usd50, Currency::EUR());
```

## Credits

- [Florian Voutzinos](https://github.com/florianv)


## License

moneyobject is licensed under the MIT license.


[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Ffortis%2Fmoneyobject.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Ffortis%2Fmoneyobject?ref=badge_large)