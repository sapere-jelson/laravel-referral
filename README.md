
<p align="center">
    <p align="center">
        <a href="https://packagist.org/packages/sapere/laravel-referral"><img alt="Latest Version on Packagist" src="https://img.shields.io/packagist/v/sapere/laravel-referral.svg?style=flat-square"></a>
        <a href="https://packagist.org/packages/sapere/laravel-referral"><img alt="Total Downloads" src="https://img.shields.io/packagist/dt/sapere/laravel-referral"></a>
        <a href="https://packagist.org/packages/sapere/laravel-referral"><img alt="License" src="https://img.shields.io/github/license/sapere/laravel-referral"></a>
    </p>
</p>


The "sapere/laravel-referral" package is a custom Laravel package that provides referral code functionality for your Laravel applications. It allows you to generate referral codes, associate them with users, retrieve users based on their referral codes and all other related features.

- [Installation](#installation)
    - [Configuration](#configuration)
    - [Migration](#migration)
    - [Add Trait](#add-trait)
- [Usage](#usage)
    - [Generate Referral Accounts for Existing Users](#generate-referral-accounts-for-existing-users)
    - [Get the Referrer of a User](#get-the-referrer-of-a-user)
    - [Get Referrer by Referral Code](#get-referrer-by-referral-code)
    - [Check if a User has a Referral Account](#check-if-a-user-has-a-referral-account)
    - [Create a Referral Account for a User](#create-a-referral-account-for-a-user)
    - [Get All Referrals of a User](#get-all-referrals-of-a-user)
    - [Get the Referral Link of a User](#get-the-referral-link-of-a-user)
- [Changelog](#changelog)
- [Contribution](#contributing)
- [License](#license)

## Installation

You can install the package via Composer by running the following command:

```bash
composer require sapere/laravel-referral
```

#### Configuration
The package provides a configuration file that allows you to customize its behavior. You should publish the migration and the config/referral.php config file with:
```php
php artisan vendor:publish --provider="sapere\LaravelReferral\Providers\ReferralServiceProvider"
```
After publishing, you can find the configuration file at config/referral.php. This file allows you to configure the cookie name and other package-specific settings.

#### Migration
After the config and migration have been published and configured, you can create the tables for this package by running:
```php
 php artisan migrate
```

#### Add Trait
Add the necessary trait to your User model:
```php
use sapere\LaravelReferral\Traits\Referrable;

class User extends Model
{
    use Referrable;
}
```

## Usage

#### Generate Referral Accounts for Existing Users
To generate referral accounts for existing users, you can visit the following URL:
```plaintext
http://localhost:8000/generate-ref-accounts
```
This will generate referral codes for all existing users in your application.<br><br>

#### Get the Referrer of a User
To get the referrer of a user, you can use the following code:
```php
use Illuminate\Support\Facades\Auth;

$user = Auth::user();
$referrer = $user->referralAccount->referrer;
```
This retrieves the referrer associated with the user.<br><br>

#### Get Referrer by Referral Code
To get the referrer by referral code, you can use the following code:
```php
use sapere\LaravelReferral\Models\Referral;
use Illuminate\Support\Facades\Cookie;

$referralCode = Cookie::get(config('referral.cookie_name'));
$referrer = Referral::userByReferralCode($referralCode);

```
This retrieves the referrer based on the referral code stored in the cookie.<br><br>

#### Check if a User has a Referral Account
To check if a user has a referral account, you can use the following code:
```php
$user->hasReferralAccount();
```
This returns `true` if the user has a referral account, and `false` otherwise.<br><br>

#### Create a Referral Account for a User
To create a referral account for a user, you can use the following code:
```php
$user->createReferralAccount($referrer->id);
```
This associates the user with the provided referrer by creating a referral account.<br><br>

#### Get All Referrals of a User
To get all referrals under a user, you can use the following code:
```php
$referrals = $user->referrals;
```
This retrieves all the referrals associated with the user.<br><br>

#### Get the Referral Link of a User
To get the referral link of a user, you can use the following code:
```php
$referralLink = $user->getReferralLink();
```
This returns the referral link associated with the user.

## Changelog
Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing
Thank you for considering contributing to the Laravel Referral Package! If you have any suggestions, bug reports, or pull requests, please feel free to open an issue or submit a pull request on the GitHub repository.

## License
The Laravel Referral Package is open-source software licensed under the [MIT](LICENSE.md) license.



