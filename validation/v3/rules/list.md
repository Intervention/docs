# Available Validation Rules
## The following validation rules are available with this package

## Postal Code

The field under validation must be a [postal code](https://en.wikipedia.org/wiki/Postal_code) of the given country.

    public Intervention\Validation\Rules\Postalcode::__construct(string $countrycode)

#### Parameters

**countrycode**

Country code in [ISO-639-1](https://en.wikipedia.org/wiki/ISO_639-1) format.

### Postal Code (static instantiation)

    public static Intervention\Validation\Rules\Postalcode::countrycode(string $countrycode): Postalcode

#### Parameters

**countrycode**

Country code in [ISO-639-1](https://en.wikipedia.org/wiki/ISO_639-1) format.

### Postal Code (static instantiation with callback)

    public static Intervention\Validation\Rules\Postalcode::resolve(callable $callback): Postalcode

#### Parameters

**callback**

Callback to resolve [ISO-639-1](https://en.wikipedia.org/wiki/ISO_639-1) country code from other source.

### Postal Code (static instantiation with reference)

    public static Intervention\Validation\Rules\Postalcode::reference(string $reference): Postalcode

#### Parameters

**reference**

Reference key to get [ISO-639-1](https://en.wikipedia.org/wiki/ISO_639-1) country code from other data in validator.



