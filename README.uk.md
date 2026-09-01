# Laravel Helpers

[English](README.md) · **Українська**

Один `require`, який ставить усі DJZT-хелпери для Laravel.

```bash
composer require djzt/laravel-helpers
```

Це Composer-**метапакет**: власного коду він не має — лише перелік пакетів нижче.
Усі провайдери підхоплюються автоматично, реєструвати нічого не треба.

## Що входить

| Пакет | Що робить | Документація |
| --- | --- | --- |
| [`djzt/laravel-request-helper`](https://github.com/DJZT/laravel-request-helper) | Типізовані аксесори запиту — `nullable*`, `optional*` і `required*`, з маркером `Optional`, який розрізняє «немає ключа», «null» і «0» | [README](https://github.com/DJZT/laravel-request-helper#readme) |
| [`djzt/laravel-resource-helper`](https://github.com/DJZT/laravel-resource-helper) | Хелпери для API Resources — єдиний формат дат у всьому API з конфіга, плюс гроші, числа, enum-и, файли та умовні атрибути | [README](https://github.com/DJZT/laravel-resource-helper#readme) |

```php
// djzt/laravel-request-helper
$request->requiredInteger('qty');   // int               — 422, якщо ключа немає, він null або не приводиться
$request->optionalString('name');   // string|null|Optional

// djzt/laravel-resource-helper
'created_at' => $this->date($this->created_at),   // "2026-09-01"
'price'      => $this->money($this->price),       // "1999.50"
```

Потрібні PHP 8.2+ і Laravel 12 або 13.

## Потрібен лише один?

Ставте його напряму — пакети незалежні й жоден із них не залежить від цього:

```bash
composer require djzt/laravel-request-helper
```

Метапакет поряд з окремим пакетом нічому не шкодить: Composer зведе їх до тієї
самої інсталяції.

## Як додати новий хелпер

1. Опублікуйте новий пакет окремо (свій репозиторій, свої теги, Packagist).
2. Додайте його в `require` тут, з `^`-обмеженням на перший стабільний мінор.
3. Поставте тег нового мінора метапакета.

Оскільки метапакет не містить нічого, крім блоку `require`, це і є весь реліз:
наявні інсталяції підхоплять новий хелпер на наступному `composer update`.

## Версіонування

Метапакет версіонується самостійно, незалежно від пакетів, на які вказує. Новий
хелпер або розширення обмеження на новий мінор наявного хелпера — це мінорний
реліз тут; вилучення пакета з набору — мажорний.

## Ліцензія

MIT. Див. [LICENSE](LICENSE).
