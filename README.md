﻿# Clean Code PHP

## မာတိကာ

  1. [Introduction](#introduction)
  2. [Variables](#variables)
     * [Use meaningful and pronounceable variable names](#use-meaningful-and-pronounceable-variable-names)
     * [Use the same vocabulary for the same type of variable](#use-the-same-vocabulary-for-the-same-type-of-variable)
     * [Use searchable names (part 1)](#use-searchable-names-part-1)
     * [Use searchable names (part 2)](#use-searchable-names-part-2)
     * [Use explanatory variables](#use-explanatory-variables)
     * [Avoid nesting too deeply and return early (part 1)](#avoid-nesting-too-deeply-and-return-early-part-1)
     * [Avoid nesting too deeply and return early (part 2)](#avoid-nesting-too-deeply-and-return-early-part-2)
     * [Avoid Mental Mapping](#avoid-mental-mapping)
     * [Don't add unneeded context](#dont-add-unneeded-context)
     * [Use default arguments instead of short circuiting or conditionals](#use-default-arguments-instead-of-short-circuiting-or-conditionals)
  3. [Comparison](#comparison)
     * [Use identical comparison](#use-identical-comparison)
  4. [Functions](#functions)
     * [Function arguments (2 or fewer ideally)](#function-arguments-2-or-fewer-ideally)
     * [Functions should do one thing](#functions-should-do-one-thing)
     * [Function names should say what they do](#function-names-should-say-what-they-do)
     * [Functions should only be one level of abstraction](#functions-should-only-be-one-level-of-abstraction)
     * [Don't use flags as function parameters](#dont-use-flags-as-function-parameters)
     * [Avoid Side Effects](#avoid-side-effects)
     * [Don't write to global functions](#dont-write-to-global-functions)
     * [Don't use a Singleton pattern](#dont-use-a-singleton-pattern)
     * [Encapsulate conditionals](#encapsulate-conditionals)
     * [Avoid negative conditionals](#avoid-negative-conditionals)
     * [Avoid conditionals](#avoid-conditionals)
     * [Avoid type-checking (part 1)](#avoid-type-checking-part-1)
     * [Avoid type-checking (part 2)](#avoid-type-checking-part-2)
     * [Remove dead code](#remove-dead-code)
  5. [Objects and Data Structures](#objects-and-data-structures)
     * [Use object encapsulation](#use-object-encapsulation)
     * [Make objects have private/protected members](#make-objects-have-privateprotected-members)
  6. [Classes](#classes)
     * [Prefer composition over inheritance](#prefer-composition-over-inheritance)
     * [Avoid fluent interfaces](#avoid-fluent-interfaces)
     * [Prefer `final` classes](#prefer-final-classes)
  7. [SOLID](#solid)
     * [Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
     * [Open/Closed Principle (OCP)](#openclosed-principle-ocp)
     * [Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
     * [Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
     * [Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)
  8. [Don’t repeat yourself (DRY)](#dont-repeat-yourself-dry)
  9. [Translations](#translations)

## နိဒါန်း

Robert C. Martin ရဲ့ လက်ရာမြှောက် [*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) စာအုပ်ထဲက Software engineering principles တွေကို PHP Language အတွက် သီးသန့် (ဆီလျှော်အောင်) ပြန်လည်မွမ်းမံ စုစည်းပေးထားတာ ဖြစ်ပါတယ်။ ဒါက Coding Style Guideline တစ်ခု မဟုတ်ပါဘူး။ PHP program တွေရေးတဲ့အခါ

- Code တွေ ရှင်းရှင်းလင်းလင်းဖြစ်အောင် (ဝါ) readable ဖြစ်အောင် ၊ 
- Code အစိတ်အပိုင်းများကို တခါရေးပြီးနောက် အခြားနေရာများတွင်လည်း ပြန်လည်အသုံးချနိုင်အောင် (ဝါ) reusable ဖြစ်အောင်၊
- ရှုပ်ထွေးနေတဲ့ Code တွေကို လိုအပ်ရင် အလွယ်တကူ သပ်သပ်ရပ်ရပ် Structure ကျကျ ပြန်လည်ပြင်ဆင်နိုင်တဲ့ (ဝါ) refactorable ဖြစ်အောင်

ရေးသားနိုင်ဖို့ အကူအညီပေးမယ့် လမ်းညွှန်ချက်တစ်ခုဆိုရင် ပိုမှန်ပါလိမ့်မယ်။

ဒီမှာဖော်ပြထားတဲ့ Software ရေးသားနည်း ဥပဒေသတွေကို တသွေမတိမ်း လိုက်နာဖို့တော့ မလိုအပ်ပါဘူး။ တကယ်ဆိုရင် တချို့သော ဥပဒေသတွေကိုသာ နေရာတိုင်းမှာ မှန်တယ်လို့ လက်ခံထားကြတာပါ။ အများစုက သူ့နေရာနဲ့သူ မှန်ကန်အောင် အသုံးချတတ်မှသာ အသုံးဝင်မှာပါ။
ဒီ ဥပဒေသတွေက လမ်းညွှန်တစ်ခုထက် မပိုပါဘူး။ ဒါပေမယ့် ဒီလမ်းညွှန်ချက်တွေက နှစ်ပေါင်းများစွာ code တွေရေးရင်း ရလာတဲ့ အတွေအကြုံတွေကို Clean Code ရဲ့ မူရင်းရေးသားသူက ကြိုးစားပြီး စုစည်းပေးထားတာပါ။

Inspired from [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript).

အခုလက်ရှိ PHP developers တော်တော်များများက PHP 5 ကို သုံးနေဆဲဖြစ်ပေမယ့်၊ Code example တော်တော်များများကိုတော့ PHP 7.1+ သာ စမ်းကြည့်လို့ ရမှာဖြစ်ပါတယ်။

## Variables

### Use meaningful and pronounceable variable names

Variable တွေနာမည်ပေးတဲ့အခါ ထင်ရှားတဲ့ အဓိပ္ပာယ်ရှိပြီး အသံထွက်ဖတ်လို့ရတဲ့ စကားလုံးမျိုးတွေကိုသာ ရွေးချယ်သင့်ပါတယ်။

**မဖြစ်သင့်:**

```php
$ymdstr = $moment->format('y-m-d');
```

**ဖြစ်သင့်:**

```php
$currentDate = $moment->format('y-m-d');
```

**[⬆ back to top](#introduction)**

### Use the same vocabulary for the same type of variable

အမျိုးအစားတူတဲ့ variable တွေအတွက် နာမည်ပေးတဲ့အခါ တူညီတဲ့ ဝေါဟာရတခုတည်းကိုသာ တသတ်မတ်တည်း အသုံးပြုသင့်ပါတယ်။

**မဖြစ်သင့်:**

```php
getUserInfo();
getUserData();
getUserRecord();
getUserProfile();
```

**ဖြစ်သင့်:**

```php
getUser();
```

**[⬆ back to top](#မာတိကာ)**

### Use searchable names (part 1)

ကျွန်တော်တို့ Programmer တွေဟာ Code ရေးလို့ အချိန်ကုန်တာထက်စာရင် ရေးပြီးသား Code ကို နားလည်အောင်ပြန်ဖတ်ရတာအတွက် အချိန်ပိုကုန်လေ့ ရှိပါတယ်။ ဒါကြောင့် ကျွန်တော်တို့ ရေးတဲ့ Code တွေဟာ ပြန်ဖတ်တဲ့အခါ ဖတ်ရလွယ်ကူဖို့နဲ့ လွယ်လင့်တကူပြန်ရှာလို့ရနိုင်ဖို့ အရေးကြီးလှပါတယ်။

ပြန်ရှာတယ်ဆိုတာ - ဥပမာ: Code Line ပေါင်း ၁၀၀၀၀ လောက် ရှိတဲ့ Project ကြီးမှာ User Log In စဝင်တဲ့ အချိန်ကို ဘယ် Variable နဲ့ မှတ်ထားမိလဲဆိုတာ ပြန်ရှာသလိုမျိုးပေါ့။ userLogInTime လို့ variable ကို နာမည်မပေးဘဲ uLInTime လို့ အတိုကောက် ပေးလိုက်ရင် နောက် Maintain လုပ်မယ့် Developer အနေနဲ့ နားလည်ဖို့ အခက်အခဲဖြစ်သွားနိုင်တာကို ဆိုလိုတာပါ။

ဒါကြောင့် variable နာမည်ပေးတဲ့အခါ ပြီးပြီးရောမပေးသင့်ပါဘူး။ ကိုယ်ရေးနေတဲ့ program ကို ပြန်ဖတ်တဲ့အခါ နားလည်လွယ်စေဖို့ ရည်ရွယ်ပြီး သေချာရွေးချယ်ပြီးမှ ပေးသင့်ပါတယ်။ အဲလိုမှ မဟုတ်ရင် ကိုယ့် program ကို ဖတ်မယ့်သူတွေကို အခက်အခဲ များစွာ ဖြစ်ပေါ်စေမှာပါ။ လိုရင်းကတော့ variable နာမည်ကို ပြန်ဖတ်ရင် အဓိပ္ပာယ်ရှိအောင်၊ ပြန်ရှာလို့လွယ်အောင် ပေးပါ။

**မဖြစ်သင့်:**

```php
// 448 ဆိုတာ ဘာကြီးလဲ၊ ဘာကိုဆိုလိုတာလဲ
$result = $serializer->serialize($data, 448);
```

**ဖြစ်သင့်:**

```php
$json = $serializer->serialize($data, JSON_UNESCAPED_SLASHES | JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE);
```

### Use searchable names (part 2)

**မဖြစ်သင့်::**

```php
// 4 ဆိုတာ ဘာကြီးလဲ၊ ဘာကိုရည်ရွယ်ခြင်တာလဲ
if ($user->access & 4) {
    // ...
}
```

**ဖြစ်သင့်:**

```php
class User
{
    const ACCESS_READ = 1;
    const ACCESS_CREATE = 2;
    const ACCESS_UPDATE = 4;
    const ACCESS_DELETE = 8;
}

if ($user->access & User::ACCESS_UPDATE) {
    // do edit ...
}
```

**[⬆ back to top](#မာတိကာ)**

### Use explanatory variables

Variable တွေကို အဓိပ္ပာယ်ပေါ်အောင် နာမည်ကောင်းကောင်း ပေးတတ်ရုံနဲ့ မလုံလောက်သေးပါဘူး။ Variable ကို အသုံးပြုမယ့် scope နဲ့ code statement ပေါ်မူတည်ပြီး မှန်ကန်အောင် ရေးတတ်ရပါသေးတယ်။ Technically အရ Scope in mind လို့ ခေါ်ပါတယ်။ 

Variable ကို အသုံးပြုထားတဲ့ code statement ကို ကြည့်ရုံနဲ့ variable ထဲမှာ ဘာ data သိမ်းပြီး process လုပ်သွားတာလဲ၊ ဘာ ရည်ရွယ်ချက်နဲ့ code statement မှာ သုံးသွားလဲဆိုတဲ့ အဓိပ္ပာယ်ပေါ်အောင်လည်း ရေးတတ်ရပါတယ်။

**မဖြစ်သင့်:**

အောက်ပါ ဥပမာမှာဆို regular expression ကို process လုပ်သွားတဲ့ preg_match function ထဲမှာ ပေးထားတဲ့ $matches ဆိုတဲ့ variable ဟာ သူ အဓိပ္ပာယ်နဲ့သူ မှန်နေပါတယ်။

ဒါပေမယ့် `saveCityZipCode` function မှာ `parameters` အနေနဲ့ပေးတဲ့အခါကျတော့ `$matches[1]`, `$matches[2]` လို့ ပေးလိုက်တာဟာ code statement ကို ဖတ်ရတာ ဝေဝါးသွားစေပါတယ်။ `$matches[1]` ဆိုတာ `$matches` ဆိုတဲ့ `array` ရဲ့ ပထမအခန်းကို ရည်ညွှန်းမှန်းသိပေမယ့် အဲ့ဒီ ပထမအခန်းထဲမှာ ဘာ data သိမ်းထားမှန်းဆိုတာကတော့ မသိရတော့ပါဘူး။ အဲဒီတော့ code ကို maintain လုပ်မယ့်သူက အပေါ်က **regular expression** ကို အသေးစိတ်နားလည်အောင် သွားဖတ်ရပါတော့မယ်။

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(.+?)\s*(\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches[1], $matches[2]);
```

**အသင့်အတင့်:**

အောက်က ပိုမိုကောင်းမွန်အောင် ပြန်လည်ပြင်ဆင်ထားတဲ့ ဥပမာကို ကြည့်ပါဦး။

ဒီဥပမာမှာတော့ `saveCityZipCode` function ရေးသားပုံက ကောင်းမွန်သွားပါပြီ။ ဒါပေသိ `[, $city, $zipCode] = $matches` ဆိုတဲ့ code line ဟာ code နားလည်လွယ်အောင် အပိုရေးလိုက်ရတဲ့ code တစ်ကြောင်းပုံစံ ဖြစ်သွားပါတယ်။ တကယ့် ရှုပ်ထွေးမှုတွေကို ဖြစ်ပေါ်စေတဲ့ **regular expression** ကို မရှင်းဘဲ code အပိုတစ်ကြောင်း ရေးလိုက်သလို ဖြစ်သွားတာပါ။

စာခြွင်း။ ။ တကယ့်လက်တွေ့မှာတော့ ဒီဥပမာက code ရေးသားမှုပုံစံဟာ လက်သင့်ခံလို့ ရပါတယ်။ အခုလောက် ရှင်းလင်းသပ်ရပ်မှု ရှိပြီဆိုရင် မဆိုးဘူးလို့ ပြောလို့ရပါပြီ။ ဘာဖြစ်လို့လဲဆိုရင် တကယ်လက်တွေ့ Project တွေမှာက အချိန်ဒီလောက် မပေးပါဘူး။ refactoring လုပ်ရင်း feature အသစ်ရေးရမယ့် အချိန်တွေပါ ကုန်သွားမှာကိုလည်း ဆင်ခြင်သင့်ပါတယ်။

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(.+?)\s*(\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

[, $city, $zipCode] = $matches;
saveCityZipCode($city, $zipCode);
```

**ဖြစ်သင့်:**

အခု ဥပမာမှာတော့ code ရေးသားမှုဟာ အကောင်းဆုံးပုံစံကို ရောက်ရှိသွားပြီလို့ ယူဆလို့ ရပါတယ်။ တကယ့် ရှုပ်ထွေးမှုကို ဖြစ်စေတဲ့ **regular expression** ကို ရှင်းလင်းအောင် `subpattern` တွေကို (naming) နာမည်ပေးပြီး ဖြေရှင်းလိုက်နိုင်ပါတယ်။  code ရေးသားမှုမှာလည်း အပိုအလို မရှိ ကျစ်လစ်သွားပါတယ်။

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(?<city>.+?)\s*(?<zipCode>\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches['city'], $matches['zipCode']);
```

**[⬆ back to top](#မာတိကာ)**

### Avoid nesting too deeply and return early (part 1)

Nested if-else statement တွေကို တတ်နိုင်သလောက် ရှောင်ပါ။ return statement တွေ အများကြီး ပြန်တာမျိုးတွေကိုလည်း ရှောင်ပါ။ (အပိုင်း ၁)

if-else statement တွေ သိပ်များသွားရင် code ကို trace လိုက်ရတာ ခက်ခဲသွားစေပါတယ်။ နောက်တစ်ခု ယူဆလို့ ရတာက ကိုယ့် ရေးတဲ့ function ထဲမှာ if-else statement တွေ ၂ ခု ၃ ခုထက် ပိုနေပြီဆိုရင် ကိုယ့် function က အလုပ်တစ်ခုထက် မက လုပ်နေပြီလို့ ယူဆလို့ ရပါတယ်။ function တစ်ခုက လုပ်ဆောင်ချက် တစ်ခုဘဲ ရှိသင့်ပါတယ်။ ဒီလို အခါမျိုးမှာ Polymorphism (သို့) State/Strategy pattern နဲ့ ပြန်ပြီး code ကို refactor လုပ်လို့ ရပါတယ်။

function တစ်ခုကနေ return statement တွေ အများကြီး ပြန်တာမျိုးတွေကိုလည်း ရှောင်သင့်ပါတယ်။ ဒီအချက်ကလည်း function တစ်ခုကို trace လိုက်ရတာ အတော်လေး ခက်ခဲသွားစေနိုင်တဲ့ အချက်ပါ။ return statement အများဆုံး ဘယ်လောက်ဘဲ ရှိသင့်တယ်လို့တော့ အတိအကျ သတ်မှတ်ထားတာ မရှိပါဘူး။ နည်းနိုင်သမျှ နည်းတာတော့ ကောင်းပါတယ်။

Returning early ဆိုတဲ့ အယူအဆ မျိုးတော့ ရှိပါတယ်။ ဥပမာ - file download လုပ်တဲ့ function တစ်ခုမှာ Internet connection မရှိရင် exception တက်တာဘဲဖြစ်ဖြစ်၊ return false ပြန်တာဘဲဖြစ်ဖြစ်ကို function ရဲ့ အပေါ်ဆုံး code line တွေမှာ ရေးလို့ ရပါတယ်။ ဒါပေမယ့် function ကို ဖတ်ရတာ ပိုကောင်းသွားစေတယ်လို့ သေချာမှသာ ဒီလိုမျိုး ရေးသင့်ပါတယ်။

စာခြွင်း ရှင်းလင်းချက်:
trace လိုက်တယ်ဆိုတာ code တကြောင်းခြင်းစီက ဘာအလုပ်လုပ်သွားလဲ၊ ဘာ output ထွက်သွားလဲဆိုတာ လိုက်ကြည့်တယ်လို့ ယေဘုယျနားလည်လို့ ရပါတယ်။ PHP မှာဆိုရင် xdebug နဲ့ debug လိုက်ကြည့်သလိုမျိုး၊ var_dump နဲ့ print ထုတ်ကြည့်သလိုမျိုးပေါ့။ ဒီလို tools တွေနဲ့ မဟုတ်ဘဲ စိတ်ထဲမှာဘဲဖြစ်စေ၊ စာအုပ်ပေါ်မှာ ချရေးပြီးတော့ ဖြစ်စေ step by step စိတ်မှန်းနဲ့လည်း trace လိုက်သွားတာမျိုးလည်း ရှိပါတယ်။ အဲဒါကို term အရ Dry Run လို့ ခေါ်ပါတယ်။

ပုံမှန် trace ကို code ရဲ့ ဘယ်နားက error တက်သွားလဲဆိုတာသိဖို့ လိုက်ကြတာ များပါတယ်။ သို့မဟုတ် သူများရေးထားတဲ့ (ကိုယ်အရင်က ရေးထားပေမယ့် မေ့သွားတဲ့) code တွေကို နားလည်အောင် ပြန် ဖတ်တဲ့ အခါမျိုးမှာလည်း သုံးပါတယ်။

**မဖြစ်သင့်:**

```php
function isShopOpen($day): bool
{
    if ($day) {
        if (is_string($day)) {
            $day = strtolower($day);
            if ($day === 'friday') {
                return true;
            } elseif ($day === 'saturday') {
                return true;
            } elseif ($day === 'sunday') {
                return true;
            } else {
                return false;
            }
        } else {
            return false;
        }
    } else {
        return false;
    }
}
```

**ဖြစ်သင့်:**

```php
function isShopOpen(string $day): bool
{
    if (empty($day)) {
        return false;
    }

    $openingDays = [
        'friday', 'saturday', 'sunday'
    ];

    return in_array(strtolower($day), $openingDays, true);
}
```

**[⬆ back to top](#မာတိကာ)**

### Avoid nesting too deeply and return early (part 2)

**မဖြစ်သင့်:**

```php
function fibonacci(int $n)
{
    if ($n < 50) {
        if ($n !== 0) {
            if ($n !== 1) {
                return fibonacci($n - 1) + fibonacci($n - 2);
            } else {
                return 1;
            }
        } else {
            return 0;
        }
    } else {
        return 'Not supported';
    }
}
```

**ဖြစ်သင့်:**

```php
function fibonacci(int $n): int
{
    if ($n === 0 || $n === 1) {
        return $n;
    }

    if ($n > 50) {
        throw new \Exception('Not supported');
    }

    return fibonacci($n - 1) + fibonacci($n - 2);
}
```

**[⬆ back to top](#မာတိကာ)**

### Avoid Mental Mapping

ဒီအချက်ကတော့ အပေါ်ကအချက်တွေကိုဘဲ မူကွဲပုံစံ တစ်မျိုးနဲ့ ပြောထားတာပါ။
Variable တစ်ခုကို နားလည်ဖို့ သူ့ထဲမှာ သိမ်းထားတဲ့ data ကို သွားဖတ်ပြီးမှ သိရတာမျိုးက မကောင်းပါဘူး။ ရှင်းလင်းပြတ်သားခြင်းက သွယ်ဝိုက်နေတာထက် ပိုကောင်းပါတယ်။

**မဖြစ်သင့်:**

```php
$l = ['Austin', 'New York', 'San Francisco'];

for ($i = 0; $i < count($l); $i++) {
    $li = $l[$i];
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    // Wait, what is `$li` for again?
    dispatch($li);
}
```

**ဖြစ်သင့်:**

```php
$locations = ['Austin', 'New York', 'San Francisco'];

foreach ($locations as $location) {
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    dispatch($location);
}
```

**[⬆ back to top](#မာတိကာ)**

### Don't add unneeded context

ဖော်ပြခဲ့သမျှ အချက်တွေကတော့ Variable နာမည် ပေးတဲ့အခါ တတ်နိုင်သမျှ ပြည့်စုံရှင်းလင်းအောင် ရေးဖို့ ပြောထားတာပါ။
ဒါပေမယ့် မလိုအပ်ဘဲ စကားဆက် (context) တွေ မထည့်မိဖို့လည်း အရေးကြီးပါတယ်။

ဥပမာပေးရမယ်ဆိုရင် class/object ထဲက member variable တိုင်းမှာ class နာမည်ကြီးကို ရှေ့က လိုက်ထည့်နေတာမျိုးပါ။ "User" class ထဲမှာ user ရဲ့ အသက်ကိုသိမ်းဖို့ variable ကို နာမည်ပေးတဲ့အခါ age ဆိုရင် လုံလောက်ပါပြီ။ userAge ဆိုပြီး စကားဆက် (context) ကို ရှေ့ကခံပေးစရာ မလိုပါဘူး။ ဘာဖြစ်လို့လဲဆိုရင်အဲ့ဒီ age ဆိုတဲ့ member variable ကို ခေါ်သုံးတဲ့အခါ `user->age` ဆိုပြီး ခေါ်သုံးရမှာ ဖြစ်လို့ပါ။  `user->age` ဆိုတဲ့ code expression ကို ကြည့်မယ်ဆိုရင် user ရဲ့ age ကို ရည်ညွှန်းမှန်း သိသာပါတယ်။ 

**မဖြစ်သင့်:**

```php
class Car
{
    public $carMake;
    public $carModel;
    public $carColor;

    //...
}
```

**ဖြစ်သင့်:**

```php
class Car
{
    public $make;
    public $model;
    public $color;

    //...
}
```

**[⬆ back to top](#မာတိကာ)**

### Use default arguments instead of short circuiting or conditionals

Programmer တွေအနေနဲ့ Function တွေကို ရေးတဲ့အခါတိုင်း parameter declaration ဆိုတာကို တနည်းမဟုတ်တနည်းနဲ့တော့ ကြုံကြရတာပါဘဲ။

Parameter ကြေငြာတဲ့အခါ အဲဒီ parameter အတွက် default value သတ်မှတ်ပေးဖို့ လိုအပ်တဲ့အခါတိုင်း default argument ကြေငြာတဲ့ပုံစံမျိုးနဲ့ဘဲ ရေးသင့်ပါတယ်။ **Ternary conditional** ပုံစံတွေ၊ **short circuiting** ပုံစံတွေနဲ့ မရေးသင့်ပါဘူး။

စာခြွင်း။ ။ **short circuiting** ဆိုတဲ့ term က တချို့သော developer တွေအတွက် အနည်းငယ် စိမ်းနေနိုင်ပါတယ်။ ဒီ [wiki link](https://en.wikipedia.org/wiki/Short-circuit_evaluation) နဲ့ [stackoverflow link](https://stackoverflow.com/questions/9344305/what-is-short-circuiting-and-how-is-it-used-when-programming-in-java) မှာတော့ ရှင်းထားတာ အတော်လေး ကောင်းပါတယ်။

**မဖြစ်သင့်:**

ဒီရေးသားမှုပုံစံဟာ လိုအပ်ချက်ရှိနေသေးတယ်လို့ ယူဆလို့ရပါတယ်။ အောက်ပါ function ကိုသာ `$this->createMicrobrewery(null)` နဲ့ call လိုက်ရင် `$breweryName` ဟာ ဖြစ်စေခြင်တဲ့ default value “Hipster Brew Co.” အစား `null` value ဝင်သွားမှာပါ။

စာခြွင်း။ ။ ကိုယ်ပိုင်အမြင်အရဆိုရင် ဒီရေးသားမှုပုံစံဟာ function ရဲ့ argument control ကို လျှော့ကျသွားတယ် ဆိုရုံလောက်ဘဲ ယူဆလို့ ရတာပါ။ **PHP** လို *dynamic typing language* တစ်ခုမှာ function parameter တစ်ခုကို `null` value ဝင်တာနဲ့ မကောင်းဘူးပြောဖို့ဆိုတာ အနည်းငယ် တဖက်သက်ဆန်တယ်လို့ ခံစားမိပါတယ်။

```php
function createMicrobrewery($breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**အသင့်အတင့်:**

ဒီရေးသားမှုပုံစံကတော့ မဆိုးဘူးလို့ ပြောလို့ရပါပြီ။ default value ကို `null` လို့ ထားလိုက်တယ်။ ပြီးမှ function body ထဲမှာ **ternary operator** နဲ့ `null` ဖြစ်ခဲ့ရင် actual default value “Hipster Brew Co.” ထည့်မယ်ဆိုပြီး ရေးလိုက်ပါတယ်။

ဒါကြောင့် argument မသတ်မှတ်ဘဲ function call လိုက်သည်ဖြစ်စေ၊ `null` or `empty value` ပေးလိုက်သည်ဖြစ်စေ `$breweryName` parameter ဟာ actual default value “Hipster Brew Co.” ရှိနေတော့မှာပါ။

စာခြွင်း။ ။ ဒီ ရေးသားမှုမှာလည်း မိမိကိုယ်ပိုင်အမြင်အရဆိုရင် အရမ်းကြီး သဘောမတူခြင်ပါဘူး။ default argument ဆိုတာ `null` value ကို ရှောင်ခြင်လို့ ရေးရတာမျိုး မဟုတ်ပါဘူး။ function call တဲ့ အချိန်မှာ လိုအပ်တဲ့ parameter အတွက် argument မပေးခဲ့ဘူးဆိုရင် logic အရ default value တစ်ခု သတ်မှတ်ပေးလိုက်တဲ့ သဘောပါ။

```php
function createMicrobrewery($name = null): void
{
    $breweryName = $name ?: 'Hipster Brew Co.';
    // ...
}
```

**ဖြစ်သင့်:**

ဒီ ရေးသားမှုမှာတော့ Php7 ရဲ့ [type hinting](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration) feature ကို အသုံးပြုပြီး argument ကို **string datatype** နဲ့ restrict လုပ်လိုက်ပါတယ်။ ဒါကြောင့် `null` value ဝင်လာခဲ့ရင် `exception` တက်မှာပါ။

`null` value ဖြစ်မှာလည်း စိုးရိမ်စရာ မလိုတော့သလို default argument လည်း ကြေငြာပြီးသား ဖြစ်သွားစေတဲ့အတွက် ကောင်းမွန်တဲ့ ရေးသားမှုတစ်ခုလို့ ဆိုလို့ရပါတယ်။

```php
function createMicrobrewery(string $breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**[⬆ back to top](#မာတိကာ)**

## Comparison

### Use [identical comparison](http://php.net/manual/en/language.operators.comparison.php)
Php မှာ == (equality) နဲ့ === (identical) ဆိုပြီး comparison operator နှစ်မျိုးရှိတာ developer တိုင်း သိကြမှာပါ။ Php မှာ == (equality) နဲ့ === (identical) ဆိုပြီး comparison operator နှစ်မျိုးရှိတာ developer တိုင်း သိကြမှာပါ။ == (equality) comparison နဲ့ condition စစ်ရင် operands တွေကို type juggling လုပ်လိုက်ပါတယ်။ === (identical) comparison မှာတော့ type juggling မလုပ်ပါဘူး။

Type juggling rules အသေးစိတ်ကိုတော့ [php official documentation](http://php.net/manual/en/language.operators.comparison.php) မှာ သွားဖတ်လို့ ရပါတယ်။

Type juggling လုပ်တဲ့ rules တွေက အနည်းငယ် ရှုပ်ထွေးပြီး အလွတ်မှတ်ထား နိုင်ဖို့လည်း မလွယ်လှပါဘူး။ ဒါကြောင့် == (equality) operator နဲ့ရေးတဲ့ comparison expression တွေမှာ ကိုယ်မမျှော်လင့်ထားတဲ့ result တွေ ထွက်လာနိုင်ပါတယ်။

ဖြစ်နိုင်ရင်တော့ condition စစ်တိုင်း (===) identical comparison operator ကိုသာ သုံးသင့်ပါတယ်။

**မဖြစ်သင့်:**

အောက်ပါ code block မှာဆိုရင် (==) equality comparison operator က string ကို integer ပြောင်းလိုက်ပါတယ်။

```php
$a = '42';
$b = 42;

if ($a != $b) {
   // The expression will always pass
}
```

*string* `42` နဲ့ *integer* `42` ဟာ computational logic အရ ဆိုရင် မတူပါဘူး။ ဒါပေမယ့် `$a != $b` လို့ comparison လုပ်လိုက်ရင်တော့ `FALSE` return ပြန်လာတာကို တွေ့ရမှာပါ။

ဘာဖြစ်လို့လဲဆိုရင် သူတို့နှစ်ခုကို (==) equality operator က type juggling လုပ်လိုက်တဲ့အတွက် *string* `42` က *integer* ဖြစ်သွားပါတယ်။ ဒါကြောင့် သူတို့နှစ်ခုကို comparison လုပ်တဲ့အခါ တူတယ်ဆိုတဲ့အဖြေဆိုတဲ့ ထွက်လာစေတာပါ။

**ဖြစ်သင့်:**

(===) identical operator ကတော့ operand တွေရဲ့ datatype မတူရင် value comparison ကို မလုပ်ဆောင်တော့ပါဘူး။

```php
$a = '42';
$b = 42;

if ($a !== $b) {
    // The expression is verified
}
```

အထက်ပါ code block မှာတော့ မျှော်လင့်ထားတဲ့အတိုင်း `TRUE` ကို ရရှိမှာဘဲ ဖြစ်ပါတယ်။

**[⬆ back to top](#မာတိကာ)**


## Functions

### Function arguments (2 or fewer ideally)

Function parameters အရေအတွက်ကို ကန့်သတ်ထားဖို့က အရမ်း အရေးကြီးပါတယ်။ Function parameters နည်းတဲ့အခါ အဲဒီ function အတွက် testing ရေးရတာ ပိုလွယ်ကူတာကို တွေ့ရမှာပါ။
Parameters ၃ ခုထက် ကျော်သွားရင် parameter တစ်ခုခြင်းစီအတွက် မတူတဲ့ value တစ်ခုခြင်းစီနဲ့ Test case တွေ လိုက်ရေးပေးနေရတဲ့အတွက် Test case တွေ အများကြီး ဖောင်းပွသွားနိုင်တာကို သတိချပ်သင့်ပါတယ်။

Zero argument (argument တစ်ခုမှ မလိုတဲ့ function) က အကောင်းဆုံးပါ။ Argument ၁ ခု (သို့) ၂ ခု လောက်ထိ အဆင်ပြေပါတယ်။ ၃ ခု ဆိုရင်တော့ စတင် သတိထားပြီး ရှောင်ရှားသင့်ပါပြီ။ အဲဒါထက် ပိုများသွားပြီဆိုရင်တော့ function ကို ပြန်ပြင်ရေးသင့်နေပါပြီ။ Argument ၂ ခုထက် ပိုနေတာဟာ အဲဒီ function က အလုပ်တစ်ခုထက်မက လုပ်နေပြီလို့ ယူဆလို့ ရပါတယ်။ အကယ်၍ ၃ ခုထက် ပိုတဲ့ argument တွေက context တစ်ခုတည်းအောက်မှာ ရှိနေတဲ့အခါမျိုးမှာတော့ object တစ်ခု အစားတည်ဆောက်ပြီး pass ပေးသင့်ပါတယ်။

အောက်ပါ ဥပမာကို လေ့လာကြည့်လို့ ရပါတယ်။ Menu တစ်ခု တည်ဆောက်ဖို့ parameter ၄ ခု pass ပေးမယ့်အစား MenuConfig ဆိုတဲ့ object တစ်ခု တည်ဆောက်ပြီး createMenu function ကို pass ပေးလိုက်တာ တွေ့ရမှာပါ။

**မဖြစ်သင့်:**

```php
function createMenu(string $title, string $body, string $buttonText, bool $cancellable): void
{
    // ...
}
```

**ဖြစ်သင့်:**

```php
class MenuConfig
{
    public $title;
    public $body;
    public $buttonText;
    public $cancellable = false;
}

$config = new MenuConfig();
$config->title = 'Foo';
$config->body = 'Bar';
$config->buttonText = 'Baz';
$config->cancellable = true;

function createMenu(MenuConfig $config): void
{
    // ...
}
```

**[⬆ back to top](#မာတိကာ)**

### Functions should do one thing

ဒါကတော့ software engineering မှာ လိုက်နာသင့်တဲ့ အရေးကြီးဆုံး စည်းကမ်း တစ်ခုပါဘဲ။ အလုပ်တစ်ခုထက်ပိုတဲ့ Functions တွေ ရေးမိတဲ့အခါ program ကို အစဉ်တကျဆက်ရေးဖို့ ခက်သွားစေပါတယ်။ ဒုတိယအချက်အနေနဲ့ test case တွေ ရေးရတာလည်း မလွယ်တော့ပါဘူး။ Function က အလုပ်တစ်ခုထက် ပိုလုပ်တဲ့အတွက် အဲဒါကို cover ဖြစ်ဖို့ function အတွက် test cases တွေ အများကြီး လိုက်ရေးရတော့တာပါဘဲ။ တတိယအချက်ကတော့ reason to change တစ်ခုထက် ပိုသွားတာပါဘဲ။ Function တစ်ခုဟာ program ထဲမှာ သူတည်ရှိနေရခြင်း ရည်ရွယ်ချက် တစ်ခုဘဲ ရှိသင့်ပါတယ်။ အဲ့ဒါကို reason to change လို့ ခေါ်ကြပါတယ်။

Function တွေကို လုပ်ဆောင်ချက် တစ်ခုတည်းကိုသာလုပ်ဖို့ ကန့်သတ်ရေးသားနိုင်မယ်ဆိုရင် refactor လုပ်ရလွယ်သလို code တွေကလည်း အတော်လေး ရှင်းလင်းသွားပါလိမ့်မယ်။ အကယ်လို့ ဒီ guide ထဲက တခြားလမ်းညွှန်ချက်တွေကို မေ့ခြင်မေ့၊ ဒီတစ်ချက်ကိုတော့ သေချာပေါက် မှတ်ထားဖို့ လိုပါတယ်။ ဒီ တစ်ချက်ကို လိုက်နာနိုင်ယုံနဲ့တင် ပုံမှန် developers တွေရေးတဲ့ code ထက် အများကြီးသာတဲ့ clean code ကို ရေးနိုင်သွားမှာပါ။

စကားချပ်။ ။ ဒီမှာ တစ်ခုရှိနိုင်တာက လုပ်ဆောင်ချက်တစ်ခုတည်းလုပ်တယ်ဆိုတာ ဘာကို ပြောတာလဲဆိုပြီး မေးခွန်းထုတ်နိုင်ပါတယ်။ Function body ထဲမှာ ရှိတဲ့ code တွေ အားလုံးဟာ abstraction level တစ်ခုတည်းအောက်မှာ ရှိနေပြီး final output result တစ်ခုတည်းရှိနေခြင်းကို ဆိုလိုပါတယ်။

ဥပမာ - harddisk ပေါ်မှာ file သိမ်းတဲ့ function တစ်ခုကိုရေးမယ်ဆိုရင် code line တွေ အများကြီး ပါဝင်နိုင်ပေမယ့် သူတို့အားလုံးရဲ့ ရည်ရွယ်ချက်ကတော့ နောက်ဆုံးမှာ file သိမ်းသွားဖို့ပါဘဲ။ cloud ပေါ်မှာ file သိမ်းတဲ့ လုပ်ဆောင်ချက်ကိုပါ ထည့်ရေးလိုက်ရင် ဒါလုပ်ဆောင်ချက်တစ်ခုထက်ပိုတဲ့ function တစ်ခု ဖြစ်သွားပါလိမ့်မယ်။ 

**မဖြစ်သင့်:**
```php
function emailClients(array $clients): void
{
    foreach ($clients as $client) {
        $clientRecord = $db->find($client);
        if ($clientRecord->isActive()) {
            email($client);
        }
    }
}
```

**ဖြစ်သင့်:**

```php
function emailClients(array $clients): void
{
    $activeClients = activeClients($clients);
    array_walk($activeClients, 'email');
}

function activeClients(array $clients): array
{
    return array_filter($clients, 'isClientActive');
}

function isClientActive(int $client): bool
{
    $clientRecord = $db->find($client);

    return $clientRecord->isActive();
}
```

**[⬆ back to top](#မာတိကာ)**

### Function names should say what they do

**Bad:**

```php
class Email
{
    //...

    public function handle(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// What is this? A handle for the message? Are we writing to a file now?
$message->handle();
```

**Good:**

```php
class Email 
{
    //...

    public function send(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// Clear and obvious
$message->send();
```

**[⬆ back to top](#မာတိကာ)**

### Functions should only be one level of abstraction

When you have more than one level of abstraction your function is usually
doing too much. Splitting up functions leads to reusability and easier
testing.

**Bad:**

```php
function parseBetterJSAlternative(string $code): void
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            // ...
        }
    }

    $ast = [];
    foreach ($tokens as $token) {
        // lex...
    }

    foreach ($ast as $node) {
        // parse...
    }
}
```

**Bad too:**

We have carried out some of the functionality, but the `parseBetterJSAlternative()` function is still very complex and not testable.

```php
function tokenize(string $code): array
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            $tokens[] = /* ... */;
        }
    }

    return $tokens;
}

function lexer(array $tokens): array
{
    $ast = [];
    foreach ($tokens as $token) {
        $ast[] = /* ... */;
    }

    return $ast;
}

function parseBetterJSAlternative(string $code): void
{
    $tokens = tokenize($code);
    $ast = lexer($tokens);
    foreach ($ast as $node) {
        // parse...
    }
}
```

**Good:**

The best solution is move out the dependencies of `parseBetterJSAlternative()` function.

```php
class Tokenizer
{
    public function tokenize(string $code): array
    {
        $regexes = [
            // ...
        ];

        $statements = explode(' ', $code);
        $tokens = [];
        foreach ($regexes as $regex) {
            foreach ($statements as $statement) {
                $tokens[] = /* ... */;
            }
        }

        return $tokens;
    }
}

class Lexer
{
    public function lexify(array $tokens): array
    {
        $ast = [];
        foreach ($tokens as $token) {
            $ast[] = /* ... */;
        }

        return $ast;
    }
}

class BetterJSAlternative
{
    private $tokenizer;
    private $lexer;

    public function __construct(Tokenizer $tokenizer, Lexer $lexer)
    {
        $this->tokenizer = $tokenizer;
        $this->lexer = $lexer;
    }

    public function parse(string $code): void
    {
        $tokens = $this->tokenizer->tokenize($code);
        $ast = $this->lexer->lexify($tokens);
        foreach ($ast as $node) {
            // parse...
        }
    }
}
```

**[⬆ back to top](#မာတိကာ)**

### Don't use flags as function parameters

Flags tell your user that this function does more than one thing. Functions should 
do one thing. Split out your functions if they are following different code paths 
based on a boolean.

**Bad:**

```php
function createFile(string $name, bool $temp = false): void
{
    if ($temp) {
        touch('./temp/'.$name);
    } else {
        touch($name);
    }
}
```

**Good:**

```php
function createFile(string $name): void
{
    touch($name);
}

function createTempFile(string $name): void
{
    touch('./temp/'.$name);
}
```

**[⬆ back to top](#မာတိကာ)**

### Avoid Side Effects

A function produces a side effect if it does anything other than take a value in and 
return another value or values. A side effect could be writing to a file, modifying 
some global variable, or accidentally wiring all your money to a stranger.

Now, you do need to have side effects in a program on occasion. Like the previous 
example, you might need to write to a file. What you want to do is to centralize where 
you are doing this. Don't have several functions and classes that write to a particular 
file. Have one service that does it. One and only one.

The main point is to avoid common pitfalls like sharing state between objects without
any structure, using mutable data types that can be written to by anything, and not 
centralizing where your side effects occur. If you can do this, you will be happier 
than the vast majority of other programmers.

**Bad:**

```php
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
$name = 'Ryan McDermott';

function splitIntoFirstAndLastName(): void
{
    global $name;

    $name = explode(' ', $name);
}

splitIntoFirstAndLastName();

var_dump($name); // ['Ryan', 'McDermott'];
```

**Good:**

```php
function splitIntoFirstAndLastName(string $name): array
{
    return explode(' ', $name);
}

$name = 'Ryan McDermott';
$newName = splitIntoFirstAndLastName($name);

var_dump($name); // 'Ryan McDermott';
var_dump($newName); // ['Ryan', 'McDermott'];
```

**[⬆ back to top](#မာတိကာ)**

### Don't write to global functions

Polluting globals is a bad practice in many languages because you could clash with another 
library and the user of your API would be none-the-wiser until they get an exception in 
production. Let's think about an example: what if you wanted to have configuration array?
You could write global function like `config()`, but it could clash with another library 
that tried to do the same thing.

**Bad:**

```php
function config(): array
{
    return  [
        'foo' => 'bar',
    ]
}
```

**Good:**

```php
class Configuration
{
    private $configuration = [];

    public function __construct(array $configuration)
    {
        $this->configuration = $configuration;
    }

    public function get(string $key): ?string
    {
        return isset($this->configuration[$key]) ? $this->configuration[$key] : null;
    }
}
```

Load configuration and create instance of `Configuration` class 

```php
$configuration = new Configuration([
    'foo' => 'bar',
]);
```

And now you must use instance of `Configuration` in your application.

**[⬆ back to top](#မာတိကာ)**

### Don't use a Singleton pattern

Singleton is an [anti-pattern](https://en.wikipedia.org/wiki/Singleton_pattern). Paraphrased from Brian Button:
 1. They are generally used as a **global instance**, why is that so bad? Because **you hide the dependencies** of your application in your code, instead of exposing them through the interfaces. Making something global to avoid passing it around is a [code smell](https://en.wikipedia.org/wiki/Code_smell).
 2. They violate the [single responsibility principle](#single-responsibility-principle-srp): by virtue of the fact that **they control their own creation and lifecycle**.
 3. They inherently cause code to be tightly [coupled](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29). This makes faking them out under **test rather difficult** in many cases.
 4. They carry state around for the lifetime of the application. Another hit to testing since **you can end up with a situation where tests need to be ordered** which is a big no for unit tests. Why? Because each unit test should be independent from the other.

There is also very good thoughts by [Misko Hevery](http://misko.hevery.com/about/) about the [root of problem](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/).

**Bad:**

```php
class DBConnection
{
    private static $instance;

    private function __construct(string $dsn)
    {
        // ...
    }

    public static function getInstance(): DBConnection
    {
        if (self::$instance === null) {
            self::$instance = new self();
        }

        return self::$instance;
    }

    // ...
}

$singleton = DBConnection::getInstance();
```

**Good:**

```php
class DBConnection
{
    public function __construct(string $dsn)
    {
        // ...
    }

     // ...
}
```

Create instance of `DBConnection` class and configure it with [DSN](http://php.net/manual/en/pdo.construct.php#refsect1-pdo.construct-parameters).

```php
$connection = new DBConnection($dsn);
```

And now you must use instance of `DBConnection` in your application.

**[⬆ back to top](#မာတိကာ)**

### Encapsulate conditionals

**Bad:**

```php
if ($article->state === 'published') {
    // ...
}
```

**Good:**

```php
if ($article->isPublished()) {
    // ...
}
```

**[⬆ back to top](#မာတိကာ)**

### Avoid negative conditionals

**Bad:**

```php
function isDOMNodeNotPresent(\DOMNode $node): bool
{
    // ...
}

if (!isDOMNodeNotPresent($node))
{
    // ...
}
```

**Good:**

```php
function isDOMNodePresent(\DOMNode $node): bool
{
    // ...
}

if (isDOMNodePresent($node)) {
    // ...
}
```

**[⬆ back to top](#မာတိကာ)**

### Avoid conditionals

This seems like an impossible task. Upon first hearing this, most people say,
"how am I supposed to do anything without an `if` statement?" The answer is that
you can use polymorphism to achieve the same task in many cases. The second
question is usually, "well that's great but why would I want to do that?" The
answer is a previous clean code concept we learned: a function should only do
one thing. When you have classes and functions that have `if` statements, you
are telling your user that your function does more than one thing. Remember,
just do one thing.

**Bad:**

```php
class Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        switch ($this->type) {
            case '777':
                return $this->getMaxAltitude() - $this->getPassengerCount();
            case 'Air Force One':
                return $this->getMaxAltitude();
            case 'Cessna':
                return $this->getMaxAltitude() - $this->getFuelExpenditure();
        }
    }
}
```

**Good:**

```php
interface Airplane
{
    // ...

    public function getCruisingAltitude(): int;
}

class Boeing777 implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getPassengerCount();
    }
}

class AirForceOne implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude();
    }
}

class Cessna implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getFuelExpenditure();
    }
}
```

**[⬆ back to top](#မာတိကာ)**

### Avoid type-checking (part 1)

PHP is untyped, which means your functions can take any type of argument.
Sometimes you are bitten by this freedom and it becomes tempting to do
type-checking in your functions. There are many ways to avoid having to do this.
The first thing to consider is consistent APIs.

**Bad:**

```php
function travelToTexas($vehicle): void
{
    if ($vehicle instanceof Bicycle) {
        $vehicle->pedalTo(new Location('texas'));
    } elseif ($vehicle instanceof Car) {
        $vehicle->driveTo(new Location('texas'));
    }
}
```

**Good:**

```php
function travelToTexas(Traveler $vehicle): void
{
    $vehicle->travelTo(new Location('texas'));
}
```

**[⬆ back to top](#မာတိကာ)**

### Avoid type-checking (part 2)

If you are working with basic primitive values like strings, integers, and arrays,
and you use PHP 7+ and you can't use polymorphism but you still feel the need to
type-check, you should consider
[type declaration](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration)
or strict mode. It provides you with static typing on top of standard PHP syntax.
The problem with manually type-checking is that doing it will require so much
extra verbiage that the faux "type-safety" you get doesn't make up for the lost
readability. Keep your PHP clean, write good tests, and have good code reviews.
Otherwise, do all of that but with PHP strict type declaration or strict mode.

**Bad:**

```php
function combine($val1, $val2): int
{
    if (!is_numeric($val1) || !is_numeric($val2)) {
        throw new \Exception('Must be of type Number');
    }

    return $val1 + $val2;
}
```

**Good:**

```php
function combine(int $val1, int $val2): int
{
    return $val1 + $val2;
}
```

**[⬆ back to top](#မာတိကာ)**

### Remove dead code

Dead code is just as bad as duplicate code. There's no reason to keep it in
your codebase. If it's not being called, get rid of it! It will still be safe
in your version history if you still need it.

**Bad:**

```php
function oldRequestModule(string $url): void
{
    // ...
}

function newRequestModule(string $url): void
{
    // ...
}

$request = newRequestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**Good:**

```php
function requestModule(string $url): void
{
    // ...
}

$request = requestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**[⬆ back to top](#မာတိကာ)**


## Objects and Data Structures

### Use object encapsulation

In PHP you can set `public`, `protected` and `private` keywords for methods. 
Using it, you can control properties modification on an object. 

* When you want to do more beyond getting an object property, you don't have
to look up and change every accessor in your codebase.
* Makes adding validation simple when doing a `set`.
* Encapsulates the internal representation.
* Easy to add logging and error handling when getting and setting.
* Inheriting this class, you can override default functionality.
* You can lazy load your object's properties, let's say getting it from a
server.

Additionally, this is part of [Open/Closed](#openclosed-principle-ocp) principle.

**Bad:**

```php
class BankAccount
{
    public $balance = 1000;
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->balance -= 100;
```

**Good:**

```php
class BankAccount
{
    private $balance;

    public function __construct(int $balance = 1000)
    {
      $this->balance = $balance;
    }

    public function withdraw(int $amount): void
    {
        if ($amount > $this->balance) {
            throw new \Exception('Amount greater than available balance.');
        }

        $this->balance -= $amount;
    }

    public function deposit(int $amount): void
    {
        $this->balance += $amount;
    }

    public function getBalance(): int
    {
        return $this->balance;
    }
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->withdraw($shoesPrice);

// Get balance
$balance = $bankAccount->getBalance();
```

**[⬆ back to top](#မာတိကာ)**

### Make objects have private/protected members

* `public` methods and properties are most dangerous for changes, because some outside code may easily rely on them and you can't control what code relies on them. **Modifications in class are dangerous for all users of class.**
* `protected` modifier are as dangerous as public, because they are available in scope of any child class. This effectively means that difference between public and protected is only in access mechanism, but encapsulation guarantee remains the same. **Modifications in class are dangerous for all descendant classes.**
* `private` modifier guarantees that code is **dangerous to modify only in boundaries of single class** (you are safe for modifications and you won't have [Jenga effect](http://www.urbandictionary.com/define.php?term=Jengaphobia&defid=2494196)).

Therefore, use `private` by default and `public/protected` when you need to provide access for external classes.

For more informations you can read the [blog post](http://fabien.potencier.org/pragmatism-over-theory-protected-vs-private.html) on this topic written by [Fabien Potencier](https://github.com/fabpot).

**Bad:**

```php
class Employee
{
    public $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->name; // Employee name: John Doe
```

**Good:**

```php
class Employee
{
    private $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    public function getName(): string
    {
        return $this->name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->getName(); // Employee name: John Doe
```

**[⬆ back to top](#မာတိကာ)**

## Classes

### Prefer composition over inheritance

As stated famously in [*Design Patterns*](https://en.wikipedia.org/wiki/Design_Patterns) by the Gang of Four,
you should prefer composition over inheritance where you can. There are lots of
good reasons to use inheritance and lots of good reasons to use composition.
The main point for this maxim is that if your mind instinctively goes for
inheritance, try to think if composition could model your problem better. In some
cases it can.

You might be wondering then, "when should I use inheritance?" It
depends on your problem at hand, but this is a decent list of when inheritance
makes more sense than composition:

1. Your inheritance represents an "is-a" relationship and not a "has-a"
relationship (Human->Animal vs. User->UserDetails).
2. You can reuse code from the base classes (Humans can move like all animals).
3. You want to make global changes to derived classes by changing a base class.
(Change the caloric expenditure of all animals when they move).

**Bad:**

```php
class Employee 
{
    private $name;
    private $email;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    // ...
}

// Bad because Employees "have" tax data. 
// EmployeeTaxData is not a type of Employee

class EmployeeTaxData extends Employee 
{
    private $ssn;
    private $salary;
    
    public function __construct(string $name, string $email, string $ssn, string $salary)
    {
        parent::__construct($name, $email);

        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}
```

**Good:**

```php
class EmployeeTaxData 
{
    private $ssn;
    private $salary;

    public function __construct(string $ssn, string $salary)
    {
        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}

class Employee 
{
    private $name;
    private $email;
    private $taxData;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    public function setTaxData(string $ssn, string $salary)
    {
        $this->taxData = new EmployeeTaxData($ssn, $salary);
    }

    // ...
}
```

**[⬆ back to top](#မာတိကာ)**

### Avoid fluent interfaces

A [Fluent interface](https://en.wikipedia.org/wiki/Fluent_interface) is an object
oriented API that aims to improve the readability of the source code by using
[Method chaining](https://en.wikipedia.org/wiki/Method_chaining).

While there can be some contexts, frequently builder objects, where this
pattern reduces the verbosity of the code (for example the [PHPUnit Mock Builder](https://phpunit.de/manual/current/en/test-doubles.html)
or the [Doctrine Query Builder](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/query-builder.html)),
more often it comes at some costs:

1. Breaks [Encapsulation](https://en.wikipedia.org/wiki/Encapsulation_%28object-oriented_programming%29).
2. Breaks [Decorators](https://en.wikipedia.org/wiki/Decorator_pattern).
3. Is harder to [mock](https://en.wikipedia.org/wiki/Mock_object) in a test suite.
4. Makes diffs of commits harder to read.

For more informations you can read the full [blog post](https://ocramius.github.io/blog/fluent-interfaces-are-evil/)
on this topic written by [Marco Pivetta](https://github.com/Ocramius).

**Bad:**

```php
class Car
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake(string $make): self
    {
        $this->make = $make;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function setModel(string $model): self
    {
        $this->model = $model;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function setColor(string $color): self
    {
        $this->color = $color;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function dump(): void
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = (new Car())
  ->setColor('pink')
  ->setMake('Ford')
  ->setModel('F-150')
  ->dump();
```

**Good:**

```php
class Car
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake(string $make): void
    {
        $this->make = $make;
    }

    public function setModel(string $model): void
    {
        $this->model = $model;
    }

    public function setColor(string $color): void
    {
        $this->color = $color;
    }

    public function dump(): void
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = new Car();
$car->setColor('pink');
$car->setMake('Ford');
$car->setModel('F-150');
$car->dump();
```

**[⬆ back to top](#မာတိကာ)**

### Prefer final classes

The `final` should be used whenever possible:

1. It prevents uncontrolled inheritance chain.
2. It encourages [composition](#prefer-composition-over-inheritance).
3. It encourages the [Single Responsibility Pattern](#single-responsibility-principle-srp).
4. It encourages developers to use your public methods instead of extending the class to get access on protected ones.
5. It allows you to change your code without any break of applications that use your class.

The only condition is that your class should implement an interface and no other public methods are defined.

For more informations you can read [the blog post](https://ocramius.github.io/blog/when-to-declare-classes-final/) on this topic written by [Marco Pivetta (Ocramius)](https://ocramius.github.io/).

**Bad:**

```php
final class Car
{
    private $color;
    
    public function __construct($color)
    {
        $this->color = $color;
    }
    
    /**
     * @return string The color of the vehicle
     */
    public function getColor() 
    {
        return $this->color;
    }
}
```

**Good:**

```php
interface Vehicle
{
    /**
     * @return string The color of the vehicle
     */
    public function getColor();
}

final class Car implements Vehicle
{
    private $color;
    
    public function __construct($color)
    {
        $this->color = $color;
    }
    
    /**
     * {@inheritdoc}
     */
    public function getColor() 
    {
        return $this->color;
    }
}
```

**[⬆ back to top](#မာတိကာ)**

## SOLID

**SOLID** is the mnemonic acronym introduced by Michael Feathers for the first five principles named by Robert Martin, which meant five basic principles of object-oriented programming and design.

 * [S: Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
 * [O: Open/Closed Principle (OCP)](#openclosed-principle-ocp)
 * [L: Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
 * [I: Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
 * [D: Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)

### Single Responsibility Principle (SRP)

As stated in Clean Code, "There should never be more than one reason for a class
to change". It's tempting to jam-pack a class with a lot of functionality, like
when you can only take one suitcase on your flight. The issue with this is
that your class won't be conceptually cohesive and it will give it many reasons
to change. Minimizing the amount of times you need to change a class is important.
It's important because if too much functionality is in one class and you modify a piece of it,
it can be difficult to understand how that will affect other dependent modules in
your codebase.

**Bad:**

```php
class UserSettings
{
    private $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }

    public function changeSettings(array $settings): void
    {
        if ($this->verifyCredentials()) {
            // ...
        }
    }

    private function verifyCredentials(): bool
    {
        // ...
    }
}
```

**Good:**

```php
class UserAuth 
{
    private $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }
    
    public function verifyCredentials(): bool
    {
        // ...
    }
}

class UserSettings 
{
    private $user;
    private $auth;

    public function __construct(User $user) 
    {
        $this->user = $user;
        $this->auth = new UserAuth($user);
    }

    public function changeSettings(array $settings): void
    {
        if ($this->auth->verifyCredentials()) {
            // ...
        }
    }
}
```

**[⬆ back to top](#မာတိကာ)**

### Open/Closed Principle (OCP)

As stated by Bertrand Meyer, "software entities (classes, modules, functions,
etc.) should be open for extension, but closed for modification." What does that
mean though? This principle basically states that you should allow users to
add new functionalities without changing existing code.

**Bad:**

```php
abstract class Adapter
{
    protected $name;

    public function getName(): string
    {
        return $this->name;
    }
}

class AjaxAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'ajaxAdapter';
    }
}

class NodeAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'nodeAdapter';
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch(string $url): Promise
    {
        $adapterName = $this->adapter->getName();

        if ($adapterName === 'ajaxAdapter') {
            return $this->makeAjaxCall($url);
        } elseif ($adapterName === 'httpNodeAdapter') {
            return $this->makeHttpCall($url);
        }
    }

    private function makeAjaxCall(string $url): Promise
    {
        // request and return promise
    }

    private function makeHttpCall(string $url): Promise
    {
        // request and return promise
    }
}
```

**Good:**

```php
interface Adapter
{
    public function request(string $url): Promise;
}

class AjaxAdapter implements Adapter
{
    public function request(string $url): Promise
    {
        // request and return promise
    }
}

class NodeAdapter implements Adapter
{
    public function request(string $url): Promise
    {
        // request and return promise
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch(string $url): Promise
    {
        return $this->adapter->request($url);
    }
}
```

**[⬆ back to top](#မာတိကာ)**

### Liskov Substitution Principle (LSP)

This is a scary term for a very simple concept. It's formally defined as "If S
is a subtype of T, then objects of type T may be replaced with objects of type S
(i.e., objects of type S may substitute objects of type T) without altering any
of the desirable properties of that program (correctness, task performed,
etc.)." That's an even scarier definition.

The best explanation for this is if you have a parent class and a child class,
then the base class and child class can be used interchangeably without getting
incorrect results. This might still be confusing, so let's take a look at the
classic Square-Rectangle example. Mathematically, a square is a rectangle, but
if you model it using the "is-a" relationship via inheritance, you quickly
get into trouble.

**Bad:**

```php
class Rectangle
{
    protected $width = 0;
    protected $height = 0;

    public function setWidth(int $width): void
    {
        $this->width = $width;
    }

    public function setHeight(int $height): void
    {
        $this->height = $height;
    }

    public function getArea(): int
    {
        return $this->width * $this->height;
    }
}

class Square extends Rectangle
{
    public function setWidth(int $width): void
    {
        $this->width = $this->height = $width;
    }

    public function setHeight(int $height): void
    {
        $this->width = $this->height = $height;
    }
}

function printArea(Rectangle $rectangle): void
{
    $rectangle->setWidth(4);
    $rectangle->setHeight(5);
 
    // BAD: Will return 25 for Square. Should be 20.
    echo sprintf('%s has area %d.', get_class($rectangle), $rectangle->getArea()).PHP_EOL;
}

$rectangles = [new Rectangle(), new Square()];

foreach ($rectangles as $rectangle) {
    printArea($rectangle);
}
```

**Good:**

The best way is separate the quadrangles and allocation of a more general subtype for both shapes.

Despite the apparent similarity of the square and the rectangle, they are different.
A square has much in common with a rhombus, and a rectangle with a parallelogram, but they are not subtype.
A square, a rectangle, a rhombus and a parallelogram are separate shapes with their own properties, albeit similar.

```php
interface Shape
{
    public function getArea(): int;
}

class Rectangle implements Shape
{
    private $width = 0;
    private $height = 0;

    public function __construct(int $width, int $height)
    {
        $this->width = $width;
        $this->height = $height;
    }

    public function getArea(): int
    {
        return $this->width * $this->height;
    }
}

class Square implements Shape
{
    private $length = 0;

    public function __construct(int $length)
    {
        $this->length = $length;
    }

    public function getArea(): int
    {
        return $this->length ** 2;
    }
}

function printArea(Shape $shape): void
{
    echo sprintf('%s has area %d.', get_class($shape), $shape->getArea()).PHP_EOL;
}

$shapes = [new Rectangle(4, 5), new Square(5)];

foreach ($shapes as $shape) {
    printArea($shape);
}
```

**[⬆ back to top](#မာတိကာ)**

### Interface Segregation Principle (ISP)

ISP states that "Clients should not be forced to depend upon interfaces that
they do not use." 

A good example to look at that demonstrates this principle is for
classes that require large settings objects. Not requiring clients to set up
huge amounts of options is beneficial, because most of the time they won't need
all of the settings. Making them optional helps prevent having a "fat interface".

**Bad:**

```php
interface Employee
{
    public function work(): void;

    public function eat(): void;
}

class Human implements Employee
{
    public function work(): void
    {
        // ....working
    }

    public function eat(): void
    {
        // ...... eating in lunch break
    }
}

class Robot implements Employee
{
    public function work(): void
    {
        //.... working much more
    }

    public function eat(): void
    {
        //.... robot can't eat, but it must implement this method
    }
}
```

**Good:**

Not every worker is an employee, but every employee is a worker.

```php
interface Workable
{
    public function work(): void;
}

interface Feedable
{
    public function eat(): void;
}

interface Employee extends Feedable, Workable
{
}

class Human implements Employee
{
    public function work(): void
    {
        // ....working
    }

    public function eat(): void
    {
        //.... eating in lunch break
    }
}

// robot can only work
class Robot implements Workable
{
    public function work(): void
    {
        // ....working
    }
}
```

**[⬆ back to top](#မာတိကာ)**

### Dependency Inversion Principle (DIP)

This principle states two essential things:
1. High-level modules should not depend on low-level modules. Both should
depend on abstractions.
2. Abstractions should not depend upon details. Details should depend on
abstractions.

This can be hard to understand at first, but if you've worked with PHP frameworks (like Symfony), you've seen an implementation of this principle in the form of Dependency
Injection (DI). While they are not identical concepts, DIP keeps high-level
modules from knowing the details of its low-level modules and setting them up.
It can accomplish this through DI. A huge benefit of this is that it reduces
the coupling between modules. Coupling is a very bad development pattern because
it makes your code hard to refactor.

**Bad:**

```php
class Employee
{
    public function work(): void
    {
        // ....working
    }
}

class Robot extends Employee
{
    public function work(): void
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage(): void
    {
        $this->employee->work();
    }
}
```

**Good:**

```php
interface Employee
{
    public function work(): void;
}

class Human implements Employee
{
    public function work(): void
    {
        // ....working
    }
}

class Robot implements Employee
{
    public function work(): void
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage(): void
    {
        $this->employee->work();
    }
}
```

**[⬆ back to top](#မာတိကာ)**

## Don’t repeat yourself (DRY)

Try to observe the [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) principle.

Do your absolute best to avoid duplicate code. Duplicate code is bad because 
it means that there's more than one place to alter something if you need to 
change some logic.

Imagine if you run a restaurant and you keep track of your inventory: all your 
tomatoes, onions, garlic, spices, etc. If you have multiple lists that
you keep this on, then all have to be updated when you serve a dish with
tomatoes in them. If you only have one list, there's only one place to update!

Often you have duplicate code because you have two or more slightly
different things, that share a lot in common, but their differences force you
to have two or more separate functions that do much of the same things. Removing 
duplicate code means creating an abstraction that can handle this set of different 
things with just one function/module/class.

Getting the abstraction right is critical, that's why you should follow the
SOLID principles laid out in the [Classes](#classes) section. Bad abstractions can be
worse than duplicate code, so be careful! Having said this, if you can make
a good abstraction, do it! Don't repeat yourself, otherwise you'll find yourself 
updating multiple places any time you want to change one thing.

**Bad:**

```php
function showDeveloperList(array $developers): void
{
    foreach ($developers as $developer) {
        $expectedSalary = $developer->calculateExpectedSalary();
        $experience = $developer->getExperience();
        $githubLink = $developer->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}

function showManagerList(array $managers): void
{
    foreach ($managers as $manager) {
        $expectedSalary = $manager->calculateExpectedSalary();
        $experience = $manager->getExperience();
        $githubLink = $manager->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Good:**

```php
function showList(array $employees): void
{
    foreach ($employees as $employee) {
        $expectedSalary = $employee->calculateExpectedSalary();
        $experience = $employee->getExperience();
        $githubLink = $employee->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Very good:**

It is better to use a compact version of the code.

```php
function showList(array $employees): void
{
    foreach ($employees as $employee) {
        render([
            $employee->calculateExpectedSalary(),
            $employee->getExperience(),
            $employee->getGithubLink()
        ]);
    }
}
```

**[⬆ back to top](#မာတိကာ)**

## Translations

This is also available in other languages:

* :cn: **Chinese:**
   * [php-cpm/clean-code-php](https://github.com/php-cpm/clean-code-php)
* :ru: **Russian:**
   * [peter-gribanov/clean-code-php](https://github.com/peter-gribanov/clean-code-php)
* :es: **Spanish:**
   * [fikoborquez/clean-code-php](https://github.com/fikoborquez/clean-code-php)
* :brazil: **Portuguese:**
   * [fabioars/clean-code-php](https://github.com/fabioars/clean-code-php)
   * [jeanjar/clean-code-php](https://github.com/jeanjar/clean-code-php/tree/pt-br)
* :thailand: **Thai:**
   * [panuwizzle/clean-code-php](https://github.com/panuwizzle/clean-code-php)
* :fr: **French:**
   * [errorname/clean-code-php](https://github.com/errorname/clean-code-php)
* :vietnam: **Vietnamese**
   * [viethuongdev/clean-code-php](https://github.com/viethuongdev/clean-code-php)
* :kr: **Korean:**
   * [yujineeee/clean-code-php](https://github.com/yujineeee/clean-code-php)
   
**[⬆ back to top](#မာတိကာ)**
