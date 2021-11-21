



## International Standard Serial Number (ISSN)

Checks for a valid [International Standard Serial Number](https://en.wikipedia.org/wiki/International_Standard_Serial_Number) (ISSN).

    public Intervention\Validation\Rules\Issn::__construct()







## JSON Web Token (JWT)

The given value must be a in format of a [JSON Web Token](https://en.wikipedia.org/wiki/JSON_Web_Token).

    public Intervention\Validation\Rules\Jwt::__construct()

## Kebab case string

The given value must be formated in [Kebab case](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles).

    public Intervention\Validation\Rules\Kebabcase::__construct()

## Lower case string 

The given value must be all lower case letters.

    public Intervention\Validation\Rules\Lowercase::__construct()

## Luhn algorithm

The given value must verify against its included [Luhn algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm) check digit.

    public Intervention\Validation\Rules\Luhn::__construct()

## MAC address 

The field under validation must be a [media access control address](https://en.wikipedia.org/wiki/MAC_address) (MAC address).

    public Intervention\Validation\Rules\MacAddress::__construct()

## Media (MIME) type

Checks for a valid [Mime Type](https://en.wikipedia.org/wiki/Media_type) (Media type).

    public Intervention\Validation\Rules\MimeType::__construct()

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

## Semantic Version Number

The field under validation must be a valid version numbers using [Semantic Versioning](https://semver.org/).

    public Intervention\Validation\Rules\SemVer::__construct()

## SEO-friendly short text (Slug)

The field under validation must be a user- and [SEO-friendly short text](https://en.wikipedia.org/wiki/Clean_URL#Slug).

    public Intervention\Validation\Rules\Slug::__construct()

## Snake case string

The field under validation must formated as [Snake case](https://en.wikipedia.org/wiki/Snake_case) text.

    public Intervention\Validation\Rules\Snakecase::__construct()

## Title case string

The field under validation must formated in [Title case](https://en.wikipedia.org/wiki/Title_case).

    public Intervention\Validation\Rules\Titlecase::__construct()

## Universally Unique Lexicographically Sortable Identifier (ULID)

The field under validation must be a valid [Universally Unique Lexicographically Sortable Identifier](https://github.com/ulid/spec).

    public Intervention\Validation\Rules\Ulid::__construct()

## Upper case string

The field under validation must be all upper case.

    public Intervention\Validation\Rules\Uppercase::__construct()

## Username

The field under validation must be a valid username. Consisting of alpha-numeric characters, underscores, minus and starting with a alphabetic character. Multiple underscore and minus chars are not allowed. Underscore and minus chars are not allowed at the beginning or end.

    public Intervention\Validation\Rules\Username::__construct()